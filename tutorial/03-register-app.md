<!-- markdownlint-disable MD002 MD041 -->

在此练习中，你将使用 Azure Active Directory 管理中心创建新的 Azure AD Web 应用程序注册。

1. 打开浏览器，并转到 [Azure Active Directory 管理中心](https://aad.portal.azure.com)。 使用 **个人帐户**（亦称为“Microsoft 帐户”）或 **工作或学校帐户** 登录。

1. 选择左侧导航栏中的“**Azure Active Directory**”，再选择“**管理**”下的“**应用注册**”。

    ![应用注册屏幕截图 ](./images/aad-portal-app-registrations.png)

1. 选择“新注册”。 在“注册应用”页上，按如下方式设置值。

    - 将“名称”设置为“`Angular Graph Tutorial`”。
    - 将“受支持的帐户类型”设置为“任何组织目录中的帐户和个人 Microsoft 帐户”。
    - 在“重定向 URI”下，将第一个下拉列表设置为“`Single-page application (SPA)`”，并将值设置为“`http://localhost:4200`”。

    ![注册应用程序页面的屏幕截图](./images/aad-register-an-app.png)

1. 选择“**注册**”。 在 **Angular Graph 教程** 页面上，复制应用 (**客户端**) ID 并保存，下一步中将需要此值。

    ![新应用注册的应用程序 ID 的屏幕截图](./images/aad-application-id.png)
