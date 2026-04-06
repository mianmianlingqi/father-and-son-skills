---
name: father-and-son-skills-core
description: "Use when: 需要处理复杂子 skill、脚本化子 skill、通用子 skill 逻辑抽取、模板化生成、资源与脚本组织；作为 Father and Son Skills 的副父 skill。"
---

# Father and Son Skills Core

Father and Son Skills Core 是副父 skill。它不负责具体业务，而是负责通用子 skill 逻辑、脚本化结构、模板复用和复杂 skill 的组织方式。

它的作用是把“子 skill 该怎么长、脚本该放哪里、资源该怎么分层、复用逻辑该怎么写”这些通用问题统一起来，然后再交给 Father and Son Skills 入口 skill 去做路由、草稿和生效控制。

## 它是做什么的

这个 skill 主要做五件事：

- 结构化：定义复杂子 skill 的标准目录结构。
- 复用化：抽出通用子 skill 逻辑，减少每个 child skill 重复写一遍。
- 脚本化：告诉子 skill 的脚本、模板、测试和资源该放在哪里。
- 组织化：把复杂子 skill 拆成可维护的模块。
- 协同化：和 Father and Son Skills 主 skill 配合，完成复杂子 skill 的创建与维护。

## 什么时候用

在下面这些场景使用它：

- 子 skill 需要内置脚本。
- 子 skill 需要模板、资源文件或测试辅助文件。
- 子 skill 的逻辑过于复杂，不适合只写一个纯文本 `SKILL.md`。
- 你要抽取多个子 skill 都能复用的通用规则。
- 你要先定义子 skill 的通用骨架，再回到主 skill 做草稿和载入。

## 什么时候不用

不要在下面这些场景使用它：

- 只是在写一个简单的说明型子 skill。
- 你已经明确知道具体业务实现，不需要通用骨架。
- 你只需要主 skill 的路由和生效控制。

## 通用子 skill 结构

复杂子 skill 的标准目录建议如下：

```text
<child-name>/
├── SKILL.md
├── scripts/
├── references/
├── assets/
└── tests/
```

说明：
- `SKILL.md` 负责说明这个子 skill 做什么、什么时候用、怎么用。
- `scripts/` 放可执行脚本、辅助脚本或自动化脚本。
- `references/` 放说明文档、校验规范、依赖说明。
- `assets/` 放模板、示例、输入输出样本。
- `tests/` 放验证脚本或最小测试样例。

## 通用逻辑沉淀

以下内容适合沉淀到副父 skill 里：

- 子 skill 的命名规则。
- 纯文本 skill 和脚本化 skill 的分界。
- 复杂 skill 的拆分策略。
- 脚本引用方式和相对路径规范。
- 复用模板和子 skill 骨架。
- 子 skill 维护和升级规则。

## 与主 skill 的关系

- 主 skill 负责路由、复用判断、草稿管理和生效控制。
- 副父 skill 负责复杂子 skill 的通用结构和脚本逻辑。
- 复杂子 skill 先经过副父 skill 生成骨架，再回到主 skill 走草稿和 active 流程。

## 一句话原则

主 skill 管流程，副父 skill 管通用结构和脚本化逻辑，复杂子 skill 先抽骨架，再进入草稿和生效流程。
