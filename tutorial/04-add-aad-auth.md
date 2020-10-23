<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="587a6-101">在本练习中，你将扩展上一练习中的应用程序，以支持 Azure AD 的身份验证。</span><span class="sxs-lookup"><span data-stu-id="587a6-101">In this exercise you will extend the application from the previous exercise to support authentication with Azure AD.</span></span> <span data-ttu-id="587a6-102">若要获取所需的 OAuth 访问令牌以调用 Microsoft Graph，这是必需的。</span><span class="sxs-lookup"><span data-stu-id="587a6-102">This is required to obtain the necessary OAuth access token to call the Microsoft Graph.</span></span> <span data-ttu-id="587a6-103">在此步骤中，将 [Microsoft 身份验证库的角度](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-angular/README.md) 集成到应用程序中。</span><span class="sxs-lookup"><span data-stu-id="587a6-103">In this step you will integrate the [Microsoft Authentication Library for Angular](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-angular/README.md) into the application.</span></span>

1. <span data-ttu-id="587a6-104">在 **/src** 目录中创建一个名为 " **oauth.** " 的新文件，并添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="587a6-104">Create a new file in the **./src** directory named **oauth.ts** and add the following code.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/oauth.example.ts":::

    <span data-ttu-id="587a6-105">将替换 `YOUR_APP_ID_HERE` 为应用程序注册门户中的应用程序 ID。</span><span class="sxs-lookup"><span data-stu-id="587a6-105">Replace `YOUR_APP_ID_HERE` with the application ID from the Application Registration Portal.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="587a6-106">如果您使用的是源代码管理（如 git），现在可以从源代码管理中排除 **oauth** .aspx 文件，以避免无意中泄漏您的应用程序 ID。</span><span class="sxs-lookup"><span data-stu-id="587a6-106">If you're using source control such as git, now would be a good time to exclude the **oauth.ts** file from source control to avoid inadvertently leaking your app ID.</span></span>

1. <span data-ttu-id="587a6-107">打开 **/src/app/app.module.ts** ，并将以下 `import` 语句添加到文件顶部。</span><span class="sxs-lookup"><span data-stu-id="587a6-107">Open **./src/app/app.module.ts** and add the following `import` statements to the top of the file.</span></span>

    ```typescript
    import { MsalModule } from '@azure/msal-angular';
    import { OAuthSettings } from '../oauth';
    ```

1. <span data-ttu-id="587a6-108">将添加 `MsalModule` 到声明中的 `imports` 数组 `@NgModule` ，并使用应用 ID 对它进行初始化。</span><span class="sxs-lookup"><span data-stu-id="587a6-108">Add the `MsalModule` to the `imports` array inside the `@NgModule` declaration, and initialize it with the app ID.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/app/app.module.ts" id="imports" highlight="6-11":::

## <a name="implement-sign-in"></a><span data-ttu-id="587a6-109">实施登录</span><span class="sxs-lookup"><span data-stu-id="587a6-109">Implement sign-in</span></span>

<span data-ttu-id="587a6-110">在本节中，您将创建一个身份验证服务，并实现登录和注销。</span><span class="sxs-lookup"><span data-stu-id="587a6-110">In this section you'll create an authentication service and implement sign-in and sign-out.</span></span>

1. <span data-ttu-id="587a6-111">在 CLI 中运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="587a6-111">Run the following command in your CLI.</span></span>

    ```Shell
    ng generate service auth
    ```

    <span data-ttu-id="587a6-112">通过为此创建服务，可以轻松地将其插入到任何需要访问身份验证方法的组件中。</span><span class="sxs-lookup"><span data-stu-id="587a6-112">By creating a service for this, you can easily inject it into any components that need access to authentication methods.</span></span>

1. <span data-ttu-id="587a6-113">命令完成后，打开 **/src/app/auth.service.ts** 并将其内容替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="587a6-113">Once the command finishes, open **./src/app/auth.service.ts** and replace its contents with the following code.</span></span>

    ```typescript
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
        let result = await this.msalService.loginPopup(OAuthSettings)
          .catch((reason) => {
            this.alertsService.addError('Login failed', JSON.stringify(reason, null, 2));
          });

        if (result) {
          this.authenticated = true;
          // Temporary placeholder
          this.user = new User();
          this.user.displayName = 'Adele Vance';
          this.user.email = 'AdeleV@contoso.com';
          this.user.avatar = '/assets/no-profile-photo.png';
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
        let result = await this.msalService.acquireTokenSilent(OAuthSettings)
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
        return null;
      }
    }
    ```

