---
title: 为 Azure Active Directory 条件访问设置 SharePoint Online 和 Exchange Online | Microsoft Docs
description: 了解如何为 Azure Active Directory 条件访问设置 SharePoint Online 和 Exchange Online。
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: mtillman
editor: ''
ms.assetid: 62349fba-3cc0-4ab5-babe-372b3389eff6
ms.service: active-directory
ms.component: conditional-access
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/15/2018
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: a5f0a17682f3481ad9a2dff5f144aa3d97f29920
ms.sourcegitcommit: cc4fdd6f0f12b44c244abc7f6bc4b181a2d05302
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2018
ms.locfileid: "47063840"
---
# <a name="how-to-set-up-sharepoint-online-and-exchange-online-for-azure-active-directory-conditional-access"></a>如何：为 Azure Active Directory 条件访问设置 SharePoint Online 和 Exchange Online 

使用 [Azure Active Directory (Azure AD) 条件访问](overview.md)，可以控制用户访问云应用的方式。 若要使用条件访问来控制对 SharePoint Online 和 Exchange Online 的访问，需要：

- 检查自己的条件访问方案是否受支持
- 防止客户端应用绕过条件访问策略的实施。   

本文介绍如何解决这两种情况。


## <a name="what-you-need-to-know"></a>需要了解的事项

如果身份验证尝试来自以下位置，可以使用 Azure AD 条件访问来保护云应用：

- Web 浏览器

- 使用[新式身份验证](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a)的客户端应用

- Exchange ActiveSync 

某些云应用还支持旧式身份验证协议。 例如，SharePoint Online 和 Exchange Online 就支持这些协议。 如果客户端应用可以使用旧式身份验证协议访问云应用，则 Azure AD 无法针对此访问尝试实施条件访问策略。 为了防止客户端应用绕过策略的实施，应该检查它是否能够做到只对受影响的云应用启用新式身份验证。 

条件访问不适用的客户端应用示例包括：

- Office 2010 和更低版本

- 未启用新式身份验证的 Office 2013



 
## <a name="control-access-to-sharepoint-online"></a>控制对 SharePoint Online 的访问

除了新式身份验证以外，SharePoint Online 还支持旧式身份验证协议。 如果已启用旧式身份验证协议，则对于不使用新式身份验证的客户端，不会实施 SharePoint 的条件访问策略。

可以使用 **[Set-SPOTenant](https://technet.microsoft.com/library/fp161390.aspx)** cmdlet 来禁用用于进行 SharePoint 访问的旧式身份验证协议。 

    Set-SPOTenant -LegacyAuthProtocolsEnabled $false

## <a name="control-access-to-exchange-online"></a>控制对 Exchange Online 的访问

为 Exchange Online 设置条件访问策略时，需要检查以下各项：

- Exchange ActiveSync

- 旧式身份验证协议



### <a name="exchange-activesync"></a>Exchange ActiveSync

尽管 Exchange Active Sync 支持新式身份验证，但对条件访问方案的支持还有一些限制：

- 只能配置设备平台条件  

    ![设备平台](./media/conditional-access-for-exo-and-spo/05.png)

- 不支持设置多重身份验证要求  

    ![条件性访问](./media/conditional-access-for-exo-and-spo/01.png)

若要有效保护从 Exchange ActiveSync 对 Exchange Online 的访问，可以：

- 遵循以下步骤配置支持的条件访问策略：

    a.在“解决方案资源管理器”中，右键单击项目文件夹下的“引用”文件夹，并单击“添加引用”。 只选择“Office 365 Exchange Online”作为云应用。  

    ![条件性访问](./media/conditional-access-for-exo-and-spo/04.png)

    b. 选择“Exchange Active Sync”作为**客户端应用**，选择“将策略仅应用到受支持的平台”。  

    ![设备平台](./media/conditional-access-for-exo-and-spo/03.png)

- 使用 Active Directory 联合身份验证服务 (AD FS) 规则阻止 Exchange ActiveSync。

        @RuleName = "Block Exchange ActiveSync"
        c1:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application", Value == "Microsoft.Exchange.ActiveSync"]
        => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "false");




### <a name="legacy-authentication-protocols"></a>旧式身份验证协议

除了新式身份验证以外，Exchange Online 还支持旧式身份验证协议。 如果已启用旧式身份验证协议，则对于不使用新式身份验证的客户端，不会实施 Exchange Online 的条件访问策略。

可以通过设置 AD FS 规则为 Exchange Online 禁用旧式身份验证协议。 这会阻止来自以下位置的访问：

- 旧版 Office 客户端，例如未启用新式身份验证的 Office 2013 

- 早期 Office 版本


## <a name="set-up-ad-fs-rules"></a>设置 AD FS 规则

可以使用以下颁发授权规则在 AD FS 级别启用或阻止流量。 

### <a name="block-legacy-traffic-from-the-extranet"></a>阻止来自 Extranet 的旧式流量

应用以下三个规则： 

- 启用对以下流量的访问：
    - Exchange ActiveSync 流量
    - 浏览器流量
    - 新式身份验证流量
- 阻止对以下流量的访问： 
    - 来自 Extranet 的旧式客户端应用

**规则 1：**

    @RuleName = "Allow all intranet traffic"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "true"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

**规则 2：**

    @RuleName = "Allow Exchange ActiveSync"
    c1:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application", Value == "Microsoft.Exchange.ActiveSync"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

**规则 3：**

    @RuleName = "Allow extranet browser and browser dialog traffic"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] &&
    c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value =~ "(/adfs/ls)|(/adfs/oauth2)"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

### <a name="block-legacy-traffic-from-anywhere"></a>阻止来自任何位置的旧式流量

应用以下三个规则：

- 启用对以下流量的访问： 
    - Exchange ActiveSync 流量
    - 浏览器流量
    - 新式身份验证流量
- 阻止对以下流量的访问： 
    - 来自任何位置的旧式应用

##### <a name="rule-1"></a>规则 1
    @RuleName = "Allow all intranet traffic only for browser and modern authentication clients"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "true"] &&
    c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value =~ "(/adfs/ls)|(/adfs/oauth2)"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");


##### <a name="rule-2"></a>规则 2
    @RuleName = "Allow Exchange ActiveSync"
    c1:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application", Value == "Microsoft.Exchange.ActiveSync"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");


##### <a name="rule-3"></a>规则 3
    @RuleName = "Allow extranet browser and browser dialog traffic"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] &&
    c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value =~ "(/adfs/ls)|(/adfs/oauth2)"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

## <a name="next-steps"></a>后续步骤

有关详细信息，请参阅 [Azure Active Directory 中的条件访问是什么](overview.md)。

有关配置声明规则的说明，请参阅[配置声明规则](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configure-claim-rules)。 






