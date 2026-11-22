# LLM Wiki 執行與檢查日誌（Execution Log）

## 階段一：原始資料 Ingest 紀錄（2026-11-23）

| 時間 | 動作 | 來源檔案 (`raw/`) | 目標 Wiki 頁面 | 閘門狀態 | 備註 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 2026-11-23 | Ingest #1 | `01_wiki_specs_and_styles.md` | `rules-and-lane.md`, `styles-comparison.md`, `equipment-and-gear.md` | PASS | 完成球道規格、三大球路與體重÷10迷思建檔 |
| 2026-11-23 | Ingest #2 | `02_scoring_rules.md` | `rules-and-lane.md` | PASS | 完成 10 格計分與第 10 格加打規則建檔 |
| 2026-11-23 | Ingest #3 | `03_beginner_tips.md` | `aiming-and-spare.md`, `equipment-and-gear.md` | PASS | 完成瞄準箭頭、防洗溝與球道禮儀建檔 |
| 2026-11-23 | Ingest #4 | `04_shoes_and_gear.md` | `equipment-and-gear.md` | PASS | 完成滑步腳/支撐腳分工與可換底編號邏輯建檔 |
| 2026-11-23 | Ingest #5 | `05_spinner_mechanics.md` | `spinner-technique.md` | PASS | 完成飛碟球翻轉動作、流派整理與防受傷警示建檔 |

---

## 階段二：教學 HTML 簡報生成與查核紀錄（2026-11-23）

### Run #1 — FAIL（退回節點 G 重生）
- **觸發檢查節點**：節點 H（簡報品質檢查閘門）
- **攔截到的具體問題**：
  1. **球路觀念混淆（P6 / P7）**：介紹飛碟球時，誤將美式曲球的「球道尾段大幅度向內急彎」寫成飛碟球特徵。
  2. **計分範例算錯（P3）**：第 10 格範例打出 `X / 8 / 1` 時，誤將總分多加一次獎勵分。
  3. **術語未統一（P2 / P9）**：直接沿用了原始資料中的港式與簡體用語（「球樽」、「洗沟」），與台灣慣用語不一致。
- **修正與流程升級（v1.0 → v2.0）**：
  - 更新 `AGENTS.md`，將「術語清洗」、「球路邊界防混淆」與「迷思過濾」往前移至 Ingest 閘門（節點 C），並新增計分獨立驗算規則。
  - 建立 `wiki/glossary.md` 作為強制替換表，並退回節點 G 重新生成 `slides/index.html`。

### Run #2 — PASS（鎖定最終版）
- **觸發檢查節點**：節點 H（簡報品質檢查閘門）
- **查核結果**：
  - 10 頁簡報皆已標註對應 `wiki/` 來源檔名，無外部幻覺。
  - P3 計分範例經逐格驗算無誤（第 1 格 20、第 2 格 38、第 3 格 47；第 10 格 `X/8/1 = 19`）。
  - P6 / P7 飛碟球與曲球邊界清晰（水平自轉、軌跡相對筆直）。
  - 全文術語已統一為台灣慣用語（球瓶、洗溝、全倒、補中）。
- **最終輸出**：`slides/index.html`