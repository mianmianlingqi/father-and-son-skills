# Father and Son Skills

这是受控自扩展 skill 的内部工作目录，用来承载草稿和生效两个状态。

## 入口
- 统一入口位于 `.claude/skills/father-and-son-skills/SKILL.md`。
- 这里仅保留内部状态与约定，不作为对外入口。

## 目录约定
- `drafts/`：模型新生成的草稿，只能提议，不能加载。
- `active/`：已批准、可加载的正式能力。

## 文件组织建议

- 子 skill 建议放在各自独立目录中，例如 `drafts/<child-name>/SKILL.md`。
- 晋级到 `active/` 时，保留相同的子目录结构，避免文件名漂移。
- 如果子 skill 需要脚本、模板或引用说明，可以一并放在该子目录下，由对应 `SKILL.md` 引用。
- 如果子 skill 需要内置脚本，建议在子目录下增加 `scripts/`、`references/`、`assets/` 和 `tests/`。
- 复杂子 skill 的通用逻辑先由副父 skill `father-and-son-skills-core` 处理，再进入当前的草稿与生效流程。

## 显式调用和创建

- 用户可以显式点名某个子 skill，系统先去 `active/` 找同名内容。
- 用户可以显式要求创建某个子 skill，系统先在 `drafts/` 建立该子 skill 的草稿。
- 草稿完成后，要询问用户是否要载入生效池。
- 用户确认后，才允许进入 `active/`。
- 如果子 skill 复杂到需要脚本或通用模板，先交给 `father-and-son-skills-core` 生成结构，再回到这里做具体落盘。

## 最小规则
- 运行时只扫描 `active/`。
- `drafts/` 只作为中间态。
- 任何内容进入 `active/`，都必须经过用户确认。

## 复杂子 skill 规则

- 纯文本型子 skill 可以直接按当前规则生成。
- 需要脚本的子 skill 不要只写一个 `SKILL.md`，要把脚本放进 `scripts/`。
- 通用逻辑、目录模板和脚本约定由副父 skill 统一管理。
- 子 skill 复杂度过高时，优先拆成可复用的脚本和说明文件，再进入 active。

## 流转规则

1. 新内容先写入 `drafts/`。
2. 如果用户显式点名某个子 skill，先查 `active/`。
3. 找到则直接调用，找不到则提示未命中。
4. 如果用户要求创建，就继续在 `drafts/` 生成该子 skill；如果 `active/` 已有同名内容，先询问用户是复用、覆盖还是改名后再建。
5. 草稿完成后，询问用户是否要载入生效池。
6. 用户确认后，再进入 `active/`。
7. 如果不通用或用户不同意，就继续留在 `drafts/`。
8. 如果 `active/` 中已有匹配内容，优先复用，不重复创建。
