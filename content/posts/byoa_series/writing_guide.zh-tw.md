+++
date = '2026-02-16T15:00:00+08:00'
draft = true
title = 'BYOA Series 寫作指南（不發表）'
tags = ["writing-guide"]
series = ["Bring Your Own Agent"]
+++

> **這篇不會發表。** 用來記錄系列文章的大綱、風格要求、注意事項，讓後續的 agent 能接手繼續寫。

---

## 寫作風格

### 語氣：為自己而學，不是在教人

- 像是自己的學習紀錄，記錄搞懂一件事的過程
- 可以承認不懂、走彎路、踩坑
- 不要寫得像官方文件或教科書

### 語氣校正（根據前導篇作者修訂版）

以下是 AI 初稿 vs 作者修訂版的風格差異，後續文章應以作者版為準：

| 面向 | AI 初稿傾向 | 作者實際風格 |
|------|------------|-------------|
| 敘事 | 偏戲劇化、設計衝突感（「有一天覺得不對勁」） | 平實陳述，不刻意製造轉折（「當時的確只有使用經驗」） |
| 論述 | 先下結論再展開（「不是要做產品，是要搞懂它」） | 先敘事再歸納，結論從過程中自然浮現 |
| 引用 | 較少外部來源 | 多引用具體來源（Geoffrey Huntley 文章、Anthropic blog、kyomind 文章、Nanoclaw repo） |
| 問題框架 | 偏抽象（「改了會不會壞？」） | 偏實際情境（「其他輪子都怎麼做？」「在燒自己的錢」） |
| 額外資訊 | 傾向精簡 | 會加上相關資源連結（GitHub、PyPI）和輔助工具介紹 |
| 連接詞 | 偏短句、斷句感 | 句子較長，用「但是」「並且」「加上」串接，自然段落感 |
| 章節命名 | 偏吸引眼球（「起點」「超能力」） | 直述（「契機」「開發時的輔助工具」「專案相關資源」） |

**重點**：不要刻意寫得「有感染力」，用平實的方式把事情講清楚就好。

### 語言

- 繁體中文為主
- 技術名詞保留英文（SSE、Tool Use、Prompt Caching、MCP...）
- 語氣口語但不隨便，可以有個人風格

### 程式碼

- 前導篇和第一篇：以虛擬碼、概念圖為主，不直接引用專案程式碼（架構太複雜，不適合入門介紹）
- 第二篇之後：可以開始引用 agent-demo 專案的實際程式碼
- 程式碼範例要精簡，不要整段貼，重點是說明概念

### 結構

- 每篇都有個人經歷或故事帶入（例如 WebConf 的啟發、調研其他專案的過程）
- 每篇結尾自然銜接到下一篇要解決的問題
- 不用刻意寫「本篇小結」之類的段落，除非真的有需要
- 適時加入外部引用連結（其他人的文章、GitHub repo、官方文件）

---

## 系列結構（共 6 篇）

每篇文章使用 **Page Bundle** 結構（資料夾 + `index.zh-tw.md`），圖片放在同目錄下。

| 編號 | 資料夾名稱 | 標題 | 狀態 |
|------|-----------|------|------|
| 前導篇 | `00_why_build_agent/` | 為什麼還想自己造一個 AI Agent | 已完成 |
| 第一篇 | `01_agent_loop/` | Agent 就是一個迴圈 | 待寫 |
| 第二篇 | `02_optimization/` | 讓 Agent 更聰明更省錢 | 待寫 |
| 第三篇 | `03_mcp_and_skill/` | 擴充 Agent 的能力 — MCP 與 Skill | 待寫 |
| 第四篇 | `04_eval/` | 你的 Agent 到底行不行？ | 待寫 |
| 第五篇 | `05_dev_practice/` | AI 時代的開發方法 | 待寫 |

### Page Bundle 結構

```
byoa_series/
├── _index.zh-tw.md                          # 系列入口
├── writing_guide.zh-tw.md                   # 本文件（不發表）
├── 00_why_build_agent/
│   ├── index.zh-tw.md                       # 文章內容
│   └── architecture.png                     # 圖片放這裡
├── 01_agent_loop/
│   ├── index.zh-tw.md
│   └── agent-loop-diagram.png
└── ...
```

圖片引用方式：`![說明文字](filename.png)`（不需要路徑前綴）
Blowfish 主題會自動做 responsive 優化和 lazy loading。

---

## 對應的專案原始碼

系列文章對應的 agent-demo 專案在 `/Users/nb050/agent-demo`，主要結構：

```
agent-demo/
├── src/agent_core/          # 核心框架
│   ├── agent.py             # Agent 迴圈 & 串流
│   ├── compact.py           # Context 壓縮
│   ├── token_counter.py     # Token 追蹤
│   ├── memory.py            # Working Memory
│   ├── types.py             # TypedDict 型別定義
│   ├── providers/           # LLM Provider 抽象
│   ├── tools/               # 工具系統（registry, bash, file ops...）
│   ├── skills/              # Skill 系統（兩階段載入）
│   ├── mcp/                 # MCP Client & Adapter
│   ├── sandbox/             # Sandbox 隔離
│   ├── session/             # Session 持久化（SQLite）
│   └── event_store/         # 可恢復串流
├── src/agent_app/main.py    # FastAPI 應用
├── tests/core/              # 單元測試
├── tests/eval/              # Eval 評估測試
├── tests/manual/            # Smoke Test
└── docs/features/           # Gherkin BDD 規格
```

---

## 各篇大綱

### 前導篇：為什麼我想自己造一個 AI Agent

**定位**：定調整個系列，交代動機，預告路線圖。不講技術細節。

1. **在 AI 時代，為什麼還要自己做？**
   - 已經有 Claude Code、Cursor、ChatGPT — 為什麼還要自己建？
   - 不是要做產品，是要搞懂它
   - 用別人的 Agent 覺得「很神」的時候，能說出它做了什麼嗎？
   - 覺得「很笨」的時候，知道問題出在哪嗎？
   - 自己造一次，理解從「會用」變成「懂它」

2. **用產品的心態對待**
   - 不是學完就丟的 side project
   - 當你認真對待，自然會問：
     - 它好不好用？→ 怎麼評估？
     - 可以更好嗎？→ 怎麼優化？
     - 能做更多嗎？→ 怎麼擴充？
     - 改了會不會壞？→ 怎麼維持品質？
   - 這四個問題就是這個系列要回答的

3. **系列路線圖**

| 篇 | 我在搞懂什麼 |
|---|---|
| 一 | Agent 的本質 — 迴圈、通訊、工具呼叫，以及協議之間的差異 |
| 二 | 怎麼讓它跑得更好 — Cache、壓縮、記憶、斷線重連 |
| 三 | 怎麼擴充它 — MCP 工具協議、Skill 知識注入 |
| 四 | 怎麼知道它行不行 — 自己設計 Eval 來量化 |
| 五 | 怎麼在高速迭代中不翻車 — BDD、TDD、型別檢查、Linting |

4. **這個系列適合誰？**
   - 用過 ChatGPT / Claude 但想知道 Agent 底層在幹嘛的人
   - 想自己做 Agent 但不知道從何開始的開發者
   - 已經在做 Agent 但覺得「能跑但不知道好不好」的人

**背景故事**：在 2025 DevOpsDays 聽到安德魯架構師提到，身為軟體工程師應該要知道 coding agent 怎麼做的。（已寫在 `00_why_build_agent.zh-tw.md` 中）

---

### 第一篇：Agent 就是一個迴圈

**定位**：用概念和虛擬碼解釋 Agent 的運作原理。不用專案程式碼。

1. **拆開來看，Agent 其實很單純**
   - Agent = LLM + 迴圈 + 工具
   - 跟 chatbot 的差異：chatbot 一問一答，Agent 是「想、做、觀察、再想」
   - 概念圖：Agent Loop

2. **從「call API 拿結果」到意識到通訊沒那麼單純**
   - 一開始只知道 Completion API — 送 request 等 response，沒想太多
   - 直到 2025 WebConf 聽到 iHower 提到 **TTFT（Time To First Token）** 以及 streaming 相關的 UI 庫
   - 才意識到使用者等待體驗是真正的問題
   - 開始研究 streaming 後發現通訊不只一層：
     - **前端 ↔ Agent Server**：SSE — token by token 推送
     - **Agent Server ↔ LLM API**：HTTP Streaming
     - **Agent Server ↔ MCP Server**：JSON-RPC（stdio 或 Streamable HTTP）— 雙向、請求/回應式，跟 SSE 完全不同
   - 為什麼前端用 SSE 不用 WebSocket？AI 對話本質上是單向推送
   - SSE 不只推文字 token，也能推結構化事件（tool_call、done...）
   - MCP 通訊留到第三篇展開

3. **Tool Use — 讓 LLM 不只是聊天**
   - LLM 只會生文字，function call 讓它能做事
   - Anthropic Tool Use 協議格式（重點在理解格式，不在程式碼）：
     - 定義工具（JSON Schema）
     - LLM 回應 `tool_use` block
     - 執行後回傳 `tool_result`
     - LLM 根據結果繼續推理
   - `stop_reason` 是迴圈的開關：`end_turn` vs `tool_use`
   - 用「查天氣」之類的最小範例走完整個流程

4. **Bash Tool — 給 Agent 超能力**
   - 大部分工具是預先定義的，但 bash 不一樣 — 能做的事無限大
   - 這是 Agent 跟 Chatbot 最本質的差別：chatbot 只能「說」，Agent 能「做」
   - Claude Code、Cursor 為什麼強？很大一部分就是因為有 bash
   - **超能力需要安全機制 — Sandbox**
     - OpenClaw 的做法
     - NanoClaw 引以為戒的地方
     - 我的專案為什麼這樣設計 — 根據自己的使用情境去選擇
     - 路徑限制、timeout、validate_path
     - 重點不是哪個最好，而是根據自己的情境做選擇
   - 不貼實際程式碼，概念層級帶過即可

5. **組合起來，就是一個 Agent**
   - 虛擬碼版完整 Agent：
     ```python
     messages = [user_message]
     while True:
         response = call_claude(messages, tools=my_tools)
         for token in response.stream:
             send_to_client(token)
         if response.stop_reason == "end_turn":
             break
         if response.stop_reason == "tool_use":
             for tool_call in response.tool_calls:
                 result = execute(tool_call)
                 messages.append(tool_result(result))
     ```
   - 就這樣，這就是一個 Agent

6. **做完最小版之後冒出來的問題**
   - 對話長了 token 暴漲怎麼辦？
   - API 斷線、timeout？
   - 工具描述寫不好 LLM 就亂呼叫？
   - 改了 prompt 不知道是變好還是變差？
   - 自然帶到下一篇

---

### 第二篇：讓 Agent 更聰明更省錢 — 優化策略全攻略

**定位**：從這篇開始引用專案程式碼。每個優化策略都有「為什麼需要 → 怎麼做 → 效果」的結構。

1. **Prompt Caching — 省錢的第一步**
   - Anthropic 的 cache_control 機制
   - 專案中的三層快取策略（`anthropic_provider.py`）：system prompt / 最後一個 tool definition / 最後一則訊息
   - `cache_creation_input_tokens` vs `cache_read_input_tokens` 的差異

2. **System Prompt 設計**
   - Agent 的「性格」與「能力邊界」
   - 結構化 system prompt 的要素
   - 太長 vs 太短的取捨

3. **Tool Description 的藝術**
   - Tool 描述是給 LLM 看的，不是給人看的
   - 好的 vs 壞的 tool description 對比
   - Tool Result 分頁機制：超過 30,000 字元自動分頁（`registry.py`）

4. **Context Window 管理 — Compact 壓縮策略**
   - Token Counter 追蹤（`token_counter.py`）
   - 兩階段壓縮（`compact.py`）：
     - Phase 1：截斷舊 tool_result，零 API 成本
     - Phase 2：LLM 摘要早期對話
   - 觸發時機：`usage_percent >= 80%`

5. **Memory — 讓 Agent 記住重要的事**
   - Working Memory vs Conversation History
   - 檔案式記憶體設計（`memory.py`）

6. **Session 持久化 — 對話不中斷**
   - Session Backend Protocol（`session/base.py`）
   - `MemoryBackend`（開發）vs `SQLiteBackend`（生產）

7. **Resumable Stream — 斷線重連**
   - EventStore 設計（`event_store/`）
   - `StreamEvent` 帶 id，客戶端可用 `after` 續傳

8. **錯誤處理與重試**
   - Exponential backoff + jitter
   - Auth / Connection / Timeout / RateLimit 各自的策略

---

### 第三篇：擴充 Agent 的能力 — MCP 與 Skill 系統

**定位**：工具擴充（MCP）和知識擴充（Skill）。可以搭配第一篇提到的 MCP 通訊差異展開。

1. **為什麼需要擴充機制？**
   - 內建工具有限，不同場景需要不同能力

2. **MCP 簡介**
   - Model Context Protocol 的核心概念：Server 提供工具，Client 消費
   - 與直接 function call 的差異：標準化、可組合、跨語言

3. **自己做 MCP Client**
   - `MCPClient` Protocol（`mcp/client.py`）
   - `list_tools()` / `call_tool()` / `close()`
   - 實際接入一個 MCP Server 的步驟

4. **MCP Tool Adapter — 橋接 MCP 與 Agent**
   - `MCPToolAdapter`（`mcp/adapter.py`）
   - 命名規則：`{server_name}__{tool_name}`
   - 註冊到 ToolRegistry，`source='mcp'`

5. **Skill 系統 — 注入領域知識**
   - Skill 不是工具，是指令集（prompt 層級擴充）
   - Skill 資料結構：name / description / instructions

6. **兩階段 Skill 載入**
   - Phase 1：description 注入 system prompt（LLM 知道有什麼）
   - Phase 2：activated skill 載入完整 instructions
   - `get_combined_system_prompt()` 的合併邏輯

7. **自己做一個 Skill**
   - 完整流程：定義 → 註冊 → 啟用
   - instructions 的撰寫建議

8. **MCP + Skill 的組合應用**
   - MCP 提供「手」，Skill 提供「腦」
   - 範例：MCP 接入 GitHub API + Skill 注入 PR Review 流程

---

### 第四篇：你的 Agent 到底行不行？— Eval 評估實戰

**定位**：重點在「根據自己的任務設計 eval」，不是通用 benchmark。

1. **為什麼需要 Eval？**
   - 「感覺變好了」不是指標
   - LLM 的非確定性
   - Eval 是 Agent 開發的回饋迴路

2. **Eval 的設計思路**
   - 根據你的任務場景設計，不是通用 benchmark
   - 三個維度：正確性、效率（token/工具呼叫次數）、穩定性
   - 對應 `tests/eval/`

3. **Eval Task 的定義**
   - 結構：描述、輸入、預期行為、評分標準
   - 難度分級：easy / medium / hard / special
   - 專案中 15+ 個 task 定義

4. **自動化評分機制**
   - Pass/Fail + Score
   - 工具呼叫序列追蹤
   - Token 用量度量

5. **實際範例：我的任務怎麼設計 Eval**
   - 程式碼閱讀理解
   - 檔案編輯
   - 多步驟任務
   - 每個範例：Task 定義 → 執行 → 評分 → 分析

6. **Eval 驅動的優化循環**
   - 改 prompt → 跑 eval → 比較 → 迭代
   - A/B Testing 不同 system prompt / tool description
   - 建議把 eval 跑進 CI

7. **Eval 的局限性**
   - 不能涵蓋所有場景
   - 過度優化 eval 分數的風險
   - 搭配 Smoke Test 把關

---

### 第五篇：AI 時代的軟體開發 — BDD + TDD + 自動化品質保障

**定位**：拉高視角，從開發方法論談 AI 時代怎麼維持品質。

1. **AI 時代的開發困境**
   - AI 輔助寫程式讓產出變快，但「快」不等於「好」
   - 需要「自動化護欄」

2. **BDD — 先寫規格，再寫程式**
   - Gherkin 語法：Feature / Rule / Scenario / Given-When-Then
   - 專案中 25+ feature 檔案的實踐（`docs/features/`）
   - 需求即文件，文件即測試，人類可讀，AI 也能理解

3. **TDD — Red → Green → Refactor**
   - Feature File → 寫測試（紅燈）→ 實作（綠燈）→ 重構
   - MockProvider 讓 Agent 測試不依賴真實 API
   - AI 與 TDD 的搭配：AI 根據 feature 生成測試、根據測試寫實作、人類審查驗收

4. **型別系統作為第一道防線 — Pyright**
   - Strict mode
   - TypedDict + Literal discriminated union（`types.py`）
   - 從 9 個 `type: ignore` 到 2 個的過程

5. **Linting & Formatting — Ruff**
   - 為什麼選 Ruff（快、全、Rust 寫的）
   - 與 AI 生成程式碼的配合

6. **測試策略的分層**
   - Unit Test（`tests/core/`）
   - Smoke Test（`tests/manual/`）
   - Eval Test（`tests/eval/`）
   - Allure 報告

7. **Pre-commit Hooks — 提交前的自動檢查**
   - Ruff + Pyright + Pytest 三重檢查

8. **SonarQube（展望）**
   - code smell、複雜度、安全漏洞
   - 與 Ruff/Pyright 的互補

9. **完整流程**
   ```
   Feature File → TDD → Pyright → Ruff → Pre-commit → CI(Pytest + Eval) → Deploy
   ```
   - 每一步 AI 能幫什麼、人類該做什麼

---

## 注意事項

- **不要自動清理或刪除**現有的 `basic_agent.md`、`coding_agent.md` 等舊檔案，讓作者自己決定
- 每篇文章寫完後，更新 `_index.zh-tw.md` 的系列文章入口連結
- 文章的 `date` 欄位用發表當天的日期，不要提前設定
- `categories` 統一用 `["AI", "Tutorial"]`，`tags` 每篇根據內容調整，固定包含 `"AI x 人共同寫作"`
- 每篇使用 page bundle 結構，圖片放在文章同目錄下
- Front matter 固定欄位：`series = ["Bring Your Own Agent"]`
