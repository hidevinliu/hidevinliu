<a id="en"></a>

## Hi, I'm Devin

[English](#en) · [中文](#zh)

**I build guardrails that let AI coding agents work unattended and still be trusted.**

AI agents do real delivery work for me every day: internal tools, data pipelines, knowledge bases,
websites. Getting an agent to write code was never the hard part. Knowing whether its "done" really
meant done was.

Every time an agent told me something was finished and it wasn't, I turned that failure into a
check that rules on an exit code. The repos below are those checks.

### What I work on and care about

- **AI-assisted programming.** How coding agents plan, verify and hand work off, and what it takes
  to let them run for hours, or several at once, without losing control.
- **Product architecture.** Turning a vague idea into a clear structure before anyone writes code:
  modules, data models, flows and acceptance criteria.
- **Engineering governance.** Keeping a codebase and its rules trustworthy over time: one source of
  truth, acceptance contracts, and guardrails that block a bad change instead of just warning about it.
- **Agent algorithms.** The decision logic inside an agent loop: telling when a loop has stalled,
  choosing which files and functions an agent should see, routing a task to the right tool, and
  recalling how a similar failure was fixed before.

### The pipeline: five places an AI agent's "done" can be wrong

| # | Where it goes wrong | What I built | Status |
|---|---|---|---|
| 1 | **The spec.** The request is vague, so the agent builds the wrong thing correctly. | [**AI-PRD-Devin**](https://github.com/hidevinliu/AI-PRD-Devin): turns a one-line idea into a spec sized to the task, and hands off a machine-readable acceptance contract | Shipped |
| 2 | **The grader.** The agent makes the tests pass by editing the tests. | [**red-green-mode**](https://github.com/hidevinliu/red-green-mode): an exit-code referee that catches skipped tests, deleted assertions and suppressed errors in the diff | Shipped · 262 tests · zero dependencies |
| 3 | **The test itself.** The test was green from birth and never checked anything. | [**mutation-check**](https://github.com/hidevinliu/red-green-mode/tree/main/skills/mutation-check): breaks the code on purpose; the test must go red | Shipped, inside red-green-mode |
| 4 | **Memory.** Every loop starts from zero and falls into the same hole again. | Loop state plus a record of past fixes, recalled when the same kind of failure comes back | Coming soon |
| 5 | **The report.** The agent says it finished. The git log disagrees. | A status sweep that checks each agent claim against commits, CI and file timestamps, and reports only the mismatches | Coming soon |

### How I think about building with agents

- **The exit code is the judge, not the agent.** A model's opinion of its own work is not evidence.
  A verifier that actually ran is.
- **Green is not done.** Tests passing, the spec being delivered and the UI matching the reference
  are three separate checks. One does not stand in for another.
- **Never fake green.** Deleting a test, loosening an assertion or mocking out the logic under test
  is the one thing an autonomous loop must never do. If a test looks wrong, stop and ask.
- **Size the process to the task.** A new product gets a full spec. A bug fix gets a five-line plan.
- **The smallest correct change.** Reuse what the project already has, then the standard library,
  and only then add a dependency, with the reason written down.
- **"Unverified" is an honest answer.** Report what actually ran and what did not. A tool being
  configured is not the same as a check having passed.

---

<a id="zh"></a>

## 你好，我是 Devin

[English](#en) · [中文](#zh)

**我做的是这样一类工具：让 AI 编程 agent 在没人盯着的时候，交出来的东西依然可信。**

AI agent 每天都在替我做实际的交付工作：内部工具、数据管道、知识库、网站。让 agent 写代码从来不难，难的是判断它说的"做完了"是不是真做完了。

每次 agent 说完成了、结果没完成，我就把这个坑做成一道检查，由程序的退出码来裁决。下面这些仓库，就是这些检查。

### 我擅长和关注的方向

- **AI 编程**：编程 agent 怎么规划、怎么验证、怎么交接工作，以及让它连续跑几个小时、或者几个同时跑的时候，怎样不失控。
- **产品架构梳理**：在写代码之前，把模糊的想法理成清晰的结构：模块、数据模型、流程和验收标准。
- **工程化治理**：让代码库和规则长期保持可信：同一件事只有一个权威来源，验收标准写成契约，护栏遇到坏改动直接拦下，而不只是提醒。
- **Agent 相关算法**：agent 循环里的决策逻辑：判断循环是不是卡住了，挑出 agent 该看的文件和函数，把任务分给合适的工具，调出以前同类失败的修法。

### AI agent 的"做完了"可能在五个地方出错

| # | 哪里出错 | 我做的工具 | 状态 |
|---|---|---|---|
| 1 | **需求**：需求太模糊，agent 把错的东西做得很对 | [**AI-PRD-Devin**](https://github.com/hidevinliu/AI-PRD-Devin)：把一句话想法按任务大小写成规格，并交出机器能读的验收契约 | 已发布 |
| 2 | **裁判**：agent 靠改测试让测试通过 | [**red-green-mode**](https://github.com/hidevinliu/red-green-mode)：只认退出码的裁判，从改动里抓出被跳过的测试、被删掉的断言、被屏蔽的报错 | 已发布 · 262 个测试 · 零依赖 |
| 3 | **测试本身**：测试从写出来就是绿的，从没检查过任何东西 | [**mutation-check**](https://github.com/hidevinliu/red-green-mode/tree/main/skills/mutation-check)：故意把代码改坏，测试必须变红 | 已发布，在 red-green-mode 里 |
| 4 | **记忆**：每一轮都从零开始，同一个坑反复踩 | 记录循环状态和以往的修法，同类失败再出现时调出来用 | 即将发布 |
| 5 | **汇报**：agent 说做完了，git 记录却对不上 | 把 agent 的每条说法拿去对提交记录、CI 和文件时间，只报对不上的 | 即将发布 |

### 我怎么看用 agent 做开发

- **退出码说了算，不是 agent 说了算。** 模型对自己工作的评价不算证据，真正跑过的验证才算。
- **测试通过不等于做完了。** 测试通过、需求交付、界面和参考图一致，是三道独立的检查，哪一道都不能代替另一道。
- **绝不作弊变绿。** 删测试、放宽断言、把被测逻辑 mock 掉，是自动循环里唯一绝对不能做的事。觉得测试写错了，就停下来问人。
- **流程跟着任务大小走。** 新产品写完整规格，修 bug 写五行方案就够。
- **用最小的正确改动。** 先用项目里已有的，再用标准库，最后才加依赖，而且写明理由。
- **"未核实"也是诚实的回答。** 跑了什么、没跑什么，照实说。工具配好了，不等于检查通过了。
