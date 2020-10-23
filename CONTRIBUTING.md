# <a name="contributing-to-microsoft-graph-training-repositories"></a><span data-ttu-id="6d931-101">对 Microsoft Graph 培训存储库的贡献</span><span class="sxs-lookup"><span data-stu-id="6d931-101">Contributing to Microsoft Graph training repositories</span></span>

<span data-ttu-id="6d931-102">感谢你参与此项目！</span><span class="sxs-lookup"><span data-stu-id="6d931-102">Thank you for contributing to this project!</span></span> <span data-ttu-id="6d931-103">在提交拉取请求之前，请务必考虑以下事项。</span><span class="sxs-lookup"><span data-stu-id="6d931-103">Before submitting your pull request, be sure to consider the following.</span></span>

## <a name="overview"></a><span data-ttu-id="6d931-104">概述</span><span class="sxs-lookup"><span data-stu-id="6d931-104">Overview</span></span>

<span data-ttu-id="6d931-105">此存储库中的代码具有三个用途：</span><span class="sxs-lookup"><span data-stu-id="6d931-105">The code in this repository serves three purposes:</span></span>

- <span data-ttu-id="6d931-106">[教程](/tutorial)文件夹中的 Markdown 文件发布为[Microsoft Graph 教程](https://docs.microsoft.com/graph/tutorials)页面上的教程。</span><span class="sxs-lookup"><span data-stu-id="6d931-106">The Markdown files in the [tutorial](/tutorial) folder are published as a tutorial on the [Microsoft Graph tutorials](https://docs.microsoft.com/graph/tutorials) page.</span></span>
- <span data-ttu-id="6d931-107">[演示](/demo)文件夹中的示例项目是[Microsoft Graph 快速入门](https://developer.microsoft.com/graph/quick-start)的来源。 \* *\** _</span><span class="sxs-lookup"><span data-stu-id="6d931-107">The sample project in the [demo](/demo) folder is the source for a [Microsoft Graph quick start](https://developer.microsoft.com/graph/quick-start).\**\**_</span></span>
- <span data-ttu-id="6d931-108">演示文件夹中的示例项目也是直接从 GitHub 下载的，并且应在某个简单配置之后运行，如下所示。</span><span class="sxs-lookup"><span data-stu-id="6d931-108">The sample project in the demo folder is also downloadable directly from GitHub and should run as-is after some simple configuration.</span></span>

> <span data-ttu-id="6d931-109">_*\**_ 并不是所有的培训存储库都可在) 中快速启动 (。</span><span class="sxs-lookup"><span data-stu-id="6d931-109">_*\**_ Not all training repositories are available as quick starts (yet).</span></span>

<span data-ttu-id="6d931-110">这一点很重要，因为一个位置中的更改 _may \* 需要在另一个位置进行更改，以使内容保持同步。Whereever 可以使用自定义语法) 直接 (Markdown 文件引用源代码文件 `:::code` ，以便更新源中的代码将自动更新 Markdown 中的代码。</span><span class="sxs-lookup"><span data-stu-id="6d931-110">This is important to keep in mind, because changes in one place _may\* require changes in another, to keep things in sync. Whereever possible, the Markdown files refer to the source code files directly (using a custom `:::code` syntax), so that updating code in source will automatically update the code in Markdown.</span></span>

## <a name="updating-code"></a><span data-ttu-id="6d931-111">更新代码</span><span class="sxs-lookup"><span data-stu-id="6d931-111">Updating code</span></span>

<span data-ttu-id="6d931-112">`:::code`Markdown 中使用的语法取决于源代码文件中的特定注释。</span><span class="sxs-lookup"><span data-stu-id="6d931-112">The `:::code` syntax used in Markdown depends on specific comments in the source code file.</span></span> <span data-ttu-id="6d931-113">这些注释的外观如下所示：</span><span class="sxs-lookup"><span data-stu-id="6d931-113">These comments look like the following:</span></span>

```csharp
// <MySnippet>
Console.WriteLine("Hello World!");
// </MySnippet>
```

<span data-ttu-id="6d931-114">如果在这些 "标记" 注释之间更新代码，则 Markdown 文件将在发布到 Microsoft Graph 文档网站时自动获取这些更改。</span><span class="sxs-lookup"><span data-stu-id="6d931-114">If you update code between these "marker" comments, the Markdown files will automatically get those changes when published to the Microsoft Graph documentation site.</span></span> <span data-ttu-id="6d931-115">如果您在这些注释之外更新代码，则很可能需要更新相应的 Markdown。</span><span class="sxs-lookup"><span data-stu-id="6d931-115">If you update code outside of those comments, it's very likely that you'll need to update the corresponding Markdown.</span></span>

## <a name="adding-features"></a><span data-ttu-id="6d931-116">添加功能</span><span class="sxs-lookup"><span data-stu-id="6d931-116">Adding features</span></span>

<span data-ttu-id="6d931-117">在热情时，请不要发送请求将新功能添加到示例中。</span><span class="sxs-lookup"><span data-stu-id="6d931-117">While the enthusiasm is appreciated, please don't send pull requests to add new features to the sample.</span></span> <span data-ttu-id="6d931-118">由于此存储库主要是 "构建您的第一个应用程序" 教程，因此功能集受设计限制。</span><span class="sxs-lookup"><span data-stu-id="6d931-118">Because this repository is primarily a "build your first app" tutorial, the feature set is limited, by design.</span></span>

## <a name="submitting-pull-requests"></a><span data-ttu-id="6d931-119">提交拉取请求</span><span class="sxs-lookup"><span data-stu-id="6d931-119">Submitting pull requests</span></span>

<span data-ttu-id="6d931-120">请将所有拉取请求提交到 `main` 分支。</span><span class="sxs-lookup"><span data-stu-id="6d931-120">Please submit all pull requests to the `main` branch.</span></span>

## <a name="when-do-changes-get-published"></a><span data-ttu-id="6d931-121">何时发布更改？</span><span class="sxs-lookup"><span data-stu-id="6d931-121">When do changes get published?</span></span>

<span data-ttu-id="6d931-122">发布 [Microsoft Graph 教程](https://docs.microsoft.com/graph/tutorials) 网站的更新不是自动的。</span><span class="sxs-lookup"><span data-stu-id="6d931-122">Publishing of updates to the [Microsoft Graph tutorials](https://docs.microsoft.com/graph/tutorials) site is not automatic.</span></span> <span data-ttu-id="6d931-123">必须首先将更改升级到 `live` 分支，然后网站管理员必须触发生成。</span><span class="sxs-lookup"><span data-stu-id="6d931-123">Changes must first be promoted to the `live` branch, then a build must be triggered by the site admins.</span></span> <span data-ttu-id="6d931-124">这通常在 "需要" 的基础上完成。</span><span class="sxs-lookup"><span data-stu-id="6d931-124">This is typically done on an "as-needed" basis.</span></span>

## <a name="code-of-conduct"></a><span data-ttu-id="6d931-125">行为准则</span><span class="sxs-lookup"><span data-stu-id="6d931-125">Code of conduct</span></span>

<span data-ttu-id="6d931-p106">此项目采用 [Microsoft 开源行为准则](https://opensource.microsoft.com/codeofconduct/)。有关详细信息，请参阅 [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/)（行为准则常见问题解答），有任何其他问题或意见，也可联系 [opencode@microsoft.com](mailto:opencode@microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="6d931-p106">This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/). For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.</span></span>
