---
title: 教程：Azure Active Directory 与 Dovetale 的集成 | Microsoft Docs
description: 了解如何在 Azure Active Directory 与 Dovetale 之间配置单一登录。
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 81da50c3-df94-458a-8b6a-a30827ee6358
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2018
ms.author: jeedes
ms.openlocfilehash: dd2aa699c22518ebbe7f29ba8dfd296da7385476
ms.sourcegitcommit: 744747d828e1ab937b0d6df358127fcf6965f8c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "40161564"
---
# <a name="tutorial-azure-active-directory-integration-with-dovetale"></a>教程：Azure Active Directory 与 Dovetale 的集成

本教程介绍如何将 Dovetale 与 Azure Active Directory (Azure AD) 集成。

将 Dovetale 与 Azure AD 集成具有以下优势：

- 可在 Azure AD 中控制谁有权访问 Dovetale。
- 可让用户使用其 Azure AD 帐户自动登录到 Dovetale（单一登录）。
- 可在中心位置（即 Azure 门户）管理帐户。

如需了解有关 SaaS 应用与 Azure AD 集成的详细信息，请参阅 [Azure Active Directory 的应用程序访问与单一登录是什么](../manage-apps/what-is-single-sign-on.md)

## <a name="prerequisites"></a>先决条件

若要配置 Azure AD 与 Dovetale 的集成，需要以下项目：

- Azure AD 订阅
- 启用了 Dovetale 单一登录的订阅

> [!NOTE]
> 为了测试本教程中的步骤，我们不建议使用生产环境。

测试本教程中的步骤应遵循以下建议：

- 除非必要，请勿使用生产环境。
- 如果没有 Azure AD 试用环境，可以[获取一个月的试用版](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>方案描述

在本教程中，将在测试环境中测试 Azure AD 单一登录。 本教程中概述的方案包括两个主要构建基块：

1. 从库中添加 Dovetale
2. 配置和测试 Azure AD 单一登录

## <a name="adding-dovetale-from-the-gallery"></a>从库中添加 Dovetale

若要配置 Dovetale 与 Azure AD 的集成，需从库中将 Dovetale 添加到托管 SaaS 应用的列表。

**若要从库中添加 Dovetale，请执行以下步骤：**

1. 在 **[Azure 门户](https://portal.azure.com)** 的左侧导航面板中，单击“Azure Active Directory”图标。 

    ![“Azure Active Directory”按钮][1]

2. 导航到“企业应用程序”。 然后转到“所有应用程序”。

    ![“企业应用程序”边栏选项卡][2]

3. 若要添加新应用程序，请单击对话框顶部的“新建应用程序”按钮。

    ![“新增应用程序”按钮][3]

4. 在搜索框中键入“Dovetale”，在结果面板中选择“Dovetale”，然后单击“添加”按钮以添加该应用程序。

    ![结果列表中的 Dovetale](./media/dovetale-tutorial/tutorial_dovetale_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>配置和测试 Azure AD 单一登录

在本部分中，基于一个名为“Britta Simon”的测试用户使用 Dovetale 配置和测试 Azure AD 单一登录。

若要运行单一登录，Azure AD 需要知道与 Azure AD 用户相对应的 Dovetale 用户。 换句话说，需要建立 Azure AD 用户与 Dovetale 中相关用户之间的关联关系。

若要配置和测试 Dovetale 的 Azure AD 单一登录，需要完成以下构建基块：

1. **[配置 Azure AD 单一登录](#configure-azure-ad-single-sign-on)** - 使用户能够使用此功能。
2. **[创建 Azure AD 测试用户](#create-an-azure-ad-test-user)** - 使用 Britta Simon 测试 Azure AD 单一登录。
3. [创建 Dovetale 测试用户](#create-a-dovetale-test-user) - 在 Dovetale 中创建 Britta Simon 的对应用户，并将其关联到用户的 Azure AD 表示形式。
4. **[分配 Azure AD 测试用户](#assign-the-azure-ad-test-user)** - 使 Britta Simon 能够使用 Azure AD 单一登录。
5. **[测试单一登录](#test-single-sign-on)** - 验证配置是否正常工作。

### <a name="configure-azure-ad-single-sign-on"></a>配置 Azure AD 单一登录

在本部分中，将在 Azure 门户中启用 Azure AD 单一登录并在 Dovetale 应用程序中配置单一登录。

**若要配置 Dovetale 的 Azure AD 单一登录，请执行以下步骤：**

1. 在 Azure 门户的 **Dovetale** 应用程序集成页上，单击“单一登录”。

    ![配置单一登录链接][4]

2. 在“单一登录”对话框中，选择“基于 SAML 的单一登录”作为“模式”以启用单一登录。

    ![“单一登录”对话框](./media/dovetale-tutorial/tutorial_dovetale_samlbase.png)

3. 在“Dovetale 域和 URL”部分，如果你要在“IDP 发起的模式”下配置应用程序，用户无需执行任何步骤，因为应用已与 Azure 进行预集成：

    ![Dovetale 域和 URL 单一登录信息](./media/dovetale-tutorial/tutorial_dovetale_url1.png)

4. 如果要在 SP 发起的模式下配置应用程序，请选中“显示高级 URL 设置”，并执行以下步骤：

    ![Dovetale 域和 URL 单一登录信息](./media/dovetale-tutorial/tutorial_dovetale_url2.png)

    在“登录 URL”文本框中，使用以下模式键入 URL： `<COMPANYNAME>.dovetale.com`

    > [!NOTE]
    > 此值不是真实值。 使用实际登录 URL 更新此值。 请联系 [Dovetale 客户端支持团队](mailto:support@dovetale.com)以获取此值。

5. Dovetale 应用程序需要特定格式的 SAML 断言。 请为此应用程序配置以下声明。 可以在应用程序集成页的“用户属性”部分管理这些属性的值。 以下屏幕截图显示一个示例。
    
    ![配置单一登录](./media/dovetale-tutorial/tutorial_attribute.png)

6. 在“用户属性”部分中，单击“查看和编辑所有其他用户属性”复选框展开属性。 对显示的各个属性执行以下步骤：

    | 属性名称 | 属性值 |
    | ---------------| --------------- |
    | 电子邮件 | user.mail |
    | first_name | user.givenname |
    | 名称 | user.userprincipalname |
    | last_name | user.surname |

    a. 单击“添加属性”，打开“添加属性”对话框。

    ![配置单一登录](./media/dovetale-tutorial/tutorial_attribute_04.png)

    ![配置单一登录](./media/dovetale-tutorial/tutorial_attribute_05.png)

    b. 在“名称”文本框中，键入为该行显示的**属性名称**。

    c. 在“值”列表中，选择为该行显示的属性值。

    d. 将“命名空间”值保留空白。

    e. 单击“确定” 。

7. 在“SAML 签名证书”部分上，单击”复制”按钮来复制**应用联合元数据 URL**，并将其粘贴到记事本。

    ![证书下载链接](./media/dovetale-tutorial/tutorial_dovetale_certificate.png) 

8. 单击“保存”按钮。

    ![配置单一登录“保存”按钮](./media/dovetale-tutorial/tutorial_general_400.png)

9. 在“Dovetale 配置”部分，单击“配置 Dovetale”打开“配置登录”窗口。 从“快速参考”部分中复制“SAML 实体 ID 和 SAML 单一登录服务 URL”。

    ![Dovetale 配置](./media/dovetale-tutorial/tutorial_dovetale_configure.png)

10. 若要在 **Dovetale** 端配置单一登录，需要将**应用联合元数据 URL、SAML 实体 ID 和 SAML 单一登录服务 URL** 发送给 [Dovetale 支持团队](mailto:support@dovetale.com)。 他们会对此进行设置，使两端的 SAML SSO 连接均正确设置。

### <a name="create-an-azure-ad-test-user"></a>创建 Azure AD 测试用户

本部分的目的是在 Azure 门户中创建名为 Britta Simon 的测试用户。

   ![创建 Azure AD 测试用户][100]

**若要在 Azure AD 中创建测试用户，请执行以下步骤：**

1. 在 Azure 门户的左窗格中，单击“Azure Active Directory”按钮。

    ![“Azure Active Directory”按钮](./media/dovetale-tutorial/create_aaduser_01.png)

2. 若要显示用户列表，请转到“用户和组”，然后单击“所有用户”。

    ![“用户和组”以及“所有用户”链接](./media/dovetale-tutorial/create_aaduser_02.png)

3. 若要打开“用户”对话框，在“所有用户”对话框顶部单击“添加”。

    ![“添加”按钮](./media/dovetale-tutorial/create_aaduser_03.png)

4. 在“用户”对话框中，执行以下步骤：

    ![“用户”对话框](./media/dovetale-tutorial/create_aaduser_04.png)

    a. 在“姓名”框中，键入“BrittaSimon”。

    b. 在“用户名”框中，键入用户 Britta Simon 的电子邮件地址。

    c. 选中“显示密码”复选框，然后记下“密码”框中显示的值。

    d. 单击“创建”。

### <a name="create-a-dovetale-test-user"></a>创建 Dovetale 测试用户

本部分的目的是在 Dovetale 中创建名为“Britta Simon”的用户。 Dovetale 支持在默认情况下启用的恰时预配。 此部分不存在任何操作项。 如果尚不存在用户，则在尝试访问 Dovetale 期间创建新用户。

> [!Note]
> 如果需要手动创建用户，请联系 [Dovetale 支持团队](mailto:support@dovetale.com)。

### <a name="assign-the-azure-ad-test-user"></a>分配 Azure AD 测试用户

在本部分中，通过向 Britta Simon 授予 Dovetale 的访问权限支持她使用 Azure 单一登录。

![分配用户角色][200]

**若要将 Britta Simon 分配到 Dovetale，请执行以下步骤：**

1. 在 Azure 门户中打开应用程序视图，导航到目录视图，接着转到“企业应用程序”，并单击“所有应用程序”。

    ![分配用户][201]

2. 在应用程序列表中，选择“Dovetale”。

    ![应用程序列表中的 Dovetale 链接](./media/dovetale-tutorial/tutorial_dovetale_app.png)  

3. 在左侧菜单中，单击“用户和组”。

    ![“用户和组”链接][202]

4. 单击“添加”按钮。 然后在“添加分配”对话框中选择“用户和组”。

    ![“添加分配”窗格][203]

5. 在“用户和组”对话框的“用户”列表中，选择“Britta Simon”。

6. 在“用户和组”对话框中单击“选择”按钮。

7. 在“添加分配”对话框中单击“分配”按钮。

### <a name="test-single-sign-on"></a>测试单一登录

在本部分中，使用访问面板测试 Azure AD 单一登录配置。

在访问面板中单击“Dovetale”磁贴即会自动登录到 Dovetale 应用程序。
有关访问面板的详细信息，请参阅 [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md)（访问面板简介）。

## <a name="additional-resources"></a>其他资源

* [有关如何将 SaaS 应用与 Azure Active Directory 集成的教程列表](tutorial-list.md)
* [什么是使用 Azure Active Directory 的应用程序访问和单一登录？](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/dovetale-tutorial/tutorial_general_01.png
[2]: ./media/dovetale-tutorial/tutorial_general_02.png
[3]: ./media/dovetale-tutorial/tutorial_general_03.png
[4]: ./media/dovetale-tutorial/tutorial_general_04.png

[100]: ./media/dovetale-tutorial/tutorial_general_100.png

[200]: ./media/dovetale-tutorial/tutorial_general_200.png
[201]: ./media/dovetale-tutorial/tutorial_general_201.png
[202]: ./media/dovetale-tutorial/tutorial_general_202.png
[203]: ./media/dovetale-tutorial/tutorial_general_203.png