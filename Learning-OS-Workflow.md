# Learning OS｜個人操作工作流

> 這是一套把「計畫、執行、學習、正式作品、回顧」分開管理的系統。  
> 核心原則：**Planner 管執行；Work Log 管證據；Vault 管可長期重用的知識。**

---

## 1. 三個 HTML 各自負責什麼

| 工具 | 它回答的問題 | 應該放什麼 | 不要放什麼 |
|---|---|---|---|
| **Weekly Planner** | 這週何時做什麼？ | Weekly Focus、Top 3 Outcomes、Learn / Practice / Work / Review 時段、指定資源、預期輸出、CMMU／語言／工作／生活安排、Weekly Review | 完整 Assignment Brief、長期能力證據、知識百科、每個細碎研究動作 |
| **Knowledge Vault** | 哪些內容值得以後再找、再想、再用？ | Knowledge Note、Concept、Thinking、Language、Idea、Source、open questions、retrieval 狀態，以及與正式作品的連結 | 行程、待辦、聊天流水帳、普通練習答案、無重用價值的隨機資訊、performance review 原文 |
| **Probation Work Log** | 我被正式交付什麼、交出什麼、表現如何？ | 正式 Assignment Brief、submission、Manager Review、revision、final result、strength／skill gap／capability evidence | 日曆、學習時數、日記、普通 Learn／Practice、每週都硬建一份 assignment |

快速判斷：

- 有「何時做」→ **Planner**
- 有「以後值得重用／複習」→ **Vault**
- 有「正式交付＋獨立完成＋會被評估」→ **Work Log**
- 同一件事可跨工具，但只放各自需要的部分。例如：Planner 只排 `W04-A01` 的工作時段；Work Log 保存完整 brief 與評語；Vault 保存從該作品萃取出的概念，並連回 `W04-A01`。

---

## 2. 每週完整生命週期

### A. 週初：先討論，再產生計畫

1. 向 AI 提供本週 reality：
   - CMMU 課程、作業、考試或簡報
   - 家教／工作／特殊活動
   - 上週未完成事項與 Weekly Review
   - 精力、健康、時間限制
   - Work Log 中最新 feedback、反覆出現的 skill gap
2. 與 AI 確定：Weekly Focus、Top 3 Outcomes、能力重點、Learn → Practice → Work → Review 順序，以及合理工作量。
3. 要求 AI 先選好真正會使用的教材與來源；不要把「找資源」留成另一個待辦。
4. 計畫定案後，才請 AI 依 Planner 內建 prompt 輸出可匯入 JSON。
5. 在 Planner 的「資料 → Plan Update」貼上 JSON，先按**預覽合併**，確認後才合併。

> Planner 日常更新是 merge：沒提供的欄位會保留；省略不等於刪除。要刪 block，必須在 JSON 明確使用 `deleteBlockIds`。

### B. 每日：照 Phase 執行，不把所有活動都記錄

- **Learn**：Teaching、assigned material、重要概念。
- **Practice**：worked example、guided practice、較獨立練習。
- **Work**：只有正式作品才帶 Assignment ID；一般練習仍留在 Planner。
- **Review**：延遲回想、隔日 retrieval、修正與反思。

當天只需要：完成 Planner block、勾選完成、必要時調整時間。不要為了「留下紀錄」而製造行政工作。

### C. 學習後：只把 durable knowledge 收進 Vault

值得存的例子：

- 能反覆使用的概念、定義、區別、框架或公式
- 被修正的重要 misconception
- 自己的觀點如何改變，以及尚未解決的問題
- 可主動使用的 English／Thai expression
- 值得保留 provenance、限制與適用範圍的來源
- 未證實但值得探索的 idea

操作：

1. 在 Vault 首頁 scratchpad 貼入原始內容。
2. 使用 **Copy Capture Prompt + Text**，一起貼給 AI。
3. 把 AI 回傳的 operations JSON 貼入 Vault。
4. 先 **Preview**，再送進 **Inbox**。
5. 在 Inbox 對每筆建議做 Accept／Edit／Retarget／Discard；有 duplicate 時優先合併既有 object。

AI 只能提出 create、update、append、link、unlink、archive，**不能永久刪除**。一般清理用 Archive。只有本人進入 object 的 Edit，經兩次確認並輸入 `DELETE`，才能永久刪除；相關 review record 也會一併清除。

### D. 正式 Assignment gate：不是每週都要建 Work Log

只有同時符合以下條件，才建立正式 Assignment：

- 已明確指定為 formal evidence
- 有清楚且有邊界的 brief 與 deliverable
- 有合理 time budget
- 需要有意義的獨立判斷
- 會有 manager review／assessment

Teaching、教材閱讀、worked example、guided practice、一般 independent practice、retrieval、learning investigation 或普通 CMMU 活動，預設都**不進 Work Log**。整個 90 天以少量、逐步變難的正式作品加 Capstone 為主，數量不是 KPI。

### E. 正式作品：從 Assigned 到 Passed

