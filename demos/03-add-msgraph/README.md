# <a name="how-to-run-the-completed-project"></a>如何运行已完成的项目

## <a name="prerequisites"></a>先决条件

若要在此文件夹中运行已完成的项目, 您需要以下各项:

- 在开发计算机上安装了[node.js](https://nodejs.org) 。 如果您没有 node.js, 请访问上一个链接 "下载选项"。 (**注意:** 本教程是使用节点版本10.7.0 编写的。 本指南中的步骤可能适用于其他版本, 但尚未经过测试。
- 在开发计算机上安装了[角度 CLI](https://cli.angular.io/) 。
- 使用 Outlook.com 上的邮箱的个人 Microsoft 帐户, 或者是 Microsoft 工作或学校帐户。

如果你没有 Microsoft 帐户, 可以使用以下几种方法获取免费帐户:

- 你可以[注册新的个人 Microsoft 帐户](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1)。
- 你可以[注册 office 365 开发人员计划](https://developer.microsoft.com/office/dev-program)以获取免费的 office 365 订阅。

## <a name="register-a-web-application-with-the-azure-active-directory-admin-center"></a>向 Azure Active Directory 管理中心注册 web 应用程序

1. 打开浏览器，并转到 [Azure Active Directory 管理中心](https://aad.portal.azure.com)。 使用**个人帐户**（亦称为“Microsoft 帐户”）或**工作或学校帐户**登录。

1. 在左侧导航栏中选择 " **Azure Active Directory** ", 然后选择 "**管理**" 下的 "**应用程序注册**"。

    ![应用注册的屏幕截图 ](/tutorial/images/aad-portal-app-registrations.png)

1. 选择“新注册”****。 在“注册应用”**** 页上，按如下方式设置值。

    - 将“名称”**** 设置为“`Angular Graph Tutorial`”。
    - 将“受支持的帐户类型”**** 设置为“任何组织目录中的帐户和个人 Microsoft 帐户”****。
    - 在“重定向 URI”**** 下，将第一个下拉列表设置为“`Web`”，并将值设置为“`http://localhost:4200`”。

    !["注册应用程序" 页的屏幕截图](/tutorial/images/aad-register-an-app.png)

1. 选择“注册”****。 在 "**角度图" 教程**页上, 复制**应用程序 (客户端) ID**的值并保存它, 下一步将需要它。

    ![新应用注册的应用程序 ID 的屏幕截图](/tutorial/images/aad-application-id.png)

1. 选择“管理”**** 下的“身份验证”****。 找到 "**隐式授予**" 部分并启用**访问令牌**和**ID 令牌**。 选择“**保存**”。

    ![隐式 grant 部分的屏幕截图](/tutorial/images/aad-implicit-grant.png)

## <a name="configure-the-sample"></a>配置示例

1. 将`oauth.ts.example`文件重命名`oauth.ts`为。
1. 编辑`oauth.ts`文件并进行以下更改。
    1. 将`YOUR_APP_ID_HERE`替换为你从应用注册门户获取的**应用程序 Id** 。
1. 在命令行界面 (CLI) 中, 导航到此目录并运行以下命令以安装要求。

    ```Shell
    npm install
    ```

## <a name="run-the-sample"></a>运行示例

1. 在 CLI 中运行以下命令以启动应用程序。

    ```Shell
    ng serve
    ```

1. 打开浏览器，然后转到 `http://localhost:4200`。