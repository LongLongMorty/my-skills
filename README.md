# my-skills

给编码 agent 用的技能包：一套**接手陌生代码库**的流程（RePPIT），加上它各阶段的可选加强技能。适用于 OpenCode、Claude Code、Codex 等支持 `SKILL.md` 的 agent。

## 目录结构

```
my-skills/
├── AGENTS.md                     # 全局工作约定（核心规则，复制到 agent 的全局指令文件）
├── UPSTREAM.md                   # 第三方技能的来源、修改说明、更新方式
├── licenses/
│   └── MIT-mattpocock.txt        # 第三方技能的 MIT 许可证全文
└── skills/
    ├── reppit/                   # 主流程：Research → Propose → Plan → Implement → Test
    │   ├── SKILL.md
    │   └── assets/               # research.md / proposal.md / plan.md 三份产出物模板
    ├── grilling/  grill-me/      # 追问（第三方）
    ├── tdd/                      # 红-绿-重构（第三方）
    ├── diagnosing-bugs/          # 诊断循环（第三方）
    ├── code-review/              # 两轴审查（第三方）
    └── handoff/                  # 会话交接（第三方）
```

## 技能一览

| 技能 | 调用方 | 什么时候用 |
| --- | --- | --- |
| `reppit` | 模型按需 / 手动 | 接手陌生库、跨模块或跨前后端改动，需要先调研再动手 |
| `grilling` / `grill-me` | 模型 / 用户 | 需求或方案没问清，需要分轮追问到没有隐含假设 |
| `tdd` | 模型 | 写功能或修 bug，要求红-绿-重构、一次一个垂直切片 |
| `diagnosing-bugs` | 模型 | 测试反复变红、原因不明，或性能回归 |
| `code-review` | 模型 | 提交前审 diff：仓库规范 + 原需求两轴 |
| `handoff` | 用户 | 上下文将满，需要交接给下一个会话 |

`reppit` 是主骨架，其余 6 个是它各阶段的可选加强项，映射关系写在 `skills/reppit/SKILL.md` 的「可选子技能」小节。

## 安装

### 方式一：用 skills 安装器

```bash
npx skills@latest add <your-github-user>/my-skills -g -a opencode claude-code codex -y --copy
```

先确认能被发现（应输出 `Found 7 skills`）：

```bash
npx skills@latest add <your-github-user>/my-skills -l
```

### 方式二：手动复制

| 工具 | Skill 目录 | 全局指令文件 |
| --- | --- | --- |
| OpenCode | `~/.config/opencode/skills/<name>/SKILL.md` | `~/.config/opencode/AGENTS.md` |
| Claude Code | `~/.claude/skills/<name>/SKILL.md` | `~/.claude/CLAUDE.md` |
| Codex CLI | `~/.codex/skills/<name>/SKILL.md` | `~/.codex/AGENTS.md` |
| 通用（多个 agent 共享） | `~/.agents/skills/<name>/SKILL.md` | — |

把 `skills/<name>` 整个目录复制过去（`assets/`、`scripts/`、`agents/` 一并带上），再把根目录 `AGENTS.md` 的内容复制到上表的全局指令文件。

### 方式三：当上游更新时

第三方部分建议直接用官方安装器覆盖，不要手改；见 `UPSTREAM.md`。

## 使用

1. 重启 agent（配置与技能在启动时加载）。
2. 遇到复杂改动说「按 RePPIT 调研一下这个库」，或直接让 agent 调用对应技能。
3. 产出物默认写到仓库的 `docs/reppit/<feature>/`，项目已有约定时跟随项目约定。

## 约定要点

- 调研只描述现状，不动代码。
- 方案给 2~3 个并停下等人选。
- 计划每步写明改哪个文件、怎么验证，确认后才实现。
- 一次只推进一个阶段，验证通过再继续，并回写 plan.md。
- 测试结论必须附实际命令与输出。

## 许可证与致谢

- `skills/reppit`、`AGENTS.md`、`README.md`、`UPSTREAM.md`：作者自有内容（如需开源请自行添加 LICENSE）。
- `skills/` 下属于 Matt Pocock 的 6 个技能：MIT，版权归 Matt Pocock，原样引用，许可证全文见 `licenses/MIT-mattpocock.txt`。