1. <span data-ttu-id="587a6-114">打开 **/src/app/nav-bar/nav-bar.component.ts** ，并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="587a6-114">Open **./src/app/nav-bar/nav-bar.component.ts** and replace its contents with the following.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/app/nav-bar/nav-bar.component.ts" id="navBarSnippet" highlight="3,15-22,24,26-28,36-38,40-42":::

1. <span data-ttu-id="587a6-115">打开 **/src/app/home/home.component.ts** ，并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="587a6-115">Open **./src/app/home/home.component.ts** and replace its contents with the following.</span></span>

    :::code language="typescript" source="snippets/snippets.ts" id="homeSnippet" highlight="3,12-19,21,23,25-32":::

<span data-ttu-id="587a6-116">保存所做的更改并刷新浏览器。</span><span class="sxs-lookup"><span data-stu-id="587a6-116">Save your changes and refresh the browser.</span></span> <span data-ttu-id="587a6-117">单击 " **单击此处进行登录** " 按钮，您应被重定向到 `https://login.microsoftonline.com` 。</span><span class="sxs-lookup"><span data-stu-id="587a6-117">Click the **Click here to sign in** button and you should be redirected to `https://login.microsoftonline.com`.</span></span> <span data-ttu-id="587a6-118">使用你的 Microsoft 帐户登录，并同意请求的权限。</span><span class="sxs-lookup"><span data-stu-id="587a6-118">Login with your Microsoft account and consent to the requested permissions.</span></span> <span data-ttu-id="587a6-119">应用程序页面应刷新，并显示令牌。</span><span class="sxs-lookup"><span data-stu-id="587a6-119">The app page should refresh, showing the token.</span></span>

### <a name="get-user-details"></a><span data-ttu-id="587a6-120">获取用户详细信息</span><span class="sxs-lookup"><span data-stu-id="587a6-120">Get user details</span></span>

<span data-ttu-id="587a6-121">现在，身份验证服务为用户的显示名称和电子邮件地址设置常量值。</span><span class="sxs-lookup"><span data-stu-id="587a6-121">Right now the authentication service sets constant values for the user's display name and email address.</span></span> <span data-ttu-id="587a6-122">现在，你已拥有访问令牌，可以从 Microsoft Graph 获取用户详细信息，以便这些值与当前用户相对应。</span><span class="sxs-lookup"><span data-stu-id="587a6-122">Now that you have an access token, you can get user details from Microsoft Graph so those values correspond to the current user.</span></span>

1. <span data-ttu-id="587a6-123">打开 **/src/app/auth.service.ts** ，并将以下 `import` 语句添加到文件顶部。</span><span class="sxs-lookup"><span data-stu-id="587a6-123">Open **./src/app/auth.service.ts** and add the following `import` statements to the top of the file.</span></span>

    ```typescript
    import { Client } from '@microsoft/microsoft-graph-client';
    import * as MicrosoftGraph from '@microsoft/microsoft-graph-types';
    ```

1. <span data-ttu-id="587a6-124">将新函数添加到称为 `AuthService` 的 `getUser` 类。</span><span class="sxs-lookup"><span data-stu-id="587a6-124">Add a new function to the `AuthService` class called `getUser`.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/app/auth.service.ts" id="getUserSnippet":::

1. <span data-ttu-id="587a6-125">在 `getAccessToken` 添加通知以显示访问令牌的方法中找到并删除以下代码。</span><span class="sxs-lookup"><span data-stu-id="587a6-125">Locate and remove the following code in the `getAccessToken` method that adds an alert to display the access token.</span></span>

    ```typescript
    // Temporary to display token in an error box
    this.alertsService.addSuccess('Token acquired', result);
    ```

1. <span data-ttu-id="587a6-126">从方法中找到并删除以下代码 `signIn` 。</span><span class="sxs-lookup"><span data-stu-id="587a6-126">Locate and remove the following code from the `signIn` method.</span></span>

    ```typescript
    // Temporary placeholder
    this.user = new User();
    this.user.displayName = "Adele Vance";
    this.user.email = "AdeleV@contoso.com";
    this.user.avatar = '/assets/no-profile-photo.png';
    ```

1. <span data-ttu-id="587a6-127">在其位置添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="587a6-127">In its place, add the following code.</span></span>

    ```typescript
    this.user = await this.getUser();
    ```

    <span data-ttu-id="587a6-128">此新代码使用 Microsoft Graph SDK 获取用户的详细信息，然后 `User` 使用 API 调用返回的值创建对象。</span><span class="sxs-lookup"><span data-stu-id="587a6-128">This new code uses the Microsoft Graph SDK to get the user's details, then creates a `User` object using values returned by the API call.</span></span>

