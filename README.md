<img width="1440" height="810" alt="image" src="https://github.com/user-attachments/assets/98b58ccf-f79d-48d7-a893-801354c1f18c" />

# Grok Bot 接入微信：3 步，把 AI 员工装进手机

以前用 AI，是这套流程：打开网页，敲问题，复制结果，粘贴走人。

现在可以换个玩法。你在地铁上、在路边等人，甚至在床上，给微信发一句：

`帮我整理今天 OpenAI、Claude、Grok 的最新动态。`

然后放下手机。云端的 Grok Bot 会自己去搜索、分析、排版，几分钟后，成品回到你的微信里。

今天就带你实操一遍：怎么把 Grok Bot 接进个人微信。

## 一、Grok Bot 到底是什么？

一句话：xAI 推出的 AI Agent，你可以把它当成**一个自带电脑的 AI 员工**。

它和普通 Grok 聊天最大的区别，是它真的会"干活"：

- **云端电脑：** 有自己的浏览器、终端和文件系统，不只是动嘴。
- **长期记忆：** 记得你的工作习惯和任务背景，不用每次从头交代。
- **自动化：** 重复任务可以定时跑，到点自己开工。
- **多 Bot 协作：** 能拉起多个助手，分工合作。

最关键的一点：任务在云端执行，你合上电脑，它不一定停工。

官方入口：<u>x.ai/bot</u>

## 二、需要什么会员？

新版 The X Subscription 的 **Premium、Super、Ultra** 套餐，都含 Grok Bot 权益。

<img width="720" height="436" alt="image" src="https://github.com/user-attachments/assets/39ddcd60-fb5e-4cd0-a1c5-db16e29aaa61" />


安装 Grok Bot，登录有权益的账号，就能开工。

国内绑卡、订阅页打不开，或想直接升到带 Bot 的档位，别卡在支付这一步——可走 [cnmgrok.com](https://cnmgrok.com/) 办理 **Grok Premium**（以及更高的 Super / Ultra 相关权益，以站点当前套餐为准）。开通后再用同一账号登录 Bot，下面的微信桥才能接得上；

免费号再怎么折腾提示词，也开不出完整 Grok Bot。


## 三、实战：3 步接入微信

先说清楚一件事：**这不是 Grok Bot 的内置功能**，而是社区方案。思路是用微信 ClawBot 的 iLink 通道，配合 Grok Bot 的 Webhook Routine 和第三方转发程序，把两头接起来。

### 第一步：打开微信 ClawBot

先确认微信版本够新：

- iOS：8.0.70 及以上
- Android：8.0.69 及以上

然后依次点：我 → 设置 → 插件，找到「微信 ClawBot」并启用。


<img width="662" height="734" alt="image" src="https://github.com/user-attachments/assets/ff0b4600-2828-4032-aa7e-7b649cabe951" />

如果插件列表里没有它，多半是你的账号还没被开放，光升级版本未必管用，这个只能等。

### 第二步：让 Grok Bot 自己搭桥

最省事的做法：别手动折腾，直接让 Bot 自己部署。打开 Grok Bot 的主对话，发这段提示词：

> 请帮我通过微信 ClawBot 的 iLink 通道，将我的个人微信连接到 Grok Bot。
>
> 使用项目：https://github.com/lawrencewzen/wx-bot
>
> 请先阅读项目 README 和 AGENTS.md，检查兼容性与安全风险，再协助我完成安装。
>
> 要求：
> 1. 使用微信 ClawBot 接收我的消息。
> 2. 通过 Webhook Routine 将消息交给当前 Grok Bot。
> 3. 处理完成后，将回复发送回微信。
> 4. 将登录凭证和 Webhook 密钥保存在私密环境中，不输出到普通聊天记录。
> 5. 需要扫码、授权时暂停并提示我。
> 6. 完成后测试消息收发，并说明如何重启和停止服务。
>
> 不要在未确认前执行删除文件、外发敏感信息或高风险操作。
<img width="720" height="373" alt="image" src="https://github.com/user-attachments/assets/2109042a-57bd-4aab-846f-430427d273f1" />


接下来 Bot 会读文档、配环境、建 Routine。中途如果要你保存 Webhook URL 和密钥，请走安全凭证输入，**千万别直接贴在聊天里**。

### 第三步：扫码，发第一句话

桥搭好之后：

1. 按提示拿到微信登录二维码；
2. 用微信扫一扫，确认绑定；
3. 打开 ClawBot 对话，主动发一条测试消息。
<img width="674" height="426" alt="image" src="https://github.com/user-attachments/assets/450cd9a3-436c-4240-ac55-ed44ef1c0f7a" />



收到回复，说明消息链路通了。没收到也别急，按顺序排查四个环节：微信绑定、转发程序、Webhook 执行状态、回复发送结果。

## 四、真实场景：微信一句话，出一份 AI 简报

接入完成，来跑一个最有用的场景。在 ClawBot 里发：

> 帮我整理最近 24 小时 OpenAI、Anthropic、xAI 和 Google 的重要 AI 新闻。只保留 5 条最值得关注的内容，包含标题、发布时间、一句话摘要和官方来源链接。用中文回复，不要编造。

背后的链路是这样的：

**微信发消息 → ClawBot 接收 → 转发程序触发 Grok Bot → Bot 搜索整理 → 报告回到微信**

你会收到类似这样的简报：

<img width="720" height="514" alt="image" src="https://github.com/user-attachments/assets/c42951a2-4d28-4e8b-8392-3596989a9c4b" />


以上只是格式示例，具体内容由 Bot 实时查询生成，不会提前填入没核实过的消息。

玩熟之后，还能往外扩：竞品监控、资料整理、代码排查，甚至在微信里指挥多个 Bot 分头干活。

## 五、踩坑提醒

**1. 微信并不是直连 Grok Bot。**
中间隔着一层第三方转发程序。云端电脑重启、服务中断、登录状态失效，都可能让你收不到回复。

**2. 别让多个机器人抢同一个微信号。**
同一个号同时挂多个 ClawBot/OpenClaw 通道，消息可能被别的实例截走。

**3. 微信的主动推送有时间窗口。**
太久没和机器人互动，主动推送未必送得到。所以定时日报，没法保证每次都准时落到微信。

**4. 权限别一次给满。**
刚开始只给查询、整理、回复。涉及支付、删除、群发、改账号设置的操作，务必人工确认。

**5. 接入微信不等于免费。**
Bot 干的每一件活，都在消耗账号的使用额度。

## 六、写在最后

Grok Bot 真正吸引人的地方，不是多了个聊天窗口，而是**AI 开始替你把活干完**。

接入微信之后，手机成了指挥入口：你只管交代任务，回头看结果。

如果你天天要盯 AI 新闻、整理资料、处理重复的办公杂活，这套玩法值得折腾一次。

前提只有一个：账号先有 Grok Bot 权益。国内想稳妥升到 **Grok Premium**（或更高档），开通路径可看 [cnmgrok.com](https://cnmgrok.com/)，办完再用同一账号登录 Bot、接微信。

