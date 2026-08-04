# Agent Skills

自建 Agent Skills、MCP integrations 與可跨專案共用的 Agent 元件。

這個 repository 只存放可被 Agent 或工具直接使用、安裝、驗證及版本控制的執行資產。一般技術筆記、研究文章與操作紀錄統一放在 [ChenHom/knowledge](https://github.com/ChenHom/knowledge)。

## 目錄

```text
skills/       Agent Skill 套件
mcp/          MCP server、wrapper、schema 與整合範例
shared/       多個 Skill 或 MCP 共用的規則、schema 與測試資料
```

## Skills

| Skill | 用途 |
|---|---|
| [`external-resource-safety`](skills/external-resource-safety/) | 檢查外部資源的間接提示詞注入、隱藏指令、擴權與來源污染風險 |
| [`shioaji`](skills/shioaji/) | 永豐 Shioaji API 的行情、委託、帳務與串流操作 |
| [`focused-test-generation`](skills/focused-test-generation/) | 小型專案、跨語言的聚焦式測試生成與需求—測試結果追蹤 |

## 收錄規則

可以放入：

- 完整 Skill 套件與 `SKILL.md`
- Skill 所需的 `references/`、`scripts/`、`assets/`、`evals/`
- MCP server、受控 CLI wrapper、tool schema 與整合範例
- 多個 Agent 元件共用的 schema、測試案例與安全規則

不要放入：

- 一般技術筆記或文章摘要
- 尚未整理的聊天內容
- 投資研究與個人操作紀錄
- Token、憑證、私鑰或正式環境設定
- 只供人閱讀、無執行用途的參考文章

## Skill 基本結構

```text
skills/<skill-name>/
├── SKILL.md
├── references/
├── scripts/
├── assets/
└── evals/
```

只建立實際需要的目錄。`SKILL.md` 是唯一入口；大型說明拆到 `references/`，可重複且必須穩定執行的動作才寫成 `scripts/`。

## 維護原則

- 目錄與檔名使用小寫英文 `kebab-case`
- Skill 的 `name` 必須與目錄名稱一致
- 說明 Skill 的觸發條件、禁止範圍與輸出契約
- 高風險動作必須有權限檢查與人工核准點
- 行為變更同步更新 `evals/`
- 給人閱讀的完整背景知識保留在 `knowledge`，此處只保留執行所需內容
