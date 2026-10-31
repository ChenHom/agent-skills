# Agent Skills

自建、可跨專案使用的 Agent Skills、MCP 整合與共用元件。每個 Skill 都有明確入口、適用情境與執行指引，供支援 Agent Skills 的工具使用。

這個 repository 只存放可被 Agent 或工具直接使用、安裝、驗證及版本控制的執行資產。一般技術筆記、研究文章與操作紀錄統一放在 [ChenHom/knowledge](https://github.com/ChenHom/knowledge)。

## 儲存庫結構

```text
skills/       Agent Skill 套件，每個 Skill 各有獨立目錄
mcp/          MCP server、受控 wrapper、schema 與整合範例
shared/       供多個 Skill 或 MCP 共用的規則、schema 與測試資料
```

## 可用 Skills

| Skill | 用途 |
|---|---|
| [`clear-writing`](skills/clear-writing/) | 借用 ASD-STE100 清晰原則，撰寫一般說明、報告、教學與 commit／PR，保留語意與創作文風 |
| [`external-resource-safety`](skills/external-resource-safety/) | 檢查外部資源的間接提示詞注入、隱藏指令、擴權與來源污染風險 |
| [`shioaji`](skills/shioaji/) | 永豐 Shioaji API 的行情、委託、帳務與串流操作 |
| [`focused-test-generation`](skills/focused-test-generation/) | 小型專案、跨語言的聚焦式測試生成與需求—測試結果追蹤 |
| [`resource-aware-development`](skills/resource-aware-development/) | 日常功能開發與效能改善兼顧資源效率、可靠性、實測與維護成本 |

## 如何使用

1. 從上表選擇符合任務的 Skill，閱讀其 `SKILL.md` 的觸發條件及範圍。
2. 依所用 Agent 工具的安裝方式，將整個 Skill 目錄安裝到該工具可讀取的 Skill 路徑；同時保留它引用的 `references/` 等檔案。
3. 依工具的載入方式啟用或重新載入，並在需要時明確指定 Skill 名稱。安裝路徑、發現機制與權限由各工具決定。
4. 在適用的任務中依 Skill 指引執行；遇到高風險或對外操作，仍須遵守使用者授權與環境規則。

每個 Skill 的 `SKILL.md` 是主要入口；`evals/` 如有提供，用來檢查預期行為，不代表案例已自動執行或通過。

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

## Skill 套件結構

```text
skills/<skill-name>/
├── SKILL.md
├── references/
├── scripts/
├── assets/
└── evals/
```

只建立實際需要的目錄。`SKILL.md` 是主要入口；大型說明拆到 `references/`，可重複且必須穩定執行的動作才寫成 `scripts/`。

## 維護原則

- 目錄與檔名使用小寫英文 `kebab-case`
- Skill 的 `name` 必須與目錄名稱一致
- 說明 Skill 的觸發條件、禁止範圍與輸出契約
- 高風險動作必須有權限檢查與人工核准點
- 行為變更同步更新 `evals/`
- 給人閱讀的完整背景知識保留在 `knowledge`，此處只保留執行所需內容