1. AI 建立 Assignment Merge JSON：`Assigned`。
2. 在 Work Log 的 **AI Merge Import** 貼上，先 Preview，再 Confirm Merge。
3. 開始實作後，只在有意義的狀態改變時更新：`In Progress` → `Submitted` → `Needs Rework`／`Passed`。
4. 提交作品給 AI review 時，同時附上 Assignment brief、submission／檔案與 Work Log operating prompt；要求 AI 評估並在最後附最小必要的 Merge JSON。
5. 本人回報完成日期、實際做法、檔案位置與真實 reflection；AI 不得捏造這些 reality。
6. 修訂與完成後，再把真正可重用的概念、方法、語言或 thinking change 用 **Work Log → Vault** prompt 萃取到 Vault。不要把整份 performance log 複製過去。

Work Log 更新規則：同一 ID 更新同一筆；省略欄位＝保留；`null`＝明確清除；未知資料不要填空字串。

### F. 週末：Review → 調整 → Consolidate

1. 在 Planner 的 Weekly Review 簡短填寫：
   - closed-book 真正能說出的內容
   - 最大阻力／一直拖的事
   - CMMU 可整合內容與 workload
   - English／Thai 實際輸出
   - Research／Evidence 的判斷與缺口
   - delayed／next-day retrieval 結果
   - Career／Business 發現
   - 下週要 reteach、練習或調整什麼
2. 按「複製給 ChatGPT」，下週規劃時與其他 context 一起提供。
3. 在 Vault 使用 **Weekly Consolidation**：合併重複、補 link、archive 低價值內容、安排 retrieval；不要只是不斷新增。
4. 檢查 Vault Review Queue：先自己 recall，再用 **Retrieval Review** prompt 請 AI 出題、判斷與補教。

---

## 3. 三個 HTML 的內建 Prompt 怎麼用

### Weekly Planner：Planner Prompt

位置：**資料 → Planner Prompt → 複製規劃指令**。

用途是讓 AI 依既定學習架構與 JSON 規格排週計畫。最穩定的用法是：

1. 先把相關 `.md` 加入同一個 Project／對話。
2. 貼 Planner Prompt。
3. 再貼「最新 reality＋上週 Review＋Work Log 摘要」。
4. 先討論，明確說「計畫定案」後才要求 JSON。
5. AI 回傳 JSON 後，在 HTML 先 preview，不要盲目匯入。

### Knowledge Vault：Capture Router 與 Prompt Library

| Prompt | 何時用 |
|---|---|
| **Vault Capture Router** | 不確定內容值不值得存、或該進哪一類時；日常預設入口 |
| **Screenshot → Vault** | 從截圖抽取 durable knowledge；不是全文 OCR |
| **Learning Session → Vault** | 一次教學／練習結束後萃取概念、誤解、問題與語言 |
| **Single Q&A → Vault** | 保存一個有長期價值的問答，避免整段聊天入庫 |
| **Language Capture** | 收 reusable English／Thai，並保留實際使用情境 |
| **Thinking / Idea Router** | 區分已形成的判斷、待驗證假設與純 idea |
| **Source / Reading Capture** | 保存來源、資料期間、地域／樣本、限制，以及能／不能支持什麼 |
| **Weekly Consolidation** | 每週合併、archive、補連結與排 retrieval |
| **Retrieval Review** | 先 recall，再由 AI 檢查、追問、補教 |
| **Merge / Duplicate Cleanup** | Vault 變碎、同題多筆時整理；保留歷史，不任意刪除 |
| **Work Log → Vault** | 從正式作品抽取知識；不搬運 performance record |

所有 Vault prompt 的正確終點都是 **operations JSON → Preview → Inbox → 人工核准**。AI 是提案者，不是資料庫的最終決策者。

### Probation Work Log：AI Operating Prompt

位置：**AI / Data** 內的 operating prompt／contract。

使用情境：

- 判斷某任務能否通過 Formal-Work Gate
- 建立正式 Assignment brief
- 把自然語言進度轉成最小 Merge JSON
- 審查 submission、記錄 manager feedback／revision／capability evidence
- 完成後更新 final result

每次不用把整個 Work Log 重貼給 AI；提供本次相關 Assignment 的最新紀錄即可。AI 回傳後仍要 preview，特別檢查它有沒有覆蓋本人 reality 或杜撰 reflection。

---

## 4. `.md` 與 HTML 要怎麼一起餵給 AI

HTML 是本機操作介面與資料庫；`.md` 是讓 AI 理解制度與長期背景的 context。AI 通常不會自動看到瀏覽器 localStorage 裡的最新內容，所以必須主動貼出／匯出與本次任務相關的資料。

| `.md` 文件 | 提供時機 | 功能 |
|---|---|---|
| `Abby — Career & Learning Master Context.md` | 新對話、方向／能力假設相關任務 | 我是誰、職涯假設、baseline、限制、學習原則 |
| `Abby-90-Day-Probation-Workflow.md` | 規劃、Assignment、review 或跨工具操作 | 正式 workflow、角色邊界、weekly loop |
| `Abby-90-Day-Probation-Prompt-Manager.md` | 希望 AI 穩定扮演 Planner／Coach／Boss 時 | Project instruction、mode、JSON 與評估原則 |
| `Learning-OS-Workflow.md` | 自己查操作，或新 AI 需要快速了解整套系統時 | 本份精簡使用手冊 |

