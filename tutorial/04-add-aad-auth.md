<!-- markdownlint-disable MD002 MD041 -->

在此练习中，你将从上一练习中扩展应用程序，以支持使用 Azure AD 进行身份验证。 这是获取调用 Microsoft Graph 所需的 OAuth 访问令牌所必需的。 在此步骤中，将 [Angular 的 Microsoft 身份验证库](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-angular/README.md) 集成到应用程序中。

1. 在 **./src** 目录中新建一个名为 **oauth.ts** 的文件并添加以下代码。

    :::code language="typescript" source="../demo/graph-tutorial/src/oauth.example.ts":::

    将 `YOUR_APP_ID_HERE` 替换为应用程序注册门户中的应用程序 ID。

    > [!IMPORTANT]
    > 如果你使用的是源代码管理（如 git），那么现在应该从源代码管理中排除 **oauth.ts** 文件，以避免意外泄露应用 ID。

1. 打开 **./src/app/app.module.ts，** 将以下语句 `import` 添加到文件顶部。

    ```typescript
    import { IPublicClientApplication,
             PublicClientApplication,
             BrowserCacheLocation } from '@azure/msal-browser';
    import { MsalModule,
             MsalService,
             MSAL_INSTANCE } from '@azure/msal-angular';
    import { OAuthSettings } from '../oauth';
    ```

1. 在 语句下方添加以下 `import` 函数。

    :::code language="typescript" source="../demo/graph-tutorial/src/app/app.module.ts" id="MSALFactorySnippet":::

1. 将 `MsalModule` 添加到 `imports` 声明内的 `@NgModule` 数组。

    :::code language="typescript" source="../demo/graph-tutorial/src/app/app.module.ts" id="ImportsSnippet" highlight="6":::

1. 将 `MSALInstanceFactory` 和 `MsalService` 添加到 `providers` 声明内的 `@NgModule` 数组。

    :::code language="typescript" source="../demo/graph-tutorial/src/app/app.module.ts" id="ProvidersSnippet" highlight="2-6":::

## <a name="implement-sign-in"></a>实施登录

在此部分中，你将创建身份验证服务并实施登录和注销。

1. 在 CLI 中运行以下命令。

    ```Shell
    ng generate service auth
    ```

    通过为此创建服务，可以轻松地将该服务注入需要访问身份验证方法的任何组件。

1. 命令完成后，打开 **./src/app/auth.service.ts，** 并将其内容替换为以下代码。

    ```typescript
    import { Injectable } from '@angular/core';
    import { AccountInfo } from '@azure/msal-browser';
    import { MsalService } from '@azure/msal-angular';

    import { AlertsService } from './alerts.service';
    import { OAuthSettings } from '../oauth';
    import { User } from './user';

    @Injectable({
      providedIn: 'root'
    })

    export class AuthService {
      public authenticated: boolean;
      public user?: User;

      constructor(
        private msalService: MsalService,
        private alertsService: AlertsService) {

        this.authenticated = false;
        this.user = undefined;
      }

      // Prompt the user to sign in and
      // grant consent to the requested permission scopes
      async signIn(): Promise<void> {
        const result = await this.msalService
          .loginPopup(OAuthSettings)
          .toPromise()
          .catch((reason) => {
            this.alertsService.addError('Login failed',
              JSON.stringify(reason, null, 2));
          });

        if (result) {
          this.msalService.instance.setActiveAccount(result.account);
          this.authenticated = true;
          // Temporary placeholder
          this.user = new User();
          this.user.displayName = 'Adele Vance';
          this.user.email = 'AdeleV@contoso.com';
          this.user.avatar = '/assets/no-profile-photo.png';
        }
      }

      // Sign out
      async signOut(): Promise<void> {
        await this.msalService.logout().toPromise();
        this.user = undefined;
        this.authenticated = false;
      }

      // Silently request an access token
      async getAccessToken(): Promise<string> {
        const result = await this.msalService
          .acquireTokenSilent({
            scopes: OAuthSettings.scopes
          })
          .toPromise()
          .catch((reason) => {
            this.alertsService.addError('Get token failed', JSON.stringify(reason, null, 2));
          });

        if (result) {
          // Temporary to display token in an error box
          this.alertsService.addSuccess('Token acquired', result.accessToken);
          return result.accessToken;
        }

        // Couldn't get a token
        this.authenticated = false;
        return '';
      }
    }
    ```

