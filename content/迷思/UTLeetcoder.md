我在学习 [CSC236](https://artsci.calendar.utoronto.ca/course/csc236h1) 和 [CSC263](https://artsci.calendar.utoronto.ca/course/csc263h1) 的时候，发现了Leetcode这个网站并开始使用Leetcode做题来巩固自己的对data structure和algorithm以及对应的analysis的理解。在我做了一段时间后发现，Leetcode并不会提供用户具体的数据，例如一天或者一周做了多少题。

于是我找到了我的室友们准备一起开发一款网页应用，用来帮助用户有效地追踪他们的日常做题任务。在进行设计后，我们进行了分工。我负责开发网页，包括但不限于设计用户界面，数据显示界面，并且同时保证应用在数据处理和同步方面的高效性。而我的室友们则主要负责后端的数据处理。

我们决定前端使用React框架，于是我们使用 [create-react-app](https://create-react-app.dev/)作为我们的build tool. 此外并我们还使用Ant Design大大缩短了设计component的时间。

一开始我们准备后端使用Express.js + Node.js + MongoDB搭建。这样一来我们可以设计用户系统，用户可以自行注册，注销。但这将让我们需要购买服务器或者购买一些云服务。为了降低成本，我们决定舍去了db并将数据序列化存储在Github上。此外我在测试阶段帮助改了后端的一些bug。

具体后端设计可以[参考](https://zhuyuezx.github.io/coding/2023/01/20/utleetcoder-website.html)

因为我们没有服务器，所以我们制定了CI Pipeline，利用GitHub Actions进行数据的自动抓取与处理，并自动部署在Github page上。