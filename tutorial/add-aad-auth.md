<!-- markdownlint-disable MD002 MD041 -->

在本练习中, 你将扩展上一练习中的应用程序, 以支持 Azure AD 的身份验证。 若要获取所需的 OAuth 访问令牌以调用 Microsoft Graph, 这是必需的。 在此步骤中, 将[Microsoft 身份验证库的角度](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-angular/README.md)集成到应用程序中。

在名为`./src` `oauth.ts`的目录中创建一个新文件, 并添加以下代码。

```TypeScript
export const OAuthSettings = {
  appId: 'YOUR_APP_ID_HERE',
  scopes: [
    "user.read",
    "calendars.read"
  ]
};
```

将`YOUR_APP_ID_HERE`替换为应用程序注册门户中的应用程序 ID。

> [!IMPORTANT]
> 如果您使用的是源代码管理 (如 git), 现在可以从源代码管理中排除`oauth.ts`该文件, 以避免无意中泄漏您的应用程序 ID。

打开`./src/app/app.module.ts`并将以下`import`语句添加到文件顶部。

```TypeScript
import { MsalModule } from '@azure/msal-angular';
import { OAuthSettings } from '../oauth';
```

然后, 将`MsalModule`添加到`imports` `@NgModule`声明中的数组, 并使用应用 ID 对它进行初始化。

```TypeScript
imports: [
  BrowserModule,
  AppRoutingModule,
  NgbModule,
  FontAwesomeModule,
  MsalModule.forRoot({
    clientID: OAuthSettings.appId
  })
],
```

## <a name="implement-sign-in"></a>实施登录

首先定义一个简单`User`的类来保存有关应用程序显示的用户的信息。 在名为`./src/app` `user.ts`的文件夹中创建一个新文件, 并添加以下代码。

```TypeScript
export class User {
  displayName: string;
  email: string;
  avatar: string;
}
```

现在, 创建身份验证服务。 通过为此创建服务, 可以轻松地将其插入到任何需要访问身份验证方法的组件中。 在 CLI 中运行以下命令。

```Shell
ng generate service auth
```

命令完成后, 打开`./src/app/auth.service.ts`文件并将其内容替换为以下代码。

```TypeScript
import { Injectable } from '@angular/core';
import { MsalService } from '@azure/msal-angular';

import { AlertsService } from './alerts.service';
import { OAuthSettings } from '../oauth';
import { User } from './user';

@Injectable({
  providedIn: 'root'
})
export class AuthService {
  public authenticated: boolean;
  public user: User;

  constructor(
    private msalService: MsalService,
    private alertsService: AlertsService) {

    this.authenticated = false;
    this.user = null;
  }

  // Prompt the user to sign in and
  // grant consent to the requested permission scopes
  async signIn(): Promise<void> {
    let result = await this.msalService.loginPopup(OAuthSettings.scopes)
      .catch((reason) => {
        this.alertsService.add('Login failed', JSON.stringify(reason, null, 2));
      });

    if (result) {
      this.authenticated = true;
      // Temporary placeholder
      this.user = new User();
      this.user.displayName = "Adele Vance";
      this.user.email = "AdeleV@contoso.com";
    }
  }

  // Sign out
  signOut(): void {
    this.msalService.logout();
    this.user = null;
    this.authenticated = false;
  }

  // Silently request an access token
  async getAccessToken(): Promise<string> {
    let result = await this.msalService.acquireTokenSilent(OAuthSettings.scopes)
      .catch((reason) => {
        this.alertsService.add('Get token failed', JSON.stringify(reason, null, 2));
      });

    // Temporary to display token in an error box
    if (result) this.alertsService.add('Token acquired', result);
    return result;
  }
}
```

现在, 你已拥有身份验证服务, 可以将其注入到执行登录的组件中。 从开始`NavBarComponent`。 打开`./src/app/nav-bar/nav-bar.component.ts`文件并进行以下更改。

- 添加`import { AuthService } from '../auth.service';`到文件顶部。
- 从类`authenticated`中`user`移除和属性, 并移除设置它们的代码`ngOnInit`。
- `AuthService`通过将以下参数添加到`constructor`: `private authService: AuthService`来插入。
- 将现有`signIn`的方法替换为以下内容:

    ```TypeScript
    async signIn(): Promise<void> {
      await this.authService.signIn();
    }
    ```

- 将现有`signOut`的方法替换为以下内容:

    ```TypeScript
    signOut(): void {
      this.authService.signOut();
    }
    ```

完成后, 代码应类似于以下代码。

```TypeScript
import { Component, OnInit } from '@angular/core';

import { AuthService } from '../auth.service';

@Component({
  selector: 'app-nav-bar',
  templateUrl: './nav-bar.component.html',
  styleUrls: ['./nav-bar.component.css']
})
export class NavBarComponent implements OnInit {

  // Should the collapsed nav show?
  showNav: boolean;

  constructor(private authService: AuthService) { }

  ngOnInit() {
    this.showNav = false;
  }

  // Used by the Bootstrap navbar-toggler button to hide/show
  // the nav in a collapsed state
  toggleNavBar(): void {
    this.showNav = !this.showNav;
  }

  async signIn(): Promise<void> {
    await this.authService.signIn();
  }

  signOut(): void {
    this.authService.signOut();
  }
}
```

