# step-by-step-coach

`step-by-step-coach` 是一个 Codex Skill，用来一步一步地教用户从 0 到 1 达成目标，而不是一上来就直接替用户把事情做完。

它适合这类“陪跑式”场景：

- 从零开始搭建一个项目
- 学习新的工具或工作流
- 以引导方式修复 bug，而不是直接打补丁
- 一步一步完成环境配置
- 先理解某个功能该怎么实现，再决定是否让 Codex 接手

## 这个 Skill 会做什么

当 Skill 被触发时，Codex 会：

- 先澄清目标结果和当前起点
- 把任务拆成小里程碑
- 一次只教下一步
- 在自然检查点暂停
- 在需要时提供局部示例、提示、代码片段或伪代码
- 默认避免直接交付完整实现
- 保留可续接的状态，让任务之后还能继续

## 默认行为

这个 Skill 默认工作在教学陪跑模式。

这意味着 Codex 应该：

- 引导用户，而不是悄悄接管任务
- 保持解释简洁、面向行动
- 一次只推荐一个最合适的下一步
- 根据用户已经尝试过的内容和观察到的结果动态调整

默认情况下，Codex 不应该：

- 直接产出完整成品
- 从头到尾重写整个文件
- 在没有明确许可的前提下把整件事做完

## 模式切换

如果用户明确要求直接执行、完整实现，或者明确表示“你来做”，Codex 可以退出教学模式，切换到代做模式。

这种切换应该被明确说明，让用户知道当前交互方式已经改变。

## 跨线程续接

这个 Skill 设计时就考虑了“中途暂停”和“切换线程”的场景，不依赖隐式线程记忆。

它使用三层续接机制：

- 在线程中的自然检查点输出简短进度摘要
- 提供可复制的 `Resume` 块，方便切换到新线程
- 在需要时把状态写入项目目录，例如 `./.codex/coach-state.yaml` 或 `./progress.md`

和具体项目相关的进度状态应该放在项目目录或工作区里，而不是放在 Skill 安装目录里。

## 示例提示词

- `Use $step-by-step-coach to teach me how to build this feature from scratch.`
- `Use $step-by-step-coach and guide me through fixing this bug without patching it directly.`
- `Use $step-by-step-coach to walk me through setting up this project step by step.`
- `Use $step-by-step-coach to coach me through this task first. If I get stuck, we can switch to direct implementation later.`

## 文件说明

- `SKILL.md`：触发描述和核心行为说明
- `agents/openai.yaml`：Skill 的 UI 元数据
- `references/continuation.md`：续接模板和项目状态文件方案

## 安装方式

把整个 Skill 目录放到：

```bash
~/.codex/skills/step-by-step-coach
```

之后可以显式使用 `$step-by-step-coach`，也可以通过这类请求自然触发：

- “一步一步教我”
- “不要直接帮我做，带我做”
- “walk me through it”
- “guide me instead of doing it for me”
- “先不要直接改代码，带我做”

## 仓库用途

这个仓库用于版本化和分享 `step-by-step-coach` 这个以“教学优先”为核心的 Codex Skill。
