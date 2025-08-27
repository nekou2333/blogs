---
title: 「翻译」The Second Half
published: 2025-08-19
description: ''
image: ''
tags: [LLM, 翻译]
category: 翻译
draft: false 
lang: ''
---

原文：<https://ysymyth.github.io/The-Second-Half/>

## The Second Half

> This recipe is completely changing the game. To recap the game of the first half:
>
> - We develop novel training methods or models that hillclimb benchmarks.
> - We create harder benchmarks and continue the loop.
>
> This game is being ruined because:
>
> - The recipe has essentially standardized and industried benchmark hillclimbing without requiring much more new ideas. As the recipe scales and generalizes well, your novel method for a particular task might improve it by 5%, while the next o-series model improve it by 30% without explicitly targeting it.
> - Even if we create harder benchmarks, pretty soon (and increasingly soon) they get solved by the recipe. My colleague Jason Wei made a beautiful figure to visualize the trend well:

这个方法正在彻底改变游戏规则。回顾一下上半场的游戏：

- 我们开发新颖的训练方法或模型来逐步提升基准测试的性能。
- 我们创建更难的基准测试，然后继续这个循环。

这个游戏之所以正在被破坏，原因如下：

- 该方法本质上已经将基准测试的性能提升过程标准化和工业化，不再需要太多新的想法。由于这种方法具有良好的扩展性和泛化性，你针对特定任务提出的新颖方法可能只能将性能提升5%，而下一个o系列模型在没有明确针对该任务的情况下就能将其提升30%。
- 即使我们创建更难的基准测试，很快（而且越来越快）它们也会被这种方法解决。我的同事杰森·魏（Jason Wei）制作了一张精美的图表，很好地可视化了这一趋势：

![](Pasted%20image%2020250819190444.png)

> Then what’s left to play in the second half? If novel methods are no longer needed and harder benchmarks will just get solved increasingly soon, what should we do?

那么下半场还有什么可玩的呢？如果不再需要新颖的方法，更难的基准测试也会很快被解决，我们该怎么办？

> I think we should fundamentally re-think evaluation. It means not just to create new and harder benchmarks, but to fundamentally question existing evaluation setups and create new ones, so that we are forced to invent new methods beyond the working recipe. It is hard because humans have inertia and seldom question basic assumptions - you just take them for granted without realizing they are assumptions, not laws.

我认为我们应该从根本上重新思考评估。这意味着不仅仅是创建新的、更难的基准测试，而是从根本上质疑现有的评估设置并创建新的评估设置，这样我们就不得不发明超越现有有效方法的新方法。这很难，因为人类有惯性，很少质疑基本假设——你只是想当然地接受它们，却没有意识到它们是假设，而不是定律。

> To explain inertia, suppose you invented one of the most successful evals in history based on human exams. It was an extremely bold idea in 2021, but 3 years later it’s saturated. What would you do? Most likely create a much harder exam. Or suppose you solved simply coding tasks. What would you do? Most likely find harder coding tasks to solve until you have reached IOI gold level.

为了解释惯性，假设你发明了历史上最成功的基于人类考试的评估之一。在2021年，这是一个极其大胆的想法，但3年后它就饱和了。你会怎么做？最有可能的是创建一个更难的考试。或者假设你解决了简单的编码任务。你会怎么做？最有可能的是找到更难的编码任务去解决，直到达到IOI金牌水平。

> Inertia is natural, but here is the problem. AI has beat world champions at chess and Go, surpassed most humans on SAT and bar exams, and reached gold medal level on IOI and IMO. But the world hasn’t changed much, at least judged by economics and GDP.

惯性是自然的，但问题就在这里。人工智能已经击败了国际象棋和围棋的世界冠军，在SAT和律师资格考试中超过了大多数人类，在IOI和IMO中达到了金牌水平。但世界并没有发生太大变化，至少从经济和GDP来看是这样。

> I call this the utility problem, and deem it the most important problem for AI.
>
> Perhaps we will solve the utility problem pretty soon, perhaps not. Either way, the root cause of this problem might be deceptively simple: our evaluation setups are different from real-world setups in many basic ways. To name two examples:

我将此称为效用问题，并认为它是人工智能最重要的问题。

也许我们很快就能解决效用问题，也许不能。无论如何，这个问题的根本原因可能简单得令人难以置信：我们的评估设置在许多基本方面与现实世界的设置不同。举两个例子：

> - Evaluation “should” run automatically, so typically an agent receives a task input, do things autonomously, then receive a task reward. But in reality, an agent has to engage with a human throughout the task — you don’t just text customer service a super long message, wait for 10 minutes, then expect a detailed response to settle everything. By questioning this setup, new benchmarks are invented to either engage real humans (e.g. Chatbot Arena) or user simulation (e.g. tau-bench) in the loop.

- 评估“应当”是自动化运行的，因此通常智能体接收任务输入后会自主行动，然后获得任务奖励。但实际上，智能体在整个任务过程中都必须与人类互动——你不会只给客服发一条超长消息，等10分钟就指望得到详细回复并解决所有问题。通过对这种设置提出质疑，新的基准测试被开发出来，将真实人类（例如Chatbot Arena）或用户模拟（例如tau-bench）纳入循环。

> - Evaluation “should” run i.i.d. If you have a test set with 500 tasks, you run each task independently, average the task metrics, and get an overall metric. But in reality, you solve tasks sequentially rather than in parallel. A Google SWE solves google3 issues increasingly better as she gets more familiar with the repo, but a SWE agent solves many issues in the same repo without gaining such familiarity. We obviously need long-term memory methods (and there are), but academia does not have the proper benchmarks to justify the need, or even the proper courage to question i.i.d. assumption that has been the foundation of machine learning.

- 评估“应当”满足独立同分布（i.i.d.）。如果你有一个包含500个任务的测试集，你会独立运行每个任务，取任务指标的平均值，从而得到整体指标。但现实中，你是按顺序而非并行地解决任务。一名谷歌软件工程师（SWE）会随着对代码库的熟悉程度提高，越来越出色地解决google3的问题，而一个软件工程师智能体在处理同一个代码库中的多个问题时却不会获得这种熟悉度。显然，我们需要长期记忆方法（而且确实存在一些），但学术界缺乏恰当的基准测试来证明这种需求的合理性，甚至缺乏质疑独立同分布这一机器学习基础假设的勇气。

>These assumptions have “always” been like this, and developing benchmarks in these assumptions were fine in the first half of AI, because when the intelligence is low, improving intelligence generally improves utility. But now, the general recipe is guaranteed to work under these assumptions. So the way to play the new game of the second half is

这些假设“一直以来”都是如此，在人工智能的前半场，基于这些假设开发基准测试是可行的，因为当智能水平较低时，提高智能通常会提升效用。但现在，在这些假设下，通用方法已被证明是有效的。因此，人工智能下半场的新玩法是：

> We develop novel evaluation setups or tasks for real-world utility.
> We solve them with the recipe or augment the recipe with novel components. Continue the loop.

我们为现实世界的效用开发新颖的评估设置或任务。
我们使用通用方法来解决这些问题，或者用新颖的组件增强通用方法。如此循环往复。

> This game is hard because it is unfamiliar. But it is exciting. While players in the first half solve video games and exams, players in the second half get to build billion or trillion dollar companies by building useful products out of intelligence. While the first half is filled with incremental methods and models, the second half filters them to some degree. The general recipe would just crush your incremental methods, unless you create new assumptions that break the recipe. Then you get to do truly game-changing research.

这个游戏之所以困难，是因为它陌生。但它也令人兴奋。如果说上半场的参与者在解决电子游戏和考试问题，那么下半场的参与者则通过将智能转化为有用的产品，打造价值数十亿甚至数万亿美元的公司。如果说上半场充斥着增量式的方法和模型，那么下半场在某种程度上会对它们进行筛选。通用方法会轻松碾压你的增量式方法，除非你创造新的假设来打破这种通用方法。那样，你就能开展真正具有颠覆性的研究。

欢迎来到下半场！
