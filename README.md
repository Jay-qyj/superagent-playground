# superagent-playground

`superagent-playground` 是 [dsh-superagent](https://github.com/deepseek-ai/dsh-superagent-prototype) 智能体（GitHub 账号 **BT7276-agent**）的工作与试验仓库。

[dsh-superagent](https://github.com/deepseek-ai/dsh-superagent-prototype) 是一个面向单个 GitHub 仓库的主动式编码智能体，以 [DeepSeek Harness](https://www.deepseek.com/en/harness/) 的 bundle 形式运行。它监听 GitHub（以及可选的 Feishu），把有人明确授权的请求转成工作项（Ticket），在自己的 Session 与工作目录中完成，并把结果——例如一个 Pull Request——回写到原来的对话里。

> dsh-superagent 是团队日常开发中生长出来的研究原型，仅供参考，**不是 DeepSeek 官方产品**。它可能包含缺陷，工程实践也不保证统一，使用前请自行审阅。

## 谁在这里工作

- **智能体账号**：[BT7276-agent](https://github.com/BT7276-agent)。智能体提交的代码、分支和 Pull Request 都以该账号署名。
- **服务**：dsh-superagent 运行在本机 `superagent` profile 中，管理面板位于 `http://127.0.0.1:3082`（侧边栏的 **Superagent** 入口）。
- **授权策略**：白名单制，只有运营者（`Jay-qyj`）可以向智能体派活；智能体以 `observe` 模式记录主动工作，不擅自执行。
- **对话入口**：GitHub 与 Feishu 机器人（糖小菲 / SU-agent）。

## 如何让智能体干活

**GitHub**：在仓库的 Issue 中评论，并 @ 智能体账号，例如：

```
@BT7276-agent 给这个项目添加一个 README 文档
```

大约一分钟后，面板里就会出现对应的 Ticket，智能体开始处理。

**Feishu**：直接给机器人发消息，或在订阅的群组里 @ 它。

## 工作流程

1. 请求进入后，dsh-superagent 依据 Policy 判断是否接受；接受则创建一个 **Ticket**。
2. 每个 Ticket 在 `~/src/superagent-playground` 的本地克隆上，用 Git worktree 切出一个独立工作目录，并创建分支 **`agent/<ticket>`**。
3. 智能体在该分支上提交、自测，然后以 `BT7276-agent` 的身份开 **Pull Request**，并把结果回复到原始对话。
4. **人工合并**：智能体不会给自己开的 Pull Request 启用 auto-merge，由人审阅并合并。合并或关闭后，相关 Ticket 仍订阅该 PR 线程，后续评论可继续推进工作。

## 约定

- 分支前缀 `agent/`（智能体的工作分支），主干为 `main`。
- 一个 Ticket 对应一个 worktree、一个分支，互不干扰。
- 智能体只在被授权时写入，并且不在仓库内开启自动合并。

## 相关文档

dsh-superagent 的概念与部署细节见其仓库中的编号文档，建议按顺序阅读：

- [000 Philosophy](https://github.com/deepseek-ai/dsh-superagent-prototype/blob/main/docs/000-philosophy.md)
- [001 Domain model](https://github.com/deepseek-ai/dsh-superagent-prototype/blob/main/docs/001-domain.md)
- [002 Authorization](https://github.com/deepseek-ai/dsh-superagent-prototype/blob/main/docs/002-authorization.md)
- [003 Execution](https://github.com/deepseek-ai/dsh-superagent-prototype/blob/main/docs/003-execution.md)
- [005 Panel](https://github.com/deepseek-ai/dsh-superagent-prototype/blob/main/docs/005-panel.md)
- [006 Deployment](https://github.com/deepseek-ai/dsh-superagent-prototype/blob/main/docs/006-deployment.md)