由于在类上`authenticated`删除`user`了和属性, 因此还需要更新`./src/app/nav-bar/nav-bar.component.html`文件。 打开该文件并进行以下更改。

- 将的`authenticated`所有实例都`authService.authenticated`替换为。
- 将的`user`的所有实例`authService.user`都替换为。

下一步`HomeComponent`更新该类。 在中`./src/app/home/home.component.ts`对`NavBarComponent`类进行所有相同的更改, 但以下情况除外。

- `HomeComponent`类中没有`signOut`方法。
- 将`signIn`方法替换为略有不同的版本。 此代码调用`getAccessToken`获取访问令牌, 该令牌现在会将令牌输出为错误。

    ```TypeScript
    async signIn(): Promise<void> {
      await this.authService.signIn();

      // Temporary to display the token
      if (this.authService.authenticated) {
        let token = await this.authService.getAccessToken();
      }
    }
    ```

完成后, 文件应如下所示。

```TypeScript
import { Component, OnInit } from '@angular/core';
import { AuthService } from '../auth.service';

@Component({
  selector: 'app-home',
  templateUrl: './home.component.html',
  styleUrls: ['./home.component.css']
})
export class HomeComponent implements OnInit {

  constructor(private authService: AuthService) { }

  ngOnInit() {
  }

  async signIn(): Promise<void> {
    await this.authService.signIn();

    // Temporary to display the token
    if (this.authService.authenticated) {
      let token = await this.authService.getAccessToken();
    }
  }
}
```

最后, 在中`./src/app/home/home.component.html`对导航栏进行相同的替换。

保存所做的更改并刷新浏览器。 单击 "**单击此处进行登录**" 按钮, 您应被重定向`https://login.microsoftonline.com`到。 使用你的 Microsoft 帐户登录, 并同意请求的权限。 应用程序页面应刷新, 并显示令牌。

### <a name="get-user-details"></a>获取用户详细信息

现在, 身份验证服务为用户的显示名称和电子邮件地址设置常量值。 现在, 你已拥有访问令牌, 可以从 Microsoft Graph 获取用户详细信息, 以便这些值与当前用户相对应。 打开`./src/app/auth.service.ts`并将以下`import`语句添加到文件顶部。

```TypeScript
import { Client } from '@microsoft/microsoft-graph-client';
```

将新函数添加到称为 `AuthService` 的 `getUser` 类。

```TypeScript
private async getUser(): Promise<User> {
  if (!this.authenticated) return null;

  let graphClient = Client.init({
    // Initialize the Graph client with an auth
    // provider that requests the token from the
    // auth service
    authProvider: async(done) => {
      let token = await this.getAccessToken()
        .catch((reason) => {
          done(reason, null);
        });

      if (token)
      {
        done(null, token);
      } else {
        done("Could not get an access token", null);
      }
    }
  });

  // Get the user from Graph (GET /me)
  let graphUser = await graphClient.api('/me').get();

  let user = new User();
  user.displayName = graphUser.displayName;
  // Prefer the mail property, but fall back to userPrincipalName
  user.email = graphUser.mail || graphUser.userPrincipalName;

  return user;
}
```

从`signIn`方法中找到并删除以下代码。

```TypeScript
// Temporary placeholder
this.user = new User();
this.user.displayName = "Adele Vance";
this.user.email = "AdeleV@contoso.com";
```

在其位置添加以下代码。

```TypeScript
this.user = await this.getUser();
```

此新代码使用 Microsoft Graph SDK 获取用户的详细信息, 然后使用 API 调用返回`User`的值创建对象。

现在, 将`constructor` `AuthService`类更改为检查用户是否已登录并加载其详细信息 (如果这样做的话)。 将现有`constructor`替换为以下项。

```TypeScript
constructor(
  private msalService: MsalService,
  private alertsService: AlertsService) {

  this.authenticated = this.msalService.getUser() != null;
  this.getUser().then((user) => {this.user = user});
}
```

最后, 从`HomeComponent`类中删除临时代码。 打开`./src/app/home/home.component.ts`文件, 并将现有`signIn`函数替换为以下项。

```TypeScript
async signIn(): Promise<void> {
  await this.authService.signIn();
}
```

现在, 如果您保存更改并启动应用程序, 登录后应返回到主页, 但 UI 应更改以指示您已登录。

![登录后主页的屏幕截图](./images/add-aad-auth-01.png)

单击右上角的用户头像以访问 "**注销**" 链接。 单击 "**注销**" 重置会话并返回到主页。

![带有 "注销" 链接的下拉菜单的屏幕截图](./images/add-aad-auth-02.png)

## <a name="storing-and-refreshing-tokens"></a>存储和刷新令牌

此时, 您的应用程序具有访问令牌, 该令牌是在 API `Authorization`调用的标头中发送的。 这是允许应用代表用户访问 Microsoft Graph 的令牌。

但是, 此令牌的生存期较短。 令牌在发出后会过期一小时。 由于应用程序使用的是 MSAL 库, 因此您无需实现任何令牌存储或刷新逻辑。 将`MsalService`在浏览器存储中缓存令牌。 该`acquireTokenSilent`方法首先检查缓存的标记, 如果它未过期, 它将返回。 如果它已过期, 则发出无提示请求以获取新的请求。