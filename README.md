# expense

面向 Agent 的项目报销材料整理 Skill：统一发票与配套材料的文件名，并依据随附 Word 母版生成报销内容简要说明。

## 项目级目录

Skill 存放在项目的 `.agents/skills/expense/` 中：

```text
项目根目录/
├─ README.md
└─ .agents/
   └─ skills/
      └─ expense/
         ├─ SKILL.md
         ├─ agents/
         ├─ assets/
         └─ references/
```

将本仓库的 `.agents/skills/expense/` 完整复制到目标项目的同名目录，并保留内部相对路径。

## Agent 使用入口

请先读取 [SKILL.md](.agents/skills/expense/SKILL.md)，再按其中的资源说明加载整理规则与 Word 填写指引。所有资源路径均相对于 Skill 所在目录。

在目标项目中向 Agent 提供以下指令：

```text
请读取本项目的 .agents/skills/expense/SKILL.md，
按其中的流程整理我提供的报销材料。
开始前请先收集我的姓名、项目编号、项目名称和材料所在目录；
多人报销时，请同时确认各张发票的人员归属。
```

支持命名调用的 Agent 环境也可使用 `$expense`。自动发现方式以所用 Agent 的项目级配置为准。

## 所需能力

Agent 需要能够读取本地 PDF 与图片、整理文件、编辑 DOCX，并生成文档预览以逐页检查。环境提供 documents、PDF 等技能时可直接复用；工具和运行时按实际环境选择。

## 整理规则

- 工作区按使用者姓名命名，一个项目对应一个工作区；多人发票汇总为一份说明。
- 发票命名为 `物品名称-姓名-价税合计.pdf`，金额保留两位小数。
- 单张发票价税合计达到或超过 200.00 元时，收集对应的订单截图和付款记录。
- 实物特殊采购的“无京东自营”原因由用户提供。
- 更新说明前，将旧版存入 `历史备份（旧版本，忽略）`。

上述要求来自本 Skill 的既定工作流程，具体项目要求可在使用时明确调整。完整规则见 [整理规则](.agents/skills/expense/references/整理规则.md)。

## 输出结构

```text
用户姓名/
├─ 发票/
├─ 订单截图/
├─ 付款记录/
├─ 历史备份（旧版本，忽略）/
└─ 报销内容简要说明.docx
```

四个目录始终保留，允许为空。正式说明按费用类别和用途汇总，省略人员明细和个人小计，并在明细末尾列出价格总计；总计按发票号码去重后汇总价税合计，金额保留两位小数。

## 随附资源

- [信息采集表](.agents/skills/expense/assets/信息采集表.md)
- [Word 母版](.agents/skills/expense/assets/报销内容简要说明.docx)
- [Word 填写与更新](.agents/skills/expense/references/Word填写与更新.md)

![Word 母版预览](.agents/skills/expense/assets/母版预览.png)

