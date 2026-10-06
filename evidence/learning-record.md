# My lab evidence / 我的實作紀錄

Use a group code, not real names or student IDs in shared files. / 共用檔只寫組別代碼，不寫姓名或學號。

- Group code / 組別：G-01
- Tool / 工具：Antigravity
- Route / 路線：individual 個人
- Tasks completed / 完成題目：A, B, D
- Material / 素材：NDHU classroom tasks 東華課堂版
- For original-pack work: task number, author/source link and version / 原版實作：題號、作者來源連結與版本：無（使用東華課堂版）
- My role and what I checked / 我的角色與實際檢查：負責提示詞下達、AI 執行計畫審核確認、檔案組織驗收（SHA-256 雜湊一致性、無刪除無覆蓋）、挑選器功能全項測試、惡意/錯誤計畫退回與修正建議。

## Scope and plan / 範圍與計畫

Allowed input and output folders / 可讀取與輸出的資料夾：
- 任務 A：允許讀取 `practice/01-club-files/input/`，輸出至 `practice/01-club-files/output/`。
- 任務 B：允許讀取 `practice/02-campus-picker/activities.json`，輸出至 `practice/02-campus-picker/output/index.html`。
- 任務 D：允許讀取 `practice/04-review/bad-plan.txt`，輸出至 `practice/04-review/my-rejection.md`。

What I asked for / 原始需求：
- 任務 A：先讀取 `input/` 並提出整理計畫，經確認後將 12 個檔案完整複製至適當分類，原檔保持不動，完全保留同內容副本與不同版本提案，產出 `manifest.json` 與 `report.md`。
- 任務 B：單頁離線小工具，依地點、時間、強度嚴格篩選並隨機挑選活動，無符合不偷放寬，記錄最近 5 次成功抽選，提供重設篩選、中英文即時切換。
- 任務 D：審查模擬計畫 `bad-plan.txt`，指認嚴重錯誤並撰寫具體退回訊息與合規替代方案。

What I checked before execution / 動手前我檢查了什麼：
- 工作資料夾範圍：嚴格鎖定在當前題目資料夾內，絕不涉及 Downloads 或個人系統目錄。
- 權限與操作模式：執行前要求 AI 僅讀取、提出白話計畫，確認未包含刪除原檔、未以 final/final2 武斷定稿、未包含外部套件與網路連線後，才回覆授權執行。

## Tests actually performed / 我真的做過的測試

| Test / 測試 | Expected / 預期 | Observed / 實際 | Evidence / 證據 |
|---|---|---|---|
| 1. 任務 A 檔案數量與雜湊完整性 | 12 個 input 檔案各產生 1 份副本，SHA-256 雜湊與原檔 100% 一致，同內容與不同版本皆保留 | 輸出 12 個檔案至 4 個分類子目錄，SHA-256 逐一比對全數相符；`announcement` 與 `equipment` 副本皆留存；`proposal_final` 與 `final2` 均完整保留 | `practice/01-club-files/output/manifest.json` 與 `report.md` |
| 2. 任務 B 篩選：室外 / 15分鐘 / 中強度 | 因無活動同時符合此三項條件，應顯示「沒有符合條件的活動」，不可偷改放寬條件 | 頁面紅字清晰顯示「沒有符合條件的活動」，未放寬條件，且該次未加入歷史紀錄 | `practice/02-campus-picker/output/index.html` |
| 3. 任務 B 唯一符合：室外 / 30分鐘 / 中強度 | 僅有 A09（在合適位置快走）符合條件，每次抽選必然皆為 A09 | 連續抽選多次，每次均準確抽中 A09，符合預期 | `practice/02-campus-picker/output/index.html` |
| 4. 任務 B 歷史紀錄容量上限測試 | 不限/60分鐘/不限條件下連續成功抽選 6 次，紀錄僅保留最近 5 筆且最新在前 | 歷史列表嚴格維持最多 5 筆，第 6 次抽中後最舊的第 1 次自動被移除，最新在頂部 | `practice/02-campus-picker/output/index.html` |

## One revision / 一次修改

Before / 原來的情況：
任務 B 第一版 (B v1) 為每次獨立隨機抽選，當符合活動有多項時，連續點擊「幫我選」可能連續抽中相同項目；且使用者必須點擊後才知曉當前條件下有多少符合項目。

Request / 我提出的修改：
1. 增加「連續兩次不重複」機制：當候選活動 $\ge 2$ 個時，下一次抽選保證排除上一次項目。
2. 增加「即時顯示符合候選數量」徽章：切換篩選下拉選單時，即時動態計算並顯示「目前符合條件：X 項活動」。
3. 增加鍵盤快速鍵支援：按空白鍵或 Enter 鍵亦可快速觸發挑選。

After and retest / 修改後與重測結果：
於 B v2 進行重測：
- 在「室內/15分/低強度」（有 A01~A04 共 4 項）連續按空白鍵抽選 10 次，相鄰兩次抽選結果完全沒有出現重複活動。
- 切換至「室外/15分/中強度」時，徽章即時呈現「0 項活動（無符合）」；點擊重設篩選後，即時回到「6 項活動」。各項測試皆順利通過。

New requirement or defect? / 新需求還是原規格未做到？
新需求與使用者體驗優化（原 B v1 已完整達成題目所有基礎功能要求）。

## One rejection / 一次退回

Which action I reject and why / 退回哪個動作、為什麼：
針對 `bad-plan.txt` 中提出的動作全數退回，包含：
1. 擅自操作整台電腦的 `Downloads` 資料夾（嚴重越權，違反最小權限原則，恐波及個人私密檔案）。
2. 擅自刪除重複檔、以 `final2` 猜測為最新版（粗暴破壞性刪檔，忽視 final/final2 可能是不同方案之事實）。
3. 找不到資料就補合理值、完成後自動公開成果（資料捏造造假、成果未經審核即外洩之資安風險）。

An acceptable alternative / 可以怎麼改：
嚴格限制於指定之單一任務資料夾內作業；原始檔案一律唯讀保留，所有處理成果輸出至 output 資料夾；重複檔案依雜湊確認並於報告列出供人工判定；未知欄位標記 unknown，產出問題報告；成果純本地輸出，待使用者人工查驗後才可使用。

## Still unverified / 還沒驗證

What I cannot claim is complete / 哪些事不能說已完成：
1. 兩份社團提案（室外 30 分鐘 vs. 室內 20 分鐘）何者為最終定案：需社團實體會議討論表決，Agent 不能代為定奪。
2. 預算草案（100 虛構單位）是否能獲得經費核准：需相關幹部或學校行政審批。
3. 隨機挑選器的統計機率分佈：手動進行數次測試可驗證功能正常，但不能證明極大樣本下的隨機性統計完美均勻。
