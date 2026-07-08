# ZCode WeChat → Obsidian 自动存档系统

将微信公众号文章自动抓取、分析、结构化存档到 Obsidian 知识库，包含双链标注和周记汇总。

## 功能

| 功能 | 触发方式 | 说明 |
|------|---------|------|
| **微信文章存档** | 发送 `mp.weixin.qq.com/s/` 链接 | 自动抓取原文→分析图片→生成结构化笔记→保存 Obsidian |
| **截图存档** | 发送文章截图 | OCR 提取文字→生成笔记（需 macOS） |
| **周记生成** | "生成周记" / "weekly review" | 汇总本周所有笔记→主题归类→跨文章洞察 |
| **双链标注** | 自动 | 笔记中自动添加 `[[]]` Obsidian 双向链接 |
| **学习计划** | 手动 | 基于阅读历史生成半导体/AI 行业学习路线 |

## 安装

### 1. 前置条件

- ZCode CLI 环境
- macOS（截图 OCR 依赖 Vision 框架）
- Obsidian
- 已配置 Obsidian 库路径

### 2. 配置

将 `skills/` 目录下的文件复制到 ZCode skills 路径：

```bash
cp skills/*.md ~/.zcode/skills/
```

编辑 `CLAUDE.md`，将 Obsidian 库路径改为你自己的路径：

```markdown
## Obsidian 库路径
`/你的/Obsidian/库/路径/`
```

### 3. 依赖工具

| 工具 | 用途 | 安装 |
|------|------|------|
| webReader | 抓取微信文章内容 | ZCode 内置 |
| analyze_image | 分析文章图片 | ZCode 内置 |
| macOS Vision | OCR 截图文字 | macOS 系统自带 |
| Python 3 | HTML 抓取和数据处理 | 系统自带 |

## 笔记格式

生成的笔记遵循统一模板：

```markdown
---
title: "文章标题"
source: "原文URL"
author: "公众号名称"
date: YYYY-MM-DD
tags: [标签1, 标签2, ...]
created: YYYY-MM-DD
---

## 摘要
## 逐图分析
## 关键发现
## 一句话总结
```

## 周记格式

```markdown
---
type: weekly-review
week: W{周数}
date_range: 周一 ~ 周日
articles: N
---

## 本周阅读清单
## 主题深入
## 跨文章洞察
## 本周核心概念
## 本周反思
```

## 技能文件

- [wechat](skills/wechat.md) — 微信文章自动存档
- [weekly-review](skills/weekly-review.md) — 周记汇总生成

## 示例笔记图谱

```
半导体/
├── 海光信息-半导体-2026-06-09.md
├── 英特尔vs海光-半导体投资-2026-06-15.md
├── DrMOS电源-半导体-2026-06-15.md
├── 先进封装/
│   ├── 应用材料-异构集成-半导体-2026-06-15.md
│   ├── HBF封装设备-半导体-2026-06-15.md
│   └── 美光封装讲义-半导体-2026-07-06.md
├── 存储/
│   ├── 英伟达VR200-HBM-半导体-2026-06-15.md
│   ├── DRAM砍半-存储-2026-06-17.md
│   └── 英伟达CMX-NAND-存储-2026-07-07.md
└── 光互联/
    ├── 光互联NPO-CPO-XPO-网络技术-2026-06-15.md
    └── 硅光子III-V-半导体-2026-07-06.md

周记/
├── 周记-W24-2026.md
└── 周记-W25-2026.md

学习计划/
└── 半导体学习计划-2026H2.md
```

## 注意事项

- 每次存档前自动获取系统日期，不会日期错乱
- 支持微信文章链接和截图两种输入
- 笔记间通过 `[[]]` 自动形成知识图谱
- 周记汇总所有文档（微信文章 + 个人笔记）