1. 打开 **./src/app/nav-bar/nav-bar.component.ts，** 并将其内容替换为以下内容。

    :::code language="typescript" source="../demo/graph-tutorial/src/app/nav-bar/nav-bar.component.ts" id="navBarSnippet" highlight="3,15-22,24,34-36,38-40":::

1. 打开 **./src/app/home/home.component.ts，** 并将其内容替换为以下内容。

    :::code language="typescript" source="snippets/snippets.ts" id="homeSnippet" highlight="3,13-20,22,26-33":::

保存更改并刷新浏览器。 单击 **"单击此处登录"按钮** ，应重定向到 `https://login.microsoftonline.com` 。 使用 Microsoft 帐户登录并同意请求的权限。 应用页面应刷新，显示令牌。

### <a name="get-user-details"></a>获取用户详细信息

现在，身份验证服务为用户的邮箱和电子邮件地址显示名称常量值。 现在你已拥有访问令牌，可以从 Microsoft Graph 获取用户详细信息，以便这些值对应于当前用户。

1. 打开 **./src/app/auth.service.ts，** 将以下语句 `import` 添加到文件顶部。

    ```typescript
    import { Client } from '@microsoft/microsoft-graph-client';
    import * as MicrosoftGraph from '@microsoft/microsoft-graph-types';
    ```

1. 将新函数添加到称为 `AuthService` 的 `getUser` 类。

    :::code language="typescript" source="../demo/graph-tutorial/src/app/auth.service.ts" id="GetUserSnippet":::

1. 在 方法中查找并删除以下 `getAccessToken` 代码，以添加警报以显示访问令牌。

    ```typescript
    // Temporary to display token in an error box
    this.alertsService.addSuccess('Token acquired', result);
    ```

1. 从 方法中查找并删除以下 `signIn` 代码。

    ```typescript
    // Temporary placeholder
    this.user = new User();
    this.user.displayName = "Adele Vance";
    this.user.email = "AdeleV@contoso.com";
    this.user.avatar = '/assets/no-profile-photo.png';
    ```

1. 在它的位置，添加以下代码。

    ```typescript
    this.user = await this.getUser();
    ```

    此新代码使用 Microsoft Graph SDK 获取用户的详细信息，然后使用 API 调用返回的值 `User` 创建对象。

1. 将 `constructor` 类的 更改为检查用户是否已登录，如果已登录， `AuthService` 则加载其详细信息。 将 现有的 `constructor` 替换为以下内容。

    :::code language="typescript" source="../demo/graph-tutorial/src/app/auth.service.ts" id="ConstructorSnippet" highlight="5-7":::

1. 从 类中删除临时 `HomeComponent` 代码。 打开 **"./src/app/home/home.component.ts"，** 将现有 `signIn` 函数替换为以下内容。

    :::code language="typescript" source="../demo/graph-tutorial/src/app/home/home.component.ts" id="SignInSnippet":::

现在，如果保存更改并启动应用，登录后应最终返回主页，但 UI 应更改以指示你已登录。

![登录后主页的屏幕截图](./images/add-aad-auth-01.png)

单击右上角的用户头像以访问 **"注销"** 链接。 单击 **"注销** "将重置会话，并返回到主页。

![具有注销链接的下拉菜单的屏幕截图](./images/add-aad-auth-02.png)

## <a name="storing-and-refreshing-tokens"></a>存储和刷新令牌

此时，应用程序具有访问令牌，该令牌在 API 调用 `Authorization` 标头中发送。 这是允许应用代表用户访问 Microsoft Graph 的令牌。

但是，此令牌期很短。 令牌在颁发后一小时过期。 由于应用使用的是 MSAL 库，因此不需要实现任何令牌存储或刷新逻辑。 缓存 `MsalService` 浏览器存储中的令牌。 `acquireTokenSilent`方法首先检查缓存的令牌，如果令牌未过期，则返回它。 如果已过期，它将进行无提示请求以获取新请求。
