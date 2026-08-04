---
name: focused-test-generation
description: Generate tests for a small, bounded scope in any programming language or test framework. Use when asked to add, write, or generate tests for a function, method, class, file, or small module in a project that already has a runnable test setup. Identify behavior targets, follow project conventions, run narrow tests immediately, and finish with full-suite validation plus requirement-to-test evidence. Do not use for broad coverage campaigns, test-framework migration, running existing tests only, or standalone test-quality audits.
---

# Focused Test Generation

為小型專案或單一功能範圍補上測試。核心目標是驗證可觀察的行為，不是讓每個檔案都被測到。

## 工作模式與範圍

- 以一次聚焦的 Direct/Focused 工作完成；不要為小範圍測試建立完整的多代理研究、規劃、實作流程。
- 先把範圍限制在一個功能、類別、方法、檔案，或最多三個直接相關的 production 檔案。若需求仍然涵蓋整個專案，先要求使用者指定功能，或明確列出你選擇的第一個切片。
- 除非使用者明確要求，不要建立 `.testagent/`、計畫檔或其他流程產物。
- 不修改 production code 來迎合測試。若程式難以測試，保留問題並回報阻塞原因。

## 流程

### 1. 讀取專案規則與測試入口

先檢查目前專案的 README、貢獻規範、CI 設定、manifest、測試設定與 package scripts。找出：

- 使用的語言、框架與測試 runner。
- 專案既有的測試命名、目錄、fixture、mock/fake、斷言與非同步寫法。
- 最窄的測試指令，以及完整測試、靜態分析或 lint 指令。

優先使用專案已定義的命令，不要自行引入新的測試框架。若找不到可執行的測試入口，先回報缺少的設定，不要假裝測試已完成。

常見線索如下；它們只是偵測提示，不是固定指令：

| 專案線索 | 優先查找 |
| --- | --- |
| `composer.json`、PHPUnit/Pest 設定 | `composer scripts` 與既有 test suite |
| `package.json`、Jest/Vitest/Mocha 設定 | `scripts` 與既有 test pattern |
| `pyproject.toml`、`pytest.ini`、`unittest` | project script、pytest 或 unittest 設定 |
| `go.mod` | package-level `go test` 慣例 |
| `Cargo.toml` | `cargo test` 與 module test 慣例 |
| `pom.xml`、`build.gradle` | Maven/Gradle 的既有 test task |
| `.csproj`、`.sln` | solution/project test runner |

遇到未列出的語言時，沿用同一原則：讀 manifest 與設定，找出該專案自己的 runner，不要把上述命令硬套上去。

### 2. 找出「該測的行為」

把下列來源當成候選訊號，再用需求與程式語意做決定：

- 使用者需求、規格、驗收條件、decision table、invariant 或狀態轉移。
- public/exported entry point、對外 API、CLI、事件 handler、controller、service 或 repository contract。
- 條件分支、邊界值、輸入驗證、資料轉換、狀態變更、錯誤與例外。
- 資料庫、檔案、網路、queue、時間、亂數、第三方服務等外部邊界。
- 金額、權限、安全、資料一致性、idempotency、重試與並行等高風險行為。
- 最近的 git diff、歷史 bug 或需求變更；沒有 git 資料時不阻塞。

用 AST、語言伺服器、搜尋、source/test 配對、複雜度或 coverage 找到的只是「可能要看」的候選，不是「一定已測」的證據。測試目標必須落在可觀察結果，例如回傳值、公開狀態、持久化內容、發出的命令/事件、錯誤型別或對外效應。

優先順序：

1. P0：金錢、權限、安全、資料一致性、idempotency、並行與不可逆副作用。
2. P1：核心商業規則、計算、狀態機、驗證、錯誤處理與外部契約。
3. P2：低風險格式化、簡單 helper、純 wiring；只有在它承擔對外契約時才需要測。

通常跳過純 getter/setter、DTO/資料容器樣板、框架預設行為與沒有決策邏輯的轉接層。

