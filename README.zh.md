<div align="center">

# AutoPin-CS

[English](README.md) · 中文 · [Español](README.es.md) · [Deutsch](README.de.md) · [Français](README.fr.md)

</div>

> **本仓库仅用于展示，不公开源码。** AutoPin-CS 是私有项目，所以这里没有代码，只介绍它做什么、怎么构建、长什么样。想聊聊它，请通过我的 [GitHub 主页](https://github.com/frommmmmg)联系我。

**面向大规模社交媒体内容运营的调度与客户端集群管理系统。** 中心服务器向一队 Windows 客户端派发任务，再加一层 AI Agent，让运维人员用日常语言就能操作整个系统。

![AutoPin-CS 架构](assets/autopin-architecture.svg)

**亮点**

- **集中调度与管理。** Flask/uWSGI 服务加 MySQL，管理任务、客户端、订单和统计分析。
- **由 Python 守护进程组成的客户端集群**，运行浏览器自动化流程，针对不同任务类型有多种运行模式。
- **安全的发布流程。** 每次客户端升级都先构建完整包、登记，**在真实的金丝雀机器上验证**后才激活，并随时可回滚。设计上禁止未经金丝雀的全量发布。
- **把运维写成 Agent 技能。** 新机器上线、远程客户端诊断、调度器巡检、发版，都写成 AI Agent 可以执行的技能，由运维人员一句话触发。
- **成文的工程纪律。** ADR、系统契约、操作手册，以及在关闭 bug 前先排查同类缺陷的流程。
- **规模。** 服务端、客户端、桌面控制、部署和测试代码加起来有数千个文件。

**技术栈：** Python · Flask · uWSGI · MySQL · Windows 服务 · 类 Playwright 的浏览器自动化 · FFmpeg

## 截图

*这里特意不放截图：管理后台里有客户端和账号数据。*

## 工作原理

![只有真实的金丝雀机器通过全部门禁，版本才会被激活。](assets/autopin-release-gate.svg)
*只有真实的金丝雀机器通过全部门禁，版本才会被激活。*

![运维人员用日常语言下指令，Agent 执行固定的操作手册并读回证据。](assets/autopin-agent-loop.svg)
*运维人员用日常语言下指令，Agent 执行固定的操作手册并读回证据。*

---

<div align="center">

<sub>截图只使用示例或公开数据。© 保留所有权利。描述文字可注明出处后引用，软件本身不可再分发。</sub>

</div>
