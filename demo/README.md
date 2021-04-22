# <a name="how-to-run-the-completed-project"></a><span data-ttu-id="8c8bc-101">如何运行已完成的项目</span><span class="sxs-lookup"><span data-stu-id="8c8bc-101">How to run the completed project</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c8bc-102">先决条件</span><span class="sxs-lookup"><span data-stu-id="8c8bc-102">Prerequisites</span></span>

<span data-ttu-id="8c8bc-103">若要在此文件夹中运行已完成的项目，您需要：</span><span class="sxs-lookup"><span data-stu-id="8c8bc-103">To run the completed project in this folder, you need the following:</span></span>

- <span data-ttu-id="8c8bc-104">[Node.js](https://nodejs.org) 安装在开发计算机上。</span><span class="sxs-lookup"><span data-stu-id="8c8bc-104">[Node.js](https://nodejs.org) installed on your development machine.</span></span> <span data-ttu-id="8c8bc-105">如果尚未安装Node.js，请访问上一链接，查看下载选项。</span><span class="sxs-lookup"><span data-stu-id="8c8bc-105">If you do not have Node.js, visit the previous link for download options.</span></span> <span data-ttu-id="8c8bc-106"> (**注意：** 本教程是使用节点版本 14.15.0 编写的。</span><span class="sxs-lookup"><span data-stu-id="8c8bc-106">(**Note:** This tutorial was written with Node version 14.15.0.</span></span> <span data-ttu-id="8c8bc-107">本指南中的步骤可能与其他版本一起运行，但尚未经过测试) </span><span class="sxs-lookup"><span data-stu-id="8c8bc-107">The steps in this guide may work with other versions, but that has not been tested.)</span></span>
- <span data-ttu-id="8c8bc-108">[在开发](https://cli.angular.io/) 计算机上安装 Angular CLI。</span><span class="sxs-lookup"><span data-stu-id="8c8bc-108">[Angular CLI](https://cli.angular.io/) installed on your development machine.</span></span>
- <span data-ttu-id="8c8bc-109">拥有邮箱的个人 Microsoft 帐户 Outlook.com Microsoft 工作或学校帐户。</span><span class="sxs-lookup"><span data-stu-id="8c8bc-109">Either a personal Microsoft account with a mailbox on Outlook.com, or a Microsoft work or school account.</span></span>

<span data-ttu-id="8c8bc-110">如果你没有 Microsoft 帐户，则有几个选项可以获取免费帐户：</span><span class="sxs-lookup"><span data-stu-id="8c8bc-110">If you don't have a Microsoft account, there are a couple of options to get a free account:</span></span>

- <span data-ttu-id="8c8bc-111">你可以 [注册新的个人 Microsoft 帐户](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1)。</span><span class="sxs-lookup"><span data-stu-id="8c8bc-111">You can [sign up for a new personal Microsoft account](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span></span>
- <span data-ttu-id="8c8bc-112">你可以 [注册 Office 365 开发人员计划](https://developer.microsoft.com/office/dev-program) ，获取免费的 Office 365 订阅。</span><span class="sxs-lookup"><span data-stu-id="8c8bc-112">You can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>

## <a name="register-a-web-application-with-the-azure-active-directory-admin-center"></a><span data-ttu-id="8c8bc-113">向 Azure Active Directory 管理中心注册 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="8c8bc-113">Register a web application with the Azure Active Directory admin center</span></span>

1. <span data-ttu-id="8c8bc-114">打开浏览器，并转到 [Azure Active Directory 管理中心](https://aad.portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="8c8bc-114">Open a browser and navigate to the [Azure Active Directory admin center](https://aad.portal.azure.com).</span></span> <span data-ttu-id="8c8bc-115">使用 **个人帐户**（亦称为“Microsoft 帐户”）或 **工作或学校帐户** 登录。</span><span class="sxs-lookup"><span data-stu-id="8c8bc-115">Login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="8c8bc-116">选择左侧导航栏中的“**Azure Active Directory**”，再选择“**管理**”下的“**应用注册**”。</span><span class="sxs-lookup"><span data-stu-id="8c8bc-116">Select **Azure Active Directory** in the left-hand navigation, then select **App registrations** under **Manage**.</span></span>

    ![<span data-ttu-id="8c8bc-117">应用注册屏幕截图</span><span class="sxs-lookup"><span data-stu-id="8c8bc-117">A screenshot of the App registrations</span></span> ](/tutorial/images/aad-portal-app-registrations.png)

1. <span data-ttu-id="8c8bc-118">选择“新注册”。</span><span class="sxs-lookup"><span data-stu-id="8c8bc-118">Select **New registration**.</span></span> <span data-ttu-id="8c8bc-119">在“注册应用”页上，按如下方式设置值。</span><span class="sxs-lookup"><span data-stu-id="8c8bc-119">On the **Register an application** page, set the values as follows.</span></span>

    - <span data-ttu-id="8c8bc-120">将“名称”设置为“`Angular Graph Tutorial`”。</span><span class="sxs-lookup"><span data-stu-id="8c8bc-120">Set **Name** to `Angular Graph Tutorial`.</span></span>
    - <span data-ttu-id="8c8bc-121">将“受支持的帐户类型”设置为“任何组织目录中的帐户和个人 Microsoft 帐户”。</span><span class="sxs-lookup"><span data-stu-id="8c8bc-121">Set **Supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**.</span></span>
    - <span data-ttu-id="8c8bc-122">在“重定向 URI”下，将第一个下拉列表设置为“`Single-page application (SPA)`”，并将值设置为“`http://localhost:4200`”。</span><span class="sxs-lookup"><span data-stu-id="8c8bc-122">Under **Redirect URI**, set the first drop-down to `Single-page application (SPA)` and set the value to `http://localhost:4200`.</span></span>

    ![注册应用程序页面的屏幕截图](/tutorial/images/aad-register-an-app.png)

1. <span data-ttu-id="8c8bc-124">选择 **“注册”**。</span><span class="sxs-lookup"><span data-stu-id="8c8bc-124">Choose **Register**.</span></span> <span data-ttu-id="8c8bc-125">在 **Angular Graph 教程** 页面上，复制应用 (**客户端**) ID 并保存，下一步中将需要此值。</span><span class="sxs-lookup"><span data-stu-id="8c8bc-125">On the **Angular Graph Tutorial** page, copy the value of the **Application (client) ID** and save it, you will need it in the next step.</span></span>

    ![新应用注册的应用程序 ID 的屏幕截图](/tutorial/images/aad-application-id.png)

## <a name="configure-the-sample"></a><span data-ttu-id="8c8bc-127">配置示例</span><span class="sxs-lookup"><span data-stu-id="8c8bc-127">Configure the sample</span></span>

1. <span data-ttu-id="8c8bc-128">将文件 `oauth.ts.example` 重命名为 `oauth.ts` 。</span><span class="sxs-lookup"><span data-stu-id="8c8bc-128">Rename the `oauth.ts.example` file to `oauth.ts`.</span></span>
1. <span data-ttu-id="8c8bc-129">编辑 `oauth.ts` 文件并做出以下更改。</span><span class="sxs-lookup"><span data-stu-id="8c8bc-129">Edit the `oauth.ts` file and make the following changes.</span></span>
    1. <span data-ttu-id="8c8bc-130">将 `YOUR_APP_ID_HERE` 替换为 **从** 应用注册门户获得的应用程序 ID。</span><span class="sxs-lookup"><span data-stu-id="8c8bc-130">Replace `YOUR_APP_ID_HERE` with the **Application Id** you got from the App Registration Portal.</span></span>
1. <span data-ttu-id="8c8bc-131">在命令行界面中 (CLI) ，导航到此目录并运行以下命令以安装要求。</span><span class="sxs-lookup"><span data-stu-id="8c8bc-131">In your command-line interface (CLI), navigate to this directory and run the following command to install requirements.</span></span>

    ```Shell
    npm install
    ```

## <a name="run-the-sample"></a><span data-ttu-id="8c8bc-132">运行示例</span><span class="sxs-lookup"><span data-stu-id="8c8bc-132">Run the sample</span></span>

1. <span data-ttu-id="8c8bc-133">在 CLI 中运行以下命令以启动应用程序。</span><span class="sxs-lookup"><span data-stu-id="8c8bc-133">Run the following command in your CLI to start the application.</span></span>

    ```Shell
    ng serve
    ```

1. <span data-ttu-id="8c8bc-134">打开浏览器，然后转到 `http://localhost:4200`。</span><span class="sxs-lookup"><span data-stu-id="8c8bc-134">Open a browser and browse to `http://localhost:4200`.</span></span>
