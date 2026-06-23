# 揭穿AstrBot闹剧:  一场由AI敷衍引发的"跨服"与降维打击

## 0. 荒谬的起点:  看不懂 Issue 与满篇的 AI Slop
我提了个 Issue https://github.com/AstrBotDevs/AstrBot/issues/8552
社区初见时选择用 AI 回复我. 完整论述如下: 

有个贡献者 **NayukiChiba** 跑来用 AI 回复(在他的回复中, 甚至把 Astrbot 当成了外部 SaaS 服务).

![敷衍回复](https://github.com/bytecategory/slam/blob/main/img/哪里是开源项目呀这明明是外部saas服务好不好.png)

后来他开始胡乱问: "你的llm是什么?你是 docker 部署还是直接跑源码?"
![胡乱问](https://github.com/bytecategory/slam/blob/main/img/胡乱问.png)

这和我的 llm 是什么/用的是不是 docker 无关.我已经说得很明白了:  Agent 执行命令 `rm -rf` 某个目录, 然后 Astrbot 就阻止了这条命令, 导致后续中断.

NayukiChiba 看不懂我的意思是想要去除这一功能, 即去除阻止这些命令的功能, 反而把我的抱怨当成核心的来看, 即"判断 Linux 版本, 获取表地址, 绕过写保护, 内核挂钩 unlinkat"这句话.

## 1. 恶人先告状
VanillaNahida 说的我人身攻击别人的证据在这里(记住以后要考), 我帮他找出来了: 
![不理解中间人攻击](https://github.com/bytecategory/slam/blob/main/img/不理解中间人攻击.png)
![以其人之道还治其人之身](https://github.com/bytecategory/slam/blob/main/img/以其人之道还治其人之身.png)

图一先发生(被引用的是我说的), 图二后发生. 可以看到是 **advent259141** 先来骂我的. 

至于他说的配置证书和 SSL 应该让 Nginx 或者 Caddy 来干 &mdash; 他们 Astrbot 小白那么多, 指望人人都会配 Nginx 反代可能吗?同时我指出他连 Github Profile 中的 Markdown 都写不明白,  这就成人身攻击了? 下图是证据

![md语法不会我教你呀](https://github.com/bytecategory/slam/blob/main/img/你先学会md语法吧.png)

## 2. 伪装理中客的Review 与 双向标准
再来看 **VanillaNahida** 在视频中的 review: 
![review](https://github.com/bytecategory/slam/blob/main/img/不专业的review.png)
`llm_compress_keep_recent_ratio` 设为 0 的意思是, 最新的对话内容都会被压缩, 而不是丢失掉. 所以他错了. 而且他是故意发现我已经 block 他后, 才去提交一个技术评论装理中客, 前面他一直在骂人. 无图无真相

![到底是谁在人身攻击](https://github.com/bytecategory/slam/blob/main/img/一上来就人身攻击.png)

## 3. 114514 的技术底色与巴甫洛夫的狗
在 [PR 8590](https://github.com/AstrBotDevs/AstrBot/pull/8590/changes/fe19528864c79af9a3c31cc4193d279963630094) 中, `max_agent_step` 设置为 114514, 是不做限制. 而他们看到 114514 只会像巴甫洛夫的狗一样条件反射. 他们也承认 30 没有什么依据, 只是一个经验值, 30 = 1 * -1 + 45 - 14, 事实上任何数字都是恶臭的. 

来看看真正的大佬对 114514 的处理态度: 
https://github.com/XTLS/REALITY/pull/29/changes/ba1a82a348da0b74f5d093bcfaababa37e157e89
这是由**风扇滑翔翼**大佬亲自编写的提交. 我解释一下 `record_detect.go` 中 163-189 行的变更: 
如果探测时对端对 2,  15,  16 个 CSS 都不 alert, 那就把 `1145141919810` 存进 `GlobalMaxCSSMsgCount` 里. 当然不是说真能发到 1145141919810 个 ChangeCipherSpec 消息, 只是不做限制罢了. 

![真大佬怎么做](https://github.com/bytecategory/slam/blob/main/img/专业人士的做法.png)

后来这个值因为 **RPRX** 发现 1145141919810 写太大在 32 位系统爆炸了, 于是才在 https://github.com/XTLS/REALITY/commit/9234c772ba8f181f31c3e81dc2b4177322e5a9a9 中改成了 `math.MaxInt`. 

![太大了](https://github.com/bytecategory/slam/blob/main/img/太大了.png)

## 4. 盲信 AI 评价与 Let's Encrypt 常识处刑
<img src="https://github.com/bytecategory/slam/blob/main/img/关于我的aaaa传输和a传输最奇葩的评价.jpg" height="250">

A/AAAA 传输竟然被 AI 说成了玩具 fork? 这是伊朗环境需要的!
第三个提交信息叫 `meow~` 的, 是根据 RPRX 的指示, 改回了正确的格式. 

![RPRX的指示](https://github.com/bytecategory/slam/blob/main/img/RPRX的指示.png)

说我没有 PR 更是贻笑大方: https://github.com/XTLS/Xray-core/pull/6123 这是什么?

![ip证书不能申请了](https://github.com/bytecategory/slam/blob/main/img/ip证书不能申请了.png)

至于证书, Let's Encrypt 在 2025 年 7 月就发布了[第一个 IP 证书](https://letsencrypt.org/2025/07/01/issuing-our-first-ip-address-certificate), [在 2026 年宣布正式发布](https://letsencrypt.org/2026/01/15/6day-and-ip-general-availability). 
而我们看一下 DeepSeek v4 pro 的知识库截止日期是 2025 年 5 月 &mdash; 这下明白了, 网页版 ds 闹麻了. 

![6天IP证书](https://github.com/bytecategory/slam/blob/main/img/6天IP证书.png)

来自datalearner的数据如下

![知识截止](https://github.com/bytecategory/slam/blob/main/img/知识截止.png)

## 5. 结语
最后再来一句: 要吵就到 https://github.com/XTLS/Xray-core/pull/6287 里去. 
那里是对 WireGuard 的重写, 使其更接近原生 socket 的行为. 期间除了个 close pipe 的 bug, 我虽然没帮上什么忙, 好歹帮他确定了读方向还是写方向. 

我估计那群人只能发布些 AI slop, 然后被 Fangliding 一脚飞掉. 
## 6. 补充: 关于"靠 AI 写代码"的指控
针对B站评论区诸如"这就是 ai 编程普及的弊端……不会写代码,全靠 AI"的言论, 我在此做个正式回应:

抱歉, 我曾经是malware developer, 这些代码AI都会拒绝生成, 我到时候把它们公开.

## 7. 我为何要写下它?

![逆天嘉豪](https://github.com/bytecategory/slam/blob/main/img/逆天嘉豪.png)

这是因为UP主 香草味的纳西妲喵 在 https://www.bilibili.com/video/BV1LD7U65Ew2/ 中公然谩骂我是逆天嘉豪,我不得已才奋起反击.
