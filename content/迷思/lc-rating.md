---
date: 2024-07-20
---

## 前导

在做题的过程中，我发现一个好的题解非常重要，可以帮助我更好的理解题目，也可以帮助我更好的学习。在经历了一系列的翻找以后我觉得0x3f讲的很好，同时我也发现了[该网站](https://huxulm.github.io/lc-rating)记录了有哪些题是有0x3f写过的题解的以及包含了一些0x3f所列的题单。唯一美中不足的是我在美服leetcode上做题而他所有题目链接都是国服上的，这让我决定做个button以便于切换。

这是我第一次完整的查看别人的项目，我的想法是从部署到component的设计逆着看，这有助于我梳理逻辑。

这个项目和我之前的所做过的utleetcoder很像，都是noserver的项目并且通过github action进行CI/CD

## 添加button

我简单的观察了一下，在该项目中有个hooks的folder，并发现该项目中并没有使用reducer。所以我决定加一个site hook，用来检查当前site state。然后我在需要的界面加了一个button用于更改state
具体更改[如内](https://github.com/huxulm/lc-rating/pull/12/commits)，但是我发现当一个页面的网址数量过多时，变换的速度会特别慢于是关了。

## 添加python script

在做题过程中发现题单似乎并没有人在维护，于是研究了一下，发现维护题单是依赖`/lc-maker/js/`下的script实现的。需要人手动复制script，然后进入对应的题单并在浏览器的console里运行script，在得到数据后还得自己手动处理。

在我研究的过程中，我发现repo owner已经将大部分对应的leetcode api写在了一个file里，这无疑是一个好消息，该项目更新题单依靠的来源正是leetcode discussion. 于是我加了一个新的gql operation，并开了一个新的script叫`0x3f_discuss.py`. 项目开头，先hard code将已有的discussion和他们的title都对应起来。并建立了对应的页面显示时所需的data class。接下来执行gql operation得到markdown数据并开始处理数据。并更新到对应的data里。