在開始寫測試前，至少閱讀目標 production code 與一個最接近的既有測試。若需求與實作衝突，列出衝突；不要猜測並把猜測寫成測試。

### 3. 建立小型需求—行為清單

把每個明確需求拆成可驗證項目。使用下列欄位即可，不必建立額外文件：

| Requirement | Observable behavior | Scenarios | Test layer/file | Status |
| --- | --- | --- | --- | --- |
| 一條需求 | 使用者能觀察到的結果 | happy path、邊界、錯誤、狀態/副作用 | unit/integration 與目標檔案 | planned/pass/block |

每條需求至少思考：正常案例、重要邊界、無效或失敗輸入，以及必要的狀態或副作用。沒有適用情境就標記為 N/A 並說明原因。

### 4. 依既有慣例寫測試

- 把測試放在現有 runner 會自動發現的位置，採用專案已有的命名與分層。
- 一個測試應表達一個主要行為；同一規則的多組輸入可使用 parameterized/data-driven 形式。
- 使用非退化、能區分錯誤實作的 fixture；不要用剛好讓任何結果都成立的資料。
- 對純邏輯優先寫 deterministic unit test；跨模組契約、資料庫或序列化行為才使用較高層測試。
- 外部系統使用專案既有的 fake、stub 或 mock；避免真實網路、共享環境、牆上時鐘、亂數、sleep、執行順序與未控制的全域狀態。
- 非同步程式必須使用 runner 支援的 await/async 方式，不能只啟動 promise/future 就結束測試。
- 斷言具體結果與重要副作用；不要只斷言「沒有丟錯」、物件存在，或 mock 被呼叫一次就算完成，除非那就是完整契約。

不要為了增加 coverage 寫沒有行為意義的測試，也不要在本工作中修改 production code、降低斷言、跳過失敗測試或改動全域測試設定。

### 5. 立即執行並迭代

1. 先執行最窄的單一測試檔、案例或 package。
2. 若編譯、載入或 runner 發現錯誤，依實際錯誤修正測試；確認 API、import、fixture 與 runner pattern，而不是修改 production code 讓測試通過。
3. 若測試失敗，判斷是測試錯誤、需求與實作不一致，還是 production bug。保留可重現證據；不要把失敗改成 skip。
4. 新增測試通過後，再從專案根目錄執行完整測試 suite。若專案已有 lint、型別檢查或靜態分析，也執行它們；沒有就不要自行增加新工具。

### 6. 做一次小型品質閘門

完成前逐項確認：

- 每條需求都有對應測試，或有明確的 N/A/block 說明。
- 測試真的能區分錯誤結果；做一次 mental pseudo-mutation check：若把邊界、運算子、回傳值或錯誤路徑改錯，測試是否會失敗？
- 已涵蓋重要分支、邊界、錯誤與必要副作用，而非只碰到程式碼。
- 沒有 tautological assertion、只測 mock 互動、未 await 的非同步斷言或環境依賴。
- 先跑窄測試，再跑完整 suite；回報實際命令與結果。

小型專案預設不執行 mutation testing。只有使用者明確要求，或專案已配置原生 mutation 工具且該範圍屬 P0/P1 時，才執行有限的 mutation check。

## 輸出格式

最後用精簡報告交付：

1. 測試了哪些 behavior，以及刻意沒有測哪些低價值樣板。
2. 新增/修改的測試檔案與各自驗證的需求。
3. `narrow test`、`full suite`、`lint/static analysis` 的實際命令與結果。
4. 尚未解決的需求衝突、不可測性或環境阻塞。

使用下列表格保持可追溯性：

| Requirement | Test | Result |
| --- | --- | --- |
| 可引用的需求或驗收條件 | `path/to/test` — 測試案例名稱 | pass/fail/block，附簡短證據 |

若沒有明確需求，標示哪些行為是根據 public contract 推導的，並把假設與風險寫出來。
