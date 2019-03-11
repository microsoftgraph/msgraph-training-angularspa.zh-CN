<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="5d7b0-101">在本练习中, 将使用应用程序注册表门户 (ARP) 创建新的 Azure AD web 应用程序注册。</span><span class="sxs-lookup"><span data-stu-id="5d7b0-101">In this exercise, you will create a new Azure AD web application registration using the Application Registry Portal (ARP).</span></span>

1. <span data-ttu-id="5d7b0-102">打开浏览器并导航到[应用程序注册门户](https://apps.dev.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="5d7b0-102">Open a browser and navigate to the [Application Registration Portal](https://apps.dev.microsoft.com).</span></span> <span data-ttu-id="5d7b0-103">使用**个人帐户**(亦称: Microsoft 帐户) 或**工作或学校帐户**登录。</span><span class="sxs-lookup"><span data-stu-id="5d7b0-103">Login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="5d7b0-104">选择页面顶部的 "**添加应用**"。</span><span class="sxs-lookup"><span data-stu-id="5d7b0-104">Select **Add an app** at the top of the page.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5d7b0-105">如果在页面上看到多个 "**添加应用程序**" 按钮, 请选择与 "**聚合应用程序**" 列表对应的项。</span><span class="sxs-lookup"><span data-stu-id="5d7b0-105">If you see more than one **Add an app** button on the page, select the one that corresponds to the **Converged apps** list.</span></span>

1. <span data-ttu-id="5d7b0-106">在 "**注册应用程序**" 页上, 将**应用程序名称**设置为 "**角度图" 教程**, 然后选择 "**创建**"。</span><span class="sxs-lookup"><span data-stu-id="5d7b0-106">On the **Register your application** page, set the **Application Name** to **Angular Graph Tutorial** and select **Create**.</span></span>

    ![在应用注册门户网站中创建新应用程序的屏幕截图](./images/arp-create-app-01.png)

1. <span data-ttu-id="5d7b0-108">在 "**角度图教程注册**" 页上的 "**属性**" 部分下, 复制**应用程序 Id** , 因为稍后将需要它。</span><span class="sxs-lookup"><span data-stu-id="5d7b0-108">On the **Angular Graph Tutorial Registration** page, under the **Properties** section, copy the **Application Id** as you will need it later.</span></span>

    ![新创建的应用程序 ID 的屏幕截图](./images/arp-create-app-02.png)

1. <span data-ttu-id="5d7b0-110">向下滚动到 "**平台**" 部分。</span><span class="sxs-lookup"><span data-stu-id="5d7b0-110">Scroll down to the **Platforms** section.</span></span>

    1. <span data-ttu-id="5d7b0-111">选择 "**添加平台**"。</span><span class="sxs-lookup"><span data-stu-id="5d7b0-111">Select **Add Platform**.</span></span>
    1. <span data-ttu-id="5d7b0-112">在 "**添加平台**" 对话框中, 选择 " **Web**"。</span><span class="sxs-lookup"><span data-stu-id="5d7b0-112">In the **Add Platform** dialog, select **Web**.</span></span>

        ![为应用程序创建平台的屏幕截图](./images/arp-create-app-03.png)

    1. <span data-ttu-id="5d7b0-114">在 " **Web**平台" 框中`http://localhost:4200` , 输入**重定向 url**。</span><span class="sxs-lookup"><span data-stu-id="5d7b0-114">In the **Web** platform box, enter `http://localhost:4200` for the **Redirect URLs**.</span></span>

        ![应用程序新添加的 Web 平台的屏幕截图](./images/arp-create-app-04.png)

1. <span data-ttu-id="5d7b0-116">滚动到页面底部, 然后选择 "**保存**"。</span><span class="sxs-lookup"><span data-stu-id="5d7b0-116">Scroll to the bottom of the page and select **Save**.</span></span>