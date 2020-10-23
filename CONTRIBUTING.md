# <a name="contributing-to-microsoft-graph-training-repositories"></a>对 Microsoft Graph 培训存储库的贡献

感谢你参与此项目！ 在提交拉取请求之前，请务必考虑以下事项。

## <a name="overview"></a>概述

此存储库中的代码具有三个用途：

- [教程](/tutorial)文件夹中的 Markdown 文件发布为[Microsoft Graph 教程](https://docs.microsoft.com/graph/tutorials)页面上的教程。
- [演示](/demo)文件夹中的示例项目是[Microsoft Graph 快速入门](https://developer.microsoft.com/graph/quick-start)的来源。 * *\** _
- 演示文件夹中的示例项目也是直接从 GitHub 下载的，并且应在某个简单配置之后运行，如下所示。

> _*\**_ 并不是所有的培训存储库都可在) 中快速启动 (。

这一点很重要，因为一个位置中的更改 _may * 需要在另一个位置进行更改，以使内容保持同步。Whereever 可以使用自定义语法) 直接 (Markdown 文件引用源代码文件 `:::code` ，以便更新源中的代码将自动更新 Markdown 中的代码。

## <a name="updating-code"></a>更新代码

`:::code`Markdown 中使用的语法取决于源代码文件中的特定注释。 这些注释的外观如下所示：

```csharp
// <MySnippet>
Console.WriteLine("Hello World!");
// </MySnippet>
```

如果在这些 "标记" 注释之间更新代码，则 Markdown 文件将在发布到 Microsoft Graph 文档网站时自动获取这些更改。 如果您在这些注释之外更新代码，则很可能需要更新相应的 Markdown。

## <a name="adding-features"></a>添加功能

在热情时，请不要发送请求将新功能添加到示例中。 由于此存储库主要是 "构建您的第一个应用程序" 教程，因此功能集受设计限制。

## <a name="submitting-pull-requests"></a>提交拉取请求

请将所有拉取请求提交到 `main` 分支。

## <a name="when-do-changes-get-published"></a>何时发布更改？

发布 [Microsoft Graph 教程](https://docs.microsoft.com/graph/tutorials) 网站的更新不是自动的。 必须首先将更改升级到 `live` 分支，然后网站管理员必须触发生成。 这通常在 "需要" 的基础上完成。

## <a name="code-of-conduct"></a>行为准则

此项目采用 [Microsoft 开源行为准则](https://opensource.microsoft.com/codeofconduct/)。有关详细信息，请参阅 [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/)（行为准则常见问题解答），有任何其他问题或意见，也可联系 [opencode@microsoft.com](mailto:opencode@microsoft.com)。
