# no-ai-slop

> House rules for AI coding agents.  
> 给 AI 编码代理的家规：杀掉 slop。

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

AI slop 指 AI 批量生成、形式完整、实质凑数的内容。它有三种常见形态：套话文风、文档里的功能尸体、代码里的防御仪式。这个仓库是一份可直接复用的 `AGENTS.md`，把它们写成可执行的 Never 规则和可验证的自查清单。

## 三种 slop

| 形态 | 典型表现 | 本仓库的约束 |
|---|---|---|
| 套话文风 | 每段都是"不是 A，而是 B"；填充词堆节奏 | 禁止该句式及其变体，除非确需纠正误解 |
| 文档尸体 | 功能删了，描述还在，补一句"已废弃" | 已移除功能整段删除；否定句只允许出现在 changelog |
| 防御仪式 | 无必要 `from __future__`；包一切的 `try/except`；死代码注释 | 钉死目标版本；禁止仪式性兼容和防御 |

三种形态的共同点：模型倾向在旧内容上打补丁，不敢直接删、直接改。规则的目标就是把"直接删、直接说、按目标版本写"钉死。

## 快速开始

把 [`AGENTS.md`](./AGENTS.md) 复制到你的项目根目录。

```bash
curl -O https://raw.githubusercontent.com/qwqzy/no-ai-slop/main/AGENTS.md
```

- **Claude Code**：在 `CLAUDE.md` 首行写 `@AGENTS.md`，避免维护两份。
- **Cursor / Codex / 其他支持 AGENTS.md 的工具**：直接识别，无需配置。
- **不支持 AGENTS.md 的工具**：把内容粘进 system prompt 或项目规则文件。

## 文件结构

```
AGENTS.md      # 规则本体，约 50 行，每次会话自动加载
README.md
LICENSE
```

规则本体刻意保持精简。每次会话都加载的内容，每多一行就多稀释一分注意力。项目专属的构建命令、目录约定，建议另建文件按需引用，不要堆进 `AGENTS.md`。

## 规则概览

- **语言与文风**：直接陈述；禁止"不是……而是……"及其变体；禁用填充词。
- **文档纪律**：文档描述"现在是什么"；已移除功能直接删除；否定句仅限 changelog 和迁移说明。
- **Python 代码**：目标 3.12；禁止无必要 `from __future__`；禁止用 `except Exception` 包住整段逻辑；删除死代码，不写兼容层。
- **输出与自查**：交付前跑五步检查——搜句式、搜否定句、查 `from __future__`、查 `try/except`、查旧代码残留。

完整规则见 [`AGENTS.md`](./AGENTS.md)。

## 为什么只放 AGENTS.md

Skill 承载可调用的能力，人格和通用约束应该始终在场。文风纪律、文档纪律、代码纪律属于每次任务都要生效的家规，放 `AGENTS.md`；"审校文档分几步""代码审查逐项查什么"这类流程，放 Skill 按需展开。两者分工，别混。

## 自定义

`AGENTS.md` 是普通 Markdown，直接改。两条建议：

1. **只写能改变行为的规则。** "请写高质量代码"不产生约束，删掉。
2. **控制长度。** 建议 60–100 行以内。流程性、任务特定的检查清单放 Skill 或独立文档。


## License

[MIT](./LICENSE)