### 最小 context 原則

不要每次把所有檔案和三個完整資料庫全塞給 AI。依任務提供最小充分組合：

- **排下週**：Master Context（新對話才需要）＋Workflow／Prompt Manager＋Planner Prompt＋上週 Review＋最新 Work Log evidence＋本週 reality。
- **上課／練習**：相關學習目標＋教材／來源＋Coach mode；結束後再用 Vault Learning Session prompt。
- **建立正式作業**：Roadmap／本週能力目標＋相關 skill gap／strength＋Work Log operating prompt。
- **審查作品**：Assignment 最新紀錄＋submission／附件＋評估要求＋Work Log operating prompt。
- **收知識**：選定的 Vault prompt＋原始內容；若要 update／link，另提供相關 Vault object 的 ID 與現有內容。
- **週回顧**：Planner Review＋本週 completion reality＋Work Log 新證據＋需要 consolidation 的 Vault objects。

若 AI 工具有 Project files／附件功能，可把穩定 `.md` 放在 Project；每次訊息只補最新 reality。若只能貼文字，優先貼 relevant sections，不必貼整份舊對話。

---

## 5. 可直接套用的 feed 範例

### 範例 1｜週初規劃

```text
請使用 Planner mode。附件／context 有：
1. Master Context
2. 90-Day Workflow
3. Prompt Manager
4. Planner 內建 prompt

最新 reality：
- 上週 Review：〔貼 Planner 複製內容〕
- Work Log evidence：〔貼本週相關 strengths / gaps / status〕
- 本週 CMMU／工作／生活限制：〔列出〕
- 未完成事項：〔列出〕

先和我討論 Weekly Focus、Top 3 Outcomes、Learn → Practice → Work → Review
與 workload；現在不要產 JSON。計畫定案後我會再請你輸出 Planner JSON。
```

### 範例 2｜學習後收進 Vault

```text
〔貼 Vault 的 Learning Session → Vault prompt〕

本次 session 原始內容：
〔貼自己的理解、被糾正的誤解、open questions、可重用英文與來源〕

若無法知道既有 Vault ID，不要捏造；用清楚名稱提出 create。
最後只回傳 Vault-compatible operations JSON。
```

### 範例 3｜正式作品 review

```text
請使用 Boss / Manager mode；不要先救我或重寫答案。
〔貼 Work Log AI Operating Prompt〕
〔貼 W04-A01 最新 brief 與狀態〕
〔附上 submission／supporting files〕

請依 brief 評估：先指出有證據的 strengths、reasoning/evidence/communication issues、
是否需要 revision，以及 status。不要捏造我的 reflection。
最後附上只含本次需變更欄位的 Work Log Merge JSON。
```

### 範例 4｜Work Log 完成後回流 Vault

```text
〔貼 Vault 的 Work Log → Vault prompt〕
正式作品 ID：W04-A01
可供萃取內容：〔貼 final output、manager feedback、真正學到的方法／概念〕
現有相關 Vault objects：〔提供 ID＋摘要；沒有就說沒有〕

只保存可重用的 knowledge / concept / thinking / language / source，
並 link 到 W04-A01；不要複製 performance review。
```

---

## 6. 備份與安全習慣

三個 HTML 的資料主要存在目前瀏覽器的 localStorage。**搬動 HTML、換瀏覽器／裝置、使用不同 profile、清除網站資料或瀏覽器資料，都可能讓原資料看似消失。**

建議節奏：

- 每週 Review 完成後：三個工具各做一次 **Full Backup JSON**。
- 正式 Assignment 提交／完成後：立刻備份 Work Log。
- 大量 Vault consolidation、手動永久刪除或匯入前：先備份 Vault。
- 大幅重排週計畫或匯入前：先匯出 Planner 本週 JSON；月底再保留 Full Backup。
- 備份檔以日期分類，例如 `2026-09-27/Planner.json`、`Vault.json`、`Work-Log.json`。

注意：

- Full Backup import 通常會**取代目前資料**，匯入前先再備份一次。
- AI 日常更新走 Merge Import；不要拿 Full Backup import 當日常更新。
- 所有 AI JSON 都先 Preview，再 Confirm。
- Archive 是正常清理方式；永久刪除只用於確定不應保留的 Vault object。

---

## 7. 最短操作口訣

> **週初 Planner 定方向與時間 → 每日 Learn / Practice / Work / Review → 值得重用的進 Vault → 通過門檻的正式作品進 Work Log → 週末 Review 與 Vault consolidation → 三份 JSON 備份。**

只要記住三句：

1. **不要把計畫當能力證據。**
2. **不要把所有學習都當正式作業。**
3. **不要把發生過的一切都存進 Vault，只存未來值得再用的。**
