# 一致性修复设计（2026-03-05）

## 目标
仅修复系统内的字段与路径不一致问题，不新增示例内容，不改变既有工作流语义。

## 范围
1. 统一收件箱状态字段为 `pending -> processed`。
2. 修复 README 截图路径与当前仓库结构不一致问题。
3. 对技能层中的收件箱 frontmatter 给出一致化建议（受只读限制，无法直接改写隐藏目录）。

## 方案对比
### 方案 A（采用）
- 最小补丁，修模板和主文档。
- 优点：风险低、立即可用。
- 缺点：隐藏目录下技能文件若不可写，仍需后续手工同步。

### 方案 B
- 同时重构全部技能和命令文件的状态字典与 frontmatter。
- 优点：一次性彻底统一。
- 缺点：改动面大，超出本次“只修一致性”的最小范围。

## 具体改动
1. `99_系统/模板/Inbox_Template.md`
- `status: captured` 改为 `status: pending`。

2. `AGENTS.md`
- 明确新收件箱条目状态为 `pending`，处理后为 `processed`。

3. `README_CN.md` 与 `README.md`
- 截图路径统一到当前根目录下实际文件：`50_资源/Screenshot.png`。

## 验证
1. 搜索 `status: captured` 应无结果（或仅历史文本，不在模板与规范中）。
2. README 截图路径均指向存在文件。
3. 后续启用 workflow 时，收件箱模板与数据库筛选口径保持一致。

## 已知限制（已解除）
2026-03-05 后续修复中，已在可写权限下完成技能文件同步：
- `.agents/skills/start-my-day/SKILL.md` 已补齐收件箱 frontmatter。
- `.codex/skills` 为指向 `.agents/skills` 的符号链接，已自动保持一致。
