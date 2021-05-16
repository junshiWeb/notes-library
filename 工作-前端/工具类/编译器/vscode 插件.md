## 基础通用插件

### Chinese

`vscode`编辑器汉化包，安装后，在 `locale.json` 中添加 `"locale": "zh-cn"`，即可载入中文（简体）语言包。

### Auto Rename Tag

自动重命名成对的`HTML`标记，修改开始标签，结束标签会同步修改

### HTML Snippets 

HTML代码片段，该插件可为你提供html标签的代码提示，不用键入尖括号了

### Bracket Pair Colorizer

该插件可以为你把成对的括号做颜色区分，并且提供一根连接线。方便我们审阅代码结构

通过修改配置文件，使得结构线高亮，食用更佳

```
"workbench.colorCustomizations": {
  "editorIndentGuide.activeBackground": "#00ffea"
},
```

### CSS Peek

css样式查看器，可快速查看我们的css样式，非常方便快捷

### Npm Intellisense

可自动完成导入语句中的npm模块

### vscode-icons

提供了非常漂亮的目录树图标主题

### Auto Close Tag

自动闭合`HTML/XML`标签

### Path Intellisense

自动提示文件路径，支持各种快速引入文件

### Beautify

在代码文件右键鼠标一键格式化 `html,js,css`

### JavaScript (ES6) code snippets

ES6语法智能提示，以及快速输入

### Vetur

`VScode`官方钦定Vue插件，`Vue`开发者必备。内含语法高亮，智能提示，`emmet`，错误提示，格式化，自动补全，`debugger`等实用功能

## 代码风格规范类插件

### ESlint

规范js代码书写规则，如果觉得太过严谨，可自定义规则

### Code Spell Checker

是拼写检查程序，检查不常见的单词，如果单词拼写错误，会给出警告提示

### koroFileHeader

在`vscode`中用于生成文件头部注释和函数注释的插件，经过多版迭代后，插件：支持所有主流语言,功能强大，灵活方便，文档齐全，食用简单！

不光如此，还能生成一些特别有意思的注释，比如这一条喷火龙...

![img](${img}/2a71eec8f7134c6c8cf053a08a47b6f2_tplv-k3u1fbpfcp-watermark.image)

### Better Align

代码书写的整洁，工整往往是衡量一个程序员素养的标准，这款插件可以让你的代码更排版优雅

选中代码配合组合键`[Ctrl+Shift+p]`，输入`Align`即可

### change-case

通常我们对一个变量的命名可能是驼峰，可能是全大写，又或是下划线，这里可通过这个插件解决变量命名规范的问题

选中变量配合组合键`[Ctrl+Shift+p]`，输入对应格式即可

### ter Comments

这款插件可以丰富注释颜色，让注释也具有生命力，如需自定义样式，需要写入配置代码

```js
配置代码
"better-comments.tags": [
  {
    "tag": "*",
    "color": "#98C379",
    "strikethrough": false,
    "backgroundColor": "transparent"
  }
]
使用
// * 绿色的高亮注释

```

### TODO Tree

我们经常会在代码中使用`TODO`来标记我们的代码，提高可读性，`TODO Tree`这款插件提供了可视化窗口来查看和管理我们的`TODO Tree`

### GitLens

`GitLens`可以帮助您更好地理解代码。快速查看更改行或代码块的对象，功能强大，功能丰富且高度可定制，可以满足您的需求

### GitHistory

`GitHistory`可查看和搜索git日志以及图形和详细信息，同时还支持分支比较，分支管理等操作，非常方便

### Partial Diff

文件比较是一个很常见的场景，如果光凭我们肉眼分别的话，累人不说还容易出错。` Partial Diff`的出现就正好解决了这个问题

### Markdown All in One

这款神器可以让我们在`vscode`里面快乐的书写`Markdown`，功能强大。提供了丰富的快捷键，可边写边看，轻松转化为`html`或`pdf`文件，十分好用，强烈推荐

### vscode-drawio

这款神器可以让我们在`vscode`里面快乐的画流程图。新建 `.drawio` 后缀文件并拖入vscode中, 即可得到如下界面

### Polacode-2020

这款神器可以将我们的代码转化成一张逼格满满的图片，在写文章或者代码分享的时候。抛出一张这样的图片，可比随手截图体面多了

### REST Client

这款神器可以让我们在`vscode`里面进行接口调试，提供丰富的api配置方式，让我们不用离开编辑器也可以随时调用接口调试

新建一个`.http`文件，写下基本的测试代码，点击` Send Request`即可在右边窗口查看接口返回结果，非常nice，强烈推荐

更多的使用配置，可查看官方文档[传送门](https://marketplace.visualstudio.com/items?itemName=humao.rest-client)

### Browser Preview

这款神器可以让我们在`vscode`里面打开浏览器，一边编码一边查看，偶尔也可以用来摸鱼，非常人性，强烈推荐

### JavaScript Booster

这款神器可以在我们代码写的不规范或者有待调整的地方，在光标聚焦后，会有一个小灯泡。会提示对应的不合理原因和改进方案。极大的提高了我们的代码优雅度，强烈推荐

让您的生活更轻松，使用代码操作为您执行重复性任务！他们可以提供很多帮助，只需跟随灯泡💡！

当在`JavaScript`（或`TypeScript / Flow`）中编辑代码时，此`VS Code`扩展提供了各种代码操作（快速修复）。只需注意左侧的灯泡，然后按一下它即可了解如何在光标下转换代码。

### Settings Sync

这款神器可以让我们的`vscode`配置同步到云端，当我们跟换电脑或者再次安装`vscode`的时候，只需要登录账号即可同步配置了，而不用再次从头开始。简直不要太香了，强烈推荐

### Live Share

这款神器可以使您能够与他人实时进行协作式编辑和调试，无论您使用的是哪种编程语言或正在构建的应用程序类型。什么意思呢？就是可以多人同时编辑一份代码，差不多有点代码共享的意思。不得不说，这款神器就太了不起了，强烈强烈强烈推荐，

搬用官网上的描述

`Visual Studio Live Share`使您能够与他人实时进行协作式编辑和调试，无论您使用的是哪种编程语言或正在构建的应用程序类型。它使您可以立即（安全地）共享当前项目，然后根据需要共享调试会话，终端实例，`localhost Web`应用程序，语音呼叫等！加入您的会话的开发人员会从您的环境（例如语言服务，调试）中获得所有编辑器上下文，从而确保他们可以立即开始进行高效的协作，而无需克隆任何存储库或安装任何`SDK`。

另外，与传统的成对编程不同，`Visual Studio Live Share`使开发人员可以一起工作，同时保留其个人编辑器的首选项（例如主题，键绑定）以及自己的光标。这样，您就可以在彼此之间无缝过渡，并能够自己探索想法/任务。在实践中，这种能力一起工作，并独立地提供了一个合作的经验，是可能有更多的自然常见的用例。





