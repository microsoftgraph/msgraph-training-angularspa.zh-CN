<!-- markdownlint-disable MD002 MD041 -->

在本节中，您将创建一个新的角度项目。

1. 打开命令行界面 (CLI) ，导航到您有权创建文件的目录，然后运行以下命令来安装 " [角度" CLI](https://www.npmjs.com/package/@angular/cli) 工具并创建一个新的角度应用。

    ```Shell
    npm install -g @angular/cli@10.1.7
    ng new graph-tutorial
    ```

1. 角度 CLI 将提示详细信息。 回答如下所示的提示。

    ```Shell
    ? Would you like to add Angular routing? Yes
    ? Which stylesheet format would you like to use? CSS
    ```

1. 命令完成后，转到 `graph-tutorial` CLI 中的目录，并运行以下命令以启动本地 web 服务器。

    ```Shell
    ng serve --open
    ```

1. 默认浏览器将打开， [https://localhost:4200/](https://localhost:4200) 并使用默认的角度页面。 如果你的浏览器未打开，请打开它并浏览以 [https://localhost:4200/](https://localhost:4200) 验证新应用是否正常工作。

## <a name="add-node-packages"></a>添加节点包

在继续操作之前，请先安装将使用的其他一些程序包：

- 用于样式和常用组件的[引导](https://github.com/twbs/bootstrap)。
- 用于从角度使用引导组件的[ng 引导](https://github.com/ng-bootstrap/ng-bootstrap)。
- 日期和时间格式的[时刻](https://github.com/moment/moment)。
- [windows-iana](https://github.com/rubenillodo/windows-iana)
- [msal-](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-angular/README.md) 用于对 Azure Active Directory 进行身份验证和检索访问令牌的角。
- microsoft graph-用于调用 Microsoft Graph 的[客户端](https://github.com/microsoftgraph/msgraph-sdk-javascript)。

1. 在 CLI 中运行以下命令。

    ```Shell
    npm install bootstrap@4.5.3 @ng-bootstrap/ng-bootstrap@7.0.0 msal@1.4.2 @azure/msal-angular@1.1.1
    npm install moment@2.29.1 moment-timezone@0.5.31 windows-iana@4.2.1
    npm install @microsoft/microsoft-graph-client@2.1.0 @microsoft/microsoft-graph-types@1.24.0
    ```

1. 在 CLI 中运行以下命令，以添加 (由 ng-引导) 所需的角度本地化包。

    ```Shell
    ng add @angular/localize
    ```

## <a name="design-the-app"></a>设计应用程序

在本节中，您将为应用程序创建用户界面。

1. 打开 **/src/styles.css** ，并添加以下行。

    :::code language="css" source="../demo/graph-tutorial/src/styles.css":::

1. 将 "启动" 模块添加到应用程序中。 打开 **/src/app/app.module.ts** ，并将其内容替换为以下内容。

    ```typescript
    import { BrowserModule } from '@angular/platform-browser';
    import { FormsModule } from '@angular/forms';
    import { NgModule } from '@angular/core';
    import { NgbModule } from '@ng-bootstrap/ng-bootstrap';

    import { AppRoutingModule } from './app-routing.module';
    import { AppComponent } from './app.component';

    @NgModule({
      declarations: [
        AppComponent
      ],
      imports: [
        BrowserModule,
        FormsModule,
        AppRoutingModule,
        NgbModule
      ],
      providers: [],
      bootstrap: [AppComponent]
    })
    export class AppModule { }
    ```

1. 在 " **/src/app** " 文件夹中创建一个名为 " **user** " 的新文件，并添加以下代码。

    :::code language="typescript" source="../demo/graph-tutorial/src/app/user.ts" id="user":::

1. 为页面上的顶部导航生成一个角度组件。 在 CLI 中，运行以下命令。

    ```Shell
    ng generate component nav-bar
    ```

1. 命令完成后，打开 **/src/app/nav-bar/nav-bar.component.ts** 并将其内容替换为以下内容。

    ```typescript
    import { Component, OnInit } from '@angular/core';

    import { User } from '../user';

    @Component({
      selector: 'app-nav-bar',
      templateUrl: './nav-bar.component.html',
      styleUrls: ['./nav-bar.component.css']
    })
    export class NavBarComponent implements OnInit {

      // Should the collapsed nav show?
      showNav: boolean;
      // Is a user logged in?
      authenticated: boolean;
      // The user
      user: User;

      constructor() { }

      ngOnInit() {
        this.showNav = false;
        this.authenticated = false;
        this.user = null;
      }

      // Used by the Bootstrap navbar-toggler button to hide/show
      // the nav in a collapsed state
      toggleNavBar(): void {
        this.showNav = !this.showNav;
      }

      signIn(): void {
        // Temporary
        this.authenticated = true;
        this.user = {
          displayName: 'Adele Vance',
          email: 'AdeleV@contoso.com',
          avatar: null
        };
      }

      signOut(): void {
        // Temporary
        this.authenticated = false;
        this.user = null;
      }
    }
    ```

1. 打开 **/src/app/nav-bar/nav-bar.component.html** 并将其内容替换为以下内容。

    :::code language="html" source="../demo/graph-tutorial/src/app/nav-bar/nav-bar.component.html" id="navHtml":::

1. 为该应用程序创建一个主页。 在 CLI 中运行以下命令。

    ```Shell
    ng generate component home
    ```

1. 命令完成后，打开 **/src/app/home/home.component.ts** 并将其内容替换为以下内容。

    ```typescript
    import { Component, OnInit } from '@angular/core';

    import { User } from '../user';

    @Component({
      selector: 'app-home',
      templateUrl: './home.component.html',
      styleUrls: ['./home.component.css']
    })
    export class HomeComponent implements OnInit {

      // Is a user logged in?
      authenticated: boolean;
      // The user
      user: any;

      constructor() { }

      ngOnInit() {
        this.authenticated = false;
        this.user = {};
      }

      signIn(): void {
        // Temporary
        this.authenticated = true;
        this.user = {
          displayName: 'Adele Vance',
          email: 'AdeleV@contoso.com'
        };
      }
    }
    ```

1. 打开 **/src/app/home/home.component.html** 并将其内容替换为以下内容。

    :::code language="html" source="../demo/graph-tutorial/src/app/home/home.component.html" id="homeHtml":::

1. 创建一个简单的 `Alert` 类。 在 **/src/app** 目录中创建一个名为 " **alert** " 的新文件，并添加以下代码。

    :::code language="typescript" source="../demo/graph-tutorial/src/app/alert.ts" id="alert":::

1. 创建一个通知服务，应用程序可以使用该服务向用户显示邮件。 在 CLI 中，运行以下命令。

    ```Shell
    ng generate service alerts
    ```

1. 打开 **/src/app/alerts.service.ts** ，并将其内容替换为以下内容。

    :::code language="typescript" source="../demo/graph-tutorial/src/app/alerts.service.ts" id="alertsService":::

1. 生成警报组件以显示警告。 在 CLI 中，运行以下命令。

    ```Shell
    ng generate component alerts
    ```

1. 命令完成后，打开 **/src/app/alerts/alerts.component.ts** 并将其内容替换为以下内容。

    :::code language="typescript" source="../demo/graph-tutorial/src/app/alerts/alerts.component.ts" id="alertComponent":::

1. 打开 **/src/app/alerts/alerts.component.html** 并将其内容替换为以下内容。

    :::code language="html" source="../demo/graph-tutorial/src/app/alerts/alerts.component.html" id="alertHtml":::

1. 打开 **/src/app/app-routing.module.ts** ，并 `const routes: Routes = [];` 将该行替换为以下代码。

    ```typescript
    import { HomeComponent } from './home/home.component';

    const routes: Routes = [
      { path: '', component: HomeComponent },
    ];
    ```

1. 打开 **/src/app/app.component.html** 并将其全部内容替换为以下内容。

    :::code language="html" source="../demo/graph-tutorial/src/app/app.component.html" id="appHtml":::

1. 在 **/src/assets**目录中，添加您选择的命名**no-profile-photo.png**的图像文件。 当用户在 Microsoft Graph 中没有照片时，此图像将用作用户的照片。

保存所有更改并刷新页面。 现在，应用程序看起来应非常不同。

![重新设计的主页的屏幕截图](images/create-app-01.png)
