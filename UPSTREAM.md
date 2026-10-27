# 第三方技能来源

| 技能 | 来源 | 说明 |
| --- | --- | --- |
| `grilling` | [mattpocock/skills](https://github.com/mattpocock/skills) | 按设计树分轮追问，每问附推荐答案；多个 grill 类技能的底层原语 |
| `grill-me` | 同上 | 用户触发入口，调用 `grilling` |
| `tdd` | 同上 | 红-绿-重构，一次一个垂直切片；附 `tests.md`、`mocking.md` |
| `diagnosing-bugs` | 同上 | 硬 bug / 性能回归的纪律化诊断循环；附 HITL 循环脚本 |
| `code-review` | 同上 | Standards + Spec 两轴并行审查 diff |
| `handoff` | 同上 | 把会话压成交接文档写给下一个 agent |

- 获取日期：2026-10-27
- 许可证：MIT，版权归 Matt Pocock，全文见 `licenses/MIT-mattpocock.txt`
- 修改情况：与上游一致，未做修改（按目录原样复制），`agents/openai.yaml` 为上游自带的产品元数据

## 已知差异

`grill-me` 的 `disable-model-invocation`、`handoff` 的 `argument-hint` 是 Claude Code 专有的 frontmatter 字段。Codex 自带的 `quick_validate.py` 会因此报 `unexpected key`（不影响加载）；若某个 agent 严格拒绝未知字段，删掉该行即可，语义损失仅为“该技能不再由模型自动触发”。

## 更新方式

不要手动改这几个目录，直接用官方安装器覆盖：

```bash
npx skills@latest add mattpocock/skills -g -a opencode claude-code codex -y --copy
```

安装后把 `~/.agents/skills/<name>` 重新复制回 `skills/<name>`，确认 diff 后提交。若确实需要本地修改，先提交原样版本，再单独提交改动，方便更新时区分。

## 与 `skills/reppit` 的关系

`reppit` 是主流程骨架，以上 6 个是它各阶段的可选加强项，挂载时机写在 `skills/reppit/SKILL.md` 的「可选子技能」小节。两者冲突时以 `reppit` 的硬规则为准。
