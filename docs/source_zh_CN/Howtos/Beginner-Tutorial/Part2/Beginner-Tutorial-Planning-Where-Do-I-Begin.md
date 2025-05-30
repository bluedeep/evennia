# 从哪里开始？

好消息是，按照这个入门教程是开始制作 Evennia 游戏的好方法。

坏消息是，每个人都不一样，当涉及到开始自己的游戏时，没有一种放之四海而皆准的答案。相反，我们会提出一系列问题来帮助你自己弄清楚。这也将帮助你评估自己的技能，并可能对你实现目标的速度设定更现实的限制。

> 本课中的问题实际上并不适用于我们的教程游戏，因为我们知道我们这样做是为了学习 Evennia。如果你只想跟随技术部分，可以跳过这一课，等到准备好开始制作自己的游戏时再回来。

## 你这样做的动机是什么？

所以你想制作一个游戏。首先，你需要对自己明确一些事情。

制作一个多人在线游戏是一项_巨大的_任务。如果你和我们大多数人一样，你会把它当作一项爱好来做，而不是为了赚钱。而且你会做很长时间。

所以你应该问自己的第一个问题（如果你有团队，也要问你的团队）是_我为什么要这样做_？在这里进行一些自我反思。以下是一些可能的答案：

- 我想从我的在线社区和/或朋友中获得认可和名声。
- 我想构建这个游戏，以便自己可以玩并享受它。
- 我想构建我已经在玩的游戏，但没有坏人。
- 我想创建一个游戏，以便我可以控制它并成为老大。
- 一个朋友或在线熟人说服我参与这个项目。
- 我这样做是因为我有报酬（哇！）
- 我只是为了自己的利益或看看自己是否能做到而构建这个。
- 我想创建一些东西来回馈我热爱的社区。
- 我想将这个项目作为通向其他项目（例如游戏设计或编程职业）的垫脚石。
- 我对编码或服务器和网络架构感兴趣，制作一个 MUD 似乎是自学的好方法。
- 我想制作一个商业游戏并赚钱。
- 我想实现制作游戏的终身梦想。

还有许多其他可能性。对于一个长期开发项目，你的答案有多“坚实”取决于你。重要的是你要问自己这个问题。

**帮助其他人** - 也许你不应该启动一个新项目 - 也许你更适合帮助其他人或改进已经存在的东西。或者你发现自己更像是一个游戏引擎开发者而不是游戏设计师。

**被情感驱动** - 有些答案可能表明你是由复仇或不安的情绪驱动的。要小心，不要让这成为你唯一的驱动力。当项目最需要你的热情和动力时，这些情绪可能已经减弱。

**走向商业化** - 如果你的目标是赚钱，你的设计目标可能与那些只为爱好或自身利益创作的人大不相同。你可能还会有一个更严格的发布时间表。

无论你的动机是什么，至少应该在你自己的脑海中清楚。确保你的团队也在同一页面上是值得的。

## 你的技能是什么？

一旦你明确了动机，你就需要对自己的技能以及团队中可用的技能进行评估，如果你有团队的话。

你的游戏将有两个主要组成部分，你需要具备相应的技能来满足这两个部分：

- 游戏引擎/代码库 - 在这种情况下是 Evennia。
- 使用游戏引擎创建的资产（“游戏世界”）

### 游戏引擎

游戏引擎由程序员（编码人员）维护和修改。它代表运行游戏的基础设施——网络代码、协议支持、命令处理、脚本编写和数据存储。

如果你只是评估 Evennia，值得做以下事情：

- 在社区/论坛/聊天中闲逛。预计在开始开发时需要问很多“愚蠢”的问题（提示：没有问题是愚蠢的）。这是一个你会感到舒适的社区吗？
- 关注手册（你已经在这里）。
- 你的 Python 技能如何？你的团队技能如何？你或你的团队已经了解它，还是愿意学习？随着 Evennia 开发人员的进展，学习语言并不罕见，但预计这会增加开发时间。你也会更难预测某件事的难度。
- 如果你不了解 Python，你应该已经从本教程的第一部分中了解到一些内容。但预计需要参考外部在线教程——Python 的许多细节不会在这里涵盖。

### 资产创建

与制作 MMORPG 的专业图形所需的工作量相比，制作泥潭的详细文本资产成本较低。这是泥潭非常适合小团队的众多原因之一。

但这并不意味着制作“专业”文本内容很容易。知道如何编写富有想象力且语法正确的散文只是最低的起点要求。一个好的资产创建者（传统上称为“构建者”）还必须能够充分利用游戏引擎的工具来编写事件、制作任务、触发器和互动、有趣的环境。

假设你不是一个人在编码，你团队内部的构建者将是第一个实际“使用”你的游戏框架和构建工具的人。他们会发现所有的错误。这意味着你需要的人不仅仅是“艺术家”或“擅长文字”的人。假设编码人员和构建者不是同一个人（早期测试中很常见），构建者需要能够很好地协作并提供清晰简洁的反馈。

如果你知道你的构建者不懂技术，你可能需要花更多时间为他们制作更简单的构建工具和命令。

## 那么，我应该从哪里开始呢？

好了，经过这一番自我反思和技能盘点，让我们回到最初的问题。也许你已经对答案有了更好的感觉：

- 继续跟随本教程，花时间真正理解示例中发生的事情。这不仅会让你更好地了解各部分是如何结合在一起的，还可能会给你带来一些可能的想法。也许有些事情比你想象的要简单！
- 在 IRC/Discord 聊天中介绍自己，并在浏览教程时不要害羞地提问。不要因为试图解决一些经验丰富的 Evennia 开发人员可能在五分钟内为你解决的问题而感到困扰。此外，并非所有错误都是你的错——教程可能不清楚或有错误，询问可以快速发现这些问题。
- 如果 Python 对你来说是新的，你应该通过第三方 Python 参考资料来补充教程，以便你可以阅读、理解和复制示例代码，而不会完全不知所措。

一旦你完成了入门教程，你将开始做自己的事情。

- 入门教程无法涵盖所有内容。浏览 [Evennia 文档](../../../index.md)。即使你没有阅读所有内容，也会让你对可用的内容有个感觉，以便在以后需要查找某些内容时使用。确保使用搜索功能。
- 你现在可以通过扩展我们将创建的教程游戏来开始。在最后一部分，将有一个可能的未来项目列表，你可以承担。独立工作而不依赖教程是下一步。

至于你的构建者，他们可以开始熟悉 Evennia 的默认构建命令……但请记住，你的游戏尚未建成！不要让你的构建者开始创建大型区域项目。如果他们真的要构建任何东西，那应该是小型测试区域，以达成一致的形式、氛围和文学风格。

## 结论

请记住，通常会杀死一个爱好游戏项目的是你自己的动力不足。因此，尽你所能保持这种动力的强烈！即使这意味着偏离像这样的教程中所读到的内容。只要以最适合你的方式将游戏发布出去即可。

在下一课中，我们将讨论你需要考虑的一些技术问题。这应该可以帮助你更好地了解你想制作的游戏。在随后的课程中，我们将尝试回答这些问题，以便创建我们的小教程游戏。
