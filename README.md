# Adaptive Learning Coach · 自适应学习教练

A project-based learning plugin and standalone skill for Codex: adapt guidance to evidence, respect learner control, and load detailed instructions only when needed.

跨领域、项目驱动、按需加载的教学插件，内含一个可独立安装的 Skill。通过真实任务，让学习者逐步获得解释、修改、验证和迁移能力。

## 能做什么

- 从可观察的目标和已有证据开始，每次推进一个关键学习动作。
- 在引导教学、无提示测评、证据排错、降阶重讲和直接支持之间切换。
- 记录 H0–H4 提示程度，区分任务完成、答案正确、因果解释和迁移表现。
- 复用项目已有进度，按授权写入增量；没有状态文件时可以只在对话中接续。
- 支持编程、英语、职业训练、研究方法和一般概念；工程规则只在工程任务中读取。

用户说“直接讲”或“直接做”时，直接提供帮助。普通事实问答和没有学习意图的代办不进入教学流程。

## 安装

### 作为插件安装

仓库根目录包含 `.codex-plugin/plugin.json`，插件版本为 `2.2.0`，仅包含教学 Skill，无需配置 MCP 服务或连接外部账号。在 Codex 中发送：

```text
请使用 $plugin-creator 将 https://github.com/ZhiHe-ma/adaptive-learning-coach
作为本地插件加入我的个人插件市场并安装，保留仓库已有插件清单和 skills 目录。
```

安装完成后，在新任务中选用“自适应学习教练”插件。个人插件市场中的安装不等于上架官方公共插件目录。插件结构与分发方式参见 [OpenAI 插件文档](https://developers.openai.com/plugins/build/plugins)。

### 仅安装独立 Skill

在 Codex 中使用内置 Skill Installer，发送：

```text
请使用 $skill-installer 从 https://github.com/ZhiHe-ma/adaptive-learning-coach
安装 skills/adaptive-learning-coach。
```

也可下载或克隆本仓库，将 `skills/adaptive-learning-coach` 整个目录复制到个人 Skills 目录：`$CODEX_HOME/skills/`；未设置 `CODEX_HOME` 时使用 `~/.codex/skills/`。保留该目录内的相对结构。如已有同名 Skill，先比较现有版本再决定是否替换。

调用：

```text
$adaptive-learning-coach 带我通过当前项目理解文件写入的成功与失败路径。
```

Skill 保持自动发现。若安装后列表没有更新，重启 Codex。安装和调用机制参见 [OpenAI 官方文档](https://developers.openai.com/zh-Hans/docs/build-skills)。

## 使用示例

```text
$adaptive-learning-coach 教我用英语描述昨天的活动，我是零基础。
$adaptive-learning-coach 继续当前学习项目，先读取已有进度，只给提示。
$adaptive-learning-coach 考我这段代码的返回值和副作用，不要给答案。
$adaptive-learning-coach 我没懂，换一个具体例子。
$adaptive-learning-coach 直接修复这个问题并验证，遵守项目现有边界。
$adaptive-learning-coach 暂停并记录在当前对话，不创建文件。
```

“独立完成”需要学习者实际作答或操作的证据；代理提供答案、运行测试或修复代码，不能代替学习者的表现。涉及写文件、权限、资金或生产数据时，沿用当前授权与项目限制。

## 文件结构

```text
adaptive-learning-coach/
├── .codex-plugin/plugin.json
├── README.md
├── LICENSE
├── THIRD_PARTY_NOTICES.md
└── skills/adaptive-learning-coach/
    ├── SKILL.md
    ├── agents/openai.yaml
    └── references/
        ├── teaching-loop.md
        ├── debugging-loop.md
        ├── state-and-evidence.md
        └── engineering-learning.md
```

插件清单负责插件身份和展示信息；Skill 入口负责教学定位与路由，四个参考文件按触发条件读取。Skill 本体仍只有六个文件，没有运行脚本或必须连接的外部服务。外层的说明和许可证用于开源分发，不需要加载到教学上下文。

## 验证范围

V2.2 制作时通过了 `quick_validate.py` 结构检查，并完成 18 类行为情境试运行，覆盖直接答案、闭卷测评、提示记录、已有状态接续和工程边界。另有临时夹具中的实际修复检查与文件写入函数隔离验证。

这些是有限情境下的验证，不保证所有未来模型输出，也不代表真人学习成效。验证使用的私人项目、学习状态与本机报告不随本仓库发布。

## 来源与许可

本项目依据 MIT 许可证发布，见 [LICENSE](LICENSE)。设计参考了 Matt Pocock 的部分 [skills](https://github.com/mattpocock/skills)，并围绕跨领域教学、证据记录与低上下文消耗进行了重构。原始来源链接保留在相应 Skill 文件底部，来源说明与上游许可证见 [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md)。

本项目为独立项目，不要求安装上游仓库，也不代表 OpenAI 或 Matt Pocock 的官方产品。
