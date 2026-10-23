# zbhgis.github.io · 归档站

**本仓库已停止更新，站点作为归档入口保留。**

- 站点主页：<https://zbhgis.github.io>
- 新站（持续更新）：<https://www.zbhgis.com>

## 状态说明

| 项目 | 状态 |
|---|---|
| 生成方式 | Gmeek（GitHub Issues → `docs/`） |
| 自动构建 | **已停用**（`Gmeek.yml` 仅保留手动触发） |
| 文章数 | 66 篇（2023–2026） |
| 跳转策略 | 65 篇正文保留 + `rel=canonical` 指向新站；1 篇无对应版本独立归档 |
| 映射表 | [`migration_map.csv`](./migration_map.csv) |

## 维护须知

1. **不要再让 Gmeek 自动构建**。`docs/` 内的横幅、CTA、canonical 均为手工注入，
   workflow 一旦运行会全部覆盖。
2. 如需重新生成，先备份 `docs/`，再手动触发 workflow。
3. 新增或修订内容请到新站 <https://www.zbhgis.com>，本仓库不再更新。
