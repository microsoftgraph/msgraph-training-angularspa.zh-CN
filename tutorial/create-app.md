<!-- markdownlint-disable MD002 MD041 -->

打开命令行接口 (CLI), 导航到您有权在其中创建文件的目录, 并运行以下命令来安装 "[角度" CLI](https://www.npmjs.com/package/@angular/cli)工具并创建一个新的角度应用。

```Shell
npm install -g @angular/cli
ng new graph-tutorial
```

角度 CLI 将提示详细信息。 回答如下所示的提示。

```Shell
? Would you like to add Angular routing? Yes
? Which stylesheet format would you like to use? CSS
```

命令完成后, 转到 CLI 中`graph-tutorial`的目录, 并运行以下命令以启动本地 web 服务器。

```Shell
ng serve --open
```

默认浏览器将打开[https://localhost:4200/](https://localhost:4200) , 并使用默认的角度页面。 如果你的浏览器未打开, 请打开它[https://localhost:4200/](https://localhost:4200)并浏览以验证新应用是否正常工作。

在继续操作之前, 请先安装将使用的其他一些程序包:

- 用于样式和常用组件的[引导](https://github.com/twbs/bootstrap)。
- 用于从角度使用引导组件的[ng 引导](https://github.com/ng-bootstrap/ng-bootstrap)。
- [fontawesome](https://github.com/FortAwesome/angular-fontawesome) , 以在角中使用 fontawesome 图标。
- [fontawesome-svg-core](https://github.com/FortAwesome/Font-Awesome)、 [free-regular-图标](https://github.com/FortAwesome/Font-Awesome), 以及示例中使用的 fontawesome 图标的[自由纯色 svg-图标](https://github.com/FortAwesome/Font-Awesome)。
- 日期和时间格式的[时刻](https://github.com/moment/moment)。
- [msal-](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-angular/README.md)用于对 Azure Active Directory 进行身份验证和检索访问令牌的角。
- [rxjs-兼容](https://github.com/ReactiveX/rxjs/tree/master/compat)性, `msal-angular`包所需。
- microsoft graph-用于调用 microsoft graph 的[客户端](https://github.com/microsoftgraph/msgraph-sdk-javascript)。

在 CLI 中运行以下命令。

```Shell
npm install bootstrap@4.3.1 @fortawesome/angular-fontawesome@0.3.0 @fortawesome/fontawesome-svg-core@1.2.15
npm install @fortawesome/free-regular-svg-icons@5.7.2 @fortawesome/free-solid-svg-icons@5.7.2
npm install moment@2.24.0 moment-timezone@0.5.23 @ng-bootstrap/ng-bootstrap@4.1.0
npm install @azure/msal-angular@0.1.2 rxjs-compat@6.4.0 @microsoft/microsoft-graph-client@1.4.0
```

## <a name="design-the-app"></a>设计应用程序

首先将引导数据库的 CSS 文件添加到应用程序, 并添加一些全局样式。 打开`./src/styles.css` , 并添加以下行。

```CSS
@import "~bootstrap/dist/css/bootstrap.css";

/* Add padding for the nav bar */
body {
  padding-top: 4.5rem;
}

/* Style debug info in alerts */
.alert-pre {
  word-wrap: break-word;
  word-break: break-all;
  white-space: pre-wrap;
}
```

接下来, 将 "引导" 和 "FontAwesome" 模块添加到应用程序中。 打开`./src/app/app.module.ts`并将以下`import`语句添加到文件顶部。

```TypeScript
import { NgbModule } from '@ng-bootstrap/ng-bootstrap';
import { FontAwesomeModule } from '@fortawesome/angular-fontawesome';
import { library } from '@fortawesome/fontawesome-svg-core';
import { faExternalLinkAlt } from '@fortawesome/free-solid-svg-icons';
import { faUserCircle } from '@fortawesome/free-regular-svg-icons';
```

然后, 在所有`import`语句后面添加以下代码。

```TypeScript
library.add(faExternalLinkAlt);
library.add(faUserCircle);
```

在`@NgModule`声明中, 将现有`imports`数组替换为以下项。

```TypeScript
imports: [
  BrowserModule,
  AppRoutingModule,
  NgbModule,
  FontAwesomeModule
]
```

现在, 为页面上的顶部导航生成一个角度组件。 在 CLI 中, 运行以下命令。

```Shell
ng generate component nav-bar
```

命令完成后, 打开`./src/app/nav-bar/nav-bar.component.ts`文件并将其内容替换为以下内容。

```TypeScript
import { Component, OnInit } from '@angular/core';

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
  user: any;

  constructor() { }

  ngOnInit() {
    this.showNav = false;
    this.authenticated = false;
    this.user = {};
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
      email: 'AdeleV@contoso.com'
    };
  }

  signOut(): void {
    // Temporary
    this.authenticated = false;
    this.user = {};
  }
}
```

打开`./src/app/nav-bar/nav-bar.component.html`文件, 并将其内容替换为以下内容。

```html
<nav class="navbar navbar-expand-md navbar-dark fixed-top bg-dark">
  <div class="container">
    <a routerLink="/" class="navbar-brand">Angular Graph Tutorial</a>
    <button class="navbar-toggler" type="button" (click)="toggleNavBar()" [attr.aria-expanded]="showNav"
    aria-controls="navbarCollapse" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" [class.show]="showNav" id="navbarCollapse">
      <ul class="navbar-nav mr-auto">
        <li class="nav-item">
          <a routerLink="/" class="nav-link" routerLinkActive="active">Home</a>
        </li>
        <li *ngIf="authenticated" class="nav-item">
          <a routerLink="/calendar" class="nav-link" routerLinkActive="active">Calendar</a>
        </li>
      </ul>
      <ul class="navbar-nav justify-content-end">
        <li class="nav-item">
          <a class="nav-link" href="https://docs.microsoft.com/graph/overview" target="_blank">
            <fa-icon [icon]="[ 'fas', 'external-link-alt' ]" class="mr-1"></fa-icon>Docs
          </a>
        </li>
        <li *ngIf="authenticated" ngbDropdown placement="bottom-right" class="nav-item">
          <a ngbDropdownToggle id="userMenu" class="nav-link" href="javascript:undefined" role="button" aria-haspopup="true"
            aria-expanded="false">
            <div *ngIf="user.avatar; then userAvatar else defaultAvatar"></div>
            <ng-template #userAvatar>
              <img src="user.avatar" class="rounded-circle align-self-center mr-2" style="width: 32px;">
            </ng-template>
            <ng-template #defaultAvatar>
              <fa-icon [icon]="[ 'far', 'user-circle' ]" fixedWidth="true" size="lg"
                class="rounded-circle align-self-center mr-2"></fa-icon>
            </ng-template>
          </a>
          <div ngbDropdownMenu aria-labelledby="userMenu">
            <h5 class="dropdown-item-text mb-0">{{user.displayName}}</h5>
            <p class="dropdown-item-text text-muted mb-0">{{user.email}}</p>
            <div class="dropdown-divider"></div>
            <a class="dropdown-item" href="javascript:undefined" role="button" (click)="signOut()">Sign Out</a>
          </div>
        </li>
        <li *ngIf="!authenticated" class="nav-item">
          <a class="nav-link" href="javascript:undefined" role="button" (click)="signIn()">Sign In</a>
        </li>
      </ul>
    </div>
  </div>
</nav>
```

接下来, 为该应用程序创建一个主页。 在 CLI 中运行以下命令。

```Shell
ng generate component home
```

命令完成后, 打开`./src/app/home/home.component.ts`文件并将其内容替换为以下内容。

```TypeScript
import { Component, OnInit } from '@angular/core';

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

然后, 打开`./src/app/home/home.component.html`文件并将其内容替换为以下内容。

```html
<div class="jumbotron">
  <h1>Angular Graph Tutorial</h1>
  <p class="lead">This sample app shows how to use the Microsoft Graph API from Angular</p>
  <div *ngIf="authenticated; then welcomeUser else signInPrompt"></div>
  <ng-template #welcomeUser>
    <h4>Welcome {{ user.displayName }}!</h4>
    <p>Use the navigation bar at the top of the page to get started.</p>
  </ng-template>
  <ng-template #signInPrompt>
    <a href="javascript:undefined" class="btn btn-primary btn-large" role="button" (click)="signIn()">Click here to sign in</a>
  </ng-template>
</div>
```

现在, 创建一个通知服务, 应用程序可以使用该服务向用户显示邮件。 首先创建一个简单`Alert`的类。 在名为`./src/app` `alert.ts`的目录中创建一个新文件, 并添加以下代码。

```TypeScript
export class Alert {
  message: string;
  debug: string;
}
```

在 CLI 中, 运行以下命令。

```Shell
ng generate service alerts
```

打开`./src/app/alerts.service.ts`文件, 并将其内容替换为以下内容。

```TypeScript
import { Injectable } from '@angular/core';
import { Alert } from './alert';

@Injectable({
  providedIn: 'root'
})
export class AlertsService {

  alerts: Alert[] = [];

  add(message: string, debug: string) {
    this.alerts.push({message: message, debug: debug});
  }

  remove(alert: Alert) {
    this.alerts.splice(this.alerts.indexOf(alert), 1);
  }
}
```

现在生成一个警报组件以显示警报。 在 CLI 中, 运行以下命令。

```Shell
ng generate component alerts
```

命令完成后, 打开`./src/app/alerts/alerts.component.ts`文件并将其内容替换为以下内容。

```TypeScript
import { Component, OnInit } from '@angular/core';
import { AlertsService } from '../alerts.service';
import { Alert } from '../alert';

@Component({
  selector: 'app-alerts',
  templateUrl: './alerts.component.html',
  styleUrls: ['./alerts.component.css']
})
export class AlertsComponent implements OnInit {

  constructor(private alertsService: AlertsService) { }

  ngOnInit() {
  }

  close(alert: Alert) {
    this.alertsService.remove(alert);
  }
}
```

然后, 打开`./src/app/alerts/alerts.component.html`文件并将其内容替换为以下内容。

```html
<div *ngFor="let alert of alertsService.alerts">
  <ngb-alert type="danger" (close)="close(alert)">
    <p>{{alert.message}}</p>
    <pre *ngIf="alert.debug" class="alert-pre border bg-light p-2"><code>{{alert.debug}}</code></pre>
  </ngb-alert>
</div>
```

现在, 定义了这些基本组件, 更新应用程序以使用它们。 首先, 打开`./src/app/app-routing.module.ts`文件并将`const routes: Routes = [];`该行替换为以下代码。

```TypeScript
import { HomeComponent } from './home/home.component';

const routes: Routes = [
  { path: '', component: HomeComponent },
];
```

打开 `./src/app/app.component.html` 文件，并将其全部内容替换为以下内容。

```html
<app-nav-bar></app-nav-bar>
<main role="main" class="container">
  <app-alerts></app-alerts>
  <router-outlet></router-outlet>
</main>
```

保存所有更改并刷新页面。 现在, 应用程序看起来应非常不同。

![重新设计的主页的屏幕截图](images/create-app-01.png)