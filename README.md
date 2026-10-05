<a id="en"></a>

## Hi, I'm Devin

[English](#en) · [中文](#zh)

I write tools that check AI coding agents' work before I accept it.

I use AI agents for much of my development work: internal tools, data pipelines, knowledge bases,
websites. The part that needed tooling was checking whether an agent's "done" was actually done.
When I ran into a specific way it wasn't, I wrote a check for it that returns an exit code. Those
checks are below.

### What I'm interested in

- **AI-assisted programming:** how coding agents plan, verify and hand work off, and how to keep long
  or parallel agent runs under control.
- **Product architecture:** turning a vague idea into a clear structure before code is written:
  modules, data models, flows and acceptance criteria.
- **Engineering governance:** keeping a codebase and its rules consistent over time: one source of
  truth, written acceptance criteria, and checks that block a bad change rather than only warn about it.
- **Agent algorithms:** the decision logic in an agent loop, such as detecting a stalled loop,
  choosing which files an agent should read, and reusing how a similar failure was fixed before.

### Projects

| What it checks | Project | Status |
|---|---|---|
| The spec: is the request clear enough to build and verify? | [**AI-PRD-Devin**](https://github.com/hidevinliu/AI-PRD-Devin), a fork of [qiaomu-ai-prd](https://github.com/joeseesun/qiaomu-ai-prd). Writes a full PRD, a short spec or a short plan depending on task size, and can output an acceptance contract for red-green-mode. | Released |
| The tests: did the agent pass them by editing them? | [**red-green-mode**](https://github.com/hidevinliu/red-green-mode) scans the diff for skipped tests, deleted assertions and suppressed errors. It blocks all 55 cheat techniques in my test set, and in its PR-review mode it blocks 3.3% of 630 merged pull requests. Method and data are in [`bench/`](https://github.com/hidevinliu/red-green-mode/tree/main/bench). It also flags fixes that only change behaviour at the tested inputs: 0 of 112 correct fixes flagged, 26 of 38 overfit ones caught on QuixBugs. | Released |
| The test itself: does it fail when the code breaks? | [**mutation-check**](https://github.com/hidevinliu/red-green-mode/tree/main/skills/mutation-check) breaks the code on purpose and checks that the test goes red. Part of red-green-mode. | Released |
| Loop memory, and checking an agent's "done" against git history | — | In progress, not released |

### How I work with agents

- A passing check is evidence. An agent saying it's done is not.
- Tests passing, the spec being delivered and the UI matching the reference are three separate checks.
- Don't delete or weaken tests to get a pass. If a test looks wrong, stop and ask.
- Size the process to the task: a full spec for a new product, a few lines for a bug fix.
- Use existing code and the standard library before adding a dependency.
- Report what was actually run, and mark the rest as unverified.

---

<a id="zh"></a>

## 你好，我是 Devin

[English](#en) · [中文](#zh)

我写一些工具，用来在接受 AI 编程 agent 的工作之前先检查它。

我的开发工作很多交给 AI agent 做：内部工具、数据管道、知识库、网站。真正需要工具的地方，是判断 agent 说的"做完了"是不是真的做完了。每遇到一种具体的"没做完"，我就为它写一道检查，结果用退出码表示。下面就是这些检查。

### 我感兴趣的方向

- **AI 编程**：编程 agent 怎么规划、验证、交接工作，以及长时间运行或多个并行时怎么不失控。
- **产品架构梳理**：在写代码之前，把模糊的想法理成清晰的结构：模块、数据模型、流程和验收标准。
- **工程化治理**：让代码库和规则长期保持一致：同一件事只有一个权威来源，验收标准写下来，检查遇到坏改动直接拦下，而不只是提醒。
- **Agent 相关算法**：agent 循环里的决策逻辑，比如判断循环是否卡住、挑出 agent 该读的文件、复用以前同类失败的修法。

### 项目

| 检查什么 | 项目 | 状态 |
|---|---|---|
| 需求：要求清楚到能做、能验收吗？ | [**AI-PRD-Devin**](https://github.com/hidevinliu/AI-PRD-Devin)，基于 [qiaomu-ai-prd](https://github.com/joeseesun/qiaomu-ai-prd) 改的。按任务大小写完整 PRD、短规格或几行方案，可以产出给 red-green-mode 用的验收契约。 | 已发布 |
| 测试：agent 是不是靠改测试过关的？ | [**red-green-mode**](https://github.com/hidevinliu/red-green-mode)，扫描改动，找出被跳过的测试、被删的断言、被屏蔽的报错。我整理的 55 种作弊手法全部能拦下；审 PR 模式下，在 630 个已合并的 PR 中拦了 3.3%。方法和数据在 [`bench/`](https://github.com/hidevinliu/red-green-mode/tree/main/bench)。也能识别"只在被测输入上改变行为"的修复：在 QuixBugs 上，112 个正确修复误报 0 个，38 个过拟合补丁抓到 26 个。 | 已发布 |
| 测试本身：代码坏了它会失败吗？ | [**mutation-check**](https://github.com/hidevinliu/red-green-mode/tree/main/skills/mutation-check)，故意把代码改坏，检查测试会不会变红。属于 red-green-mode 的一部分。 | 已发布 |
| 循环记忆，以及拿 git 记录核对 agent 说的"做完了" | — | 进行中，未发布 |

### 我和 agent 一起工作的原则

- 检查通过才算证据，agent 说做完了不算。
- 测试通过、需求交付、界面和参考图一致，是三道独立的检查。
- 不靠删测试、放宽测试来过关。觉得测试写错了，就停下来问。
- 流程跟着任务大小走：新产品写完整规格，修 bug 写几行就够。
- 先用已有的代码和标准库，最后才加依赖。
- 只汇报实际跑过的，其余的标"未核实"。