1. <span data-ttu-id="587a6-129">更改 `constructor` 类的， `AuthService` 以检查用户是否已登录并加载其详细信息（如果这样做的话）。</span><span class="sxs-lookup"><span data-stu-id="587a6-129">Change the `constructor` for the `AuthService` class to check if the user is already logged in and load their details if so.</span></span> <span data-ttu-id="587a6-130">将现有替换 `constructor` 为以下项。</span><span class="sxs-lookup"><span data-stu-id="587a6-130">Replace the existing `constructor` with the following.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/app/auth.service.ts" id="constructorSnippet" highlight="5-6":::

1. <span data-ttu-id="587a6-131">从类中删除临时代码 `HomeComponent` 。</span><span class="sxs-lookup"><span data-stu-id="587a6-131">Remove the temporary code from the `HomeComponent` class.</span></span> <span data-ttu-id="587a6-132">打开 **/src/app/home/home.component.ts** ，并将现有 `signIn` 函数替换为以下项。</span><span class="sxs-lookup"><span data-stu-id="587a6-132">Open **./src/app/home/home.component.ts** and replace the existing `signIn` function with the following.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/app/home/home.component.ts" id="signInSnippet":::

<span data-ttu-id="587a6-133">现在，如果您保存更改并启动应用程序，登录后应返回到主页，但 UI 应更改以指示您已登录。</span><span class="sxs-lookup"><span data-stu-id="587a6-133">Now if you save your changes and start the app, after sign-in you should end up back on the home page, but the UI should change to indicate that you are signed-in.</span></span>

![登录后主页的屏幕截图](./images/add-aad-auth-01.png)

<span data-ttu-id="587a6-135">单击右上角的用户头像以访问 " **注销** " 链接。</span><span class="sxs-lookup"><span data-stu-id="587a6-135">Click the user avatar in the top right corner to access the **Sign Out** link.</span></span> <span data-ttu-id="587a6-136">单击 " **注销** " 重置会话并返回到主页。</span><span class="sxs-lookup"><span data-stu-id="587a6-136">Clicking **Sign Out** resets the session and returns you to the home page.</span></span>

![带有 "注销" 链接的下拉菜单的屏幕截图](./images/add-aad-auth-02.png)

## <a name="storing-and-refreshing-tokens"></a><span data-ttu-id="587a6-138">存储和刷新令牌</span><span class="sxs-lookup"><span data-stu-id="587a6-138">Storing and refreshing tokens</span></span>

<span data-ttu-id="587a6-139">此时，您的应用程序具有访问令牌，该令牌是在 `Authorization` API 调用的标头中发送的。</span><span class="sxs-lookup"><span data-stu-id="587a6-139">At this point your application has an access token, which is sent in the `Authorization` header of API calls.</span></span> <span data-ttu-id="587a6-140">这是允许应用代表用户访问 Microsoft Graph 的令牌。</span><span class="sxs-lookup"><span data-stu-id="587a6-140">This is the token that allows the app to access the Microsoft Graph on the user's behalf.</span></span>

<span data-ttu-id="587a6-141">但是，此令牌的生存期较短。</span><span class="sxs-lookup"><span data-stu-id="587a6-141">However, this token is short-lived.</span></span> <span data-ttu-id="587a6-142">令牌在发出后会过期一小时。</span><span class="sxs-lookup"><span data-stu-id="587a6-142">The token expires an hour after it is issued.</span></span> <span data-ttu-id="587a6-143">由于应用程序使用的是 MSAL 库，因此您无需实现任何令牌存储或刷新逻辑。</span><span class="sxs-lookup"><span data-stu-id="587a6-143">Because the app is using the MSAL library, you do not have to implement any token storage or refresh logic.</span></span> <span data-ttu-id="587a6-144">将在 `MsalService` 浏览器存储中缓存令牌。</span><span class="sxs-lookup"><span data-stu-id="587a6-144">The `MsalService` caches the token in the browser storage.</span></span> <span data-ttu-id="587a6-145">该 `acquireTokenSilent` 方法首先检查缓存的标记，如果它未过期，它将返回。</span><span class="sxs-lookup"><span data-stu-id="587a6-145">The `acquireTokenSilent` method first checks the cached token, and if it is not expired, it returns it.</span></span> <span data-ttu-id="587a6-146">如果它已过期，则发出无提示请求以获取新的请求。</span><span class="sxs-lookup"><span data-stu-id="587a6-146">If it is expired, it makes a silent request to obtain a new one.</span></span>
