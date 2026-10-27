# 全局工作约定

> 复制到对应位置后生效：
> `~/.config/opencode/AGENTS.md`、`~/.claude/CLAUDE.md`、`~/.codex/AGENTS.md`

## 复杂改动走 RePPIT 流程

接手陌生代码库、跨模块/跨前后端改动、需要先定位数据流再决定做法时，加载 `reppit` skill 并按其流程执行，产出 `docs/reppit/<feature>/` 下的 research.md / proposal.md / plan.md。

精简版硬约束（skill 里的完整版优先）：

- 调研阶段只描述现状，不改任何代码。
- 给 2~3 个方案，停下等我选，不要自行开工。
- 计划里每步写明改哪个文件、怎么验证；我确认后再实现。
- 一次只推进一个阶段，验证通过才继续，并回写 plan.md。
- 汇报测试结果必须附实际执行的命令与输出，不说"应该没问题"。
