# MetaphysicsQuant - 工程化中國術數分析平台（粵語）

<p align="center">
  <a href="../README.md">Main</a> |
  <a href="./README_CN.md">简体中文</a> |
  <a href="./README_ZH_TW.md">繁體中文</a> |
  <a href="./README_YUE.md">粵語</a> |
  <a href="./README_EN.md">English</a>
</p>

> **展示說明**：本倉庫只用嚟做項目介紹同成果展示，不包含任何項目源碼、資料檔案、案例資料庫或者 API 設定。

MetaphysicsQuant 唔係一個只係會顯示四柱、星盤或卦盤嘅排盤工具。佢將中國傳統術數中最難工程化嘅部分做成咗可運行嘅軟件系統：曆法換算、干支推導、神煞同格局規則、古籍條文檢索、專題化報告、AI 二次解讀、SQLite 案例庫、Markdown/TXT 匯出同桌面端完整工作流。

而家穩定主線係 `mainAppUI.py` 嘅 PySide6 桌面應用；`mainAppUI_modern.py` 係註冊表驅動嘅現代化外殼；`mainWebUI.py` 同 `web_platform/` 保留為 Web 方向程式碼。

最後更新：2026-05-03

## 目錄

- [核心功能概覽](#核心功能概覽)
- [介面截圖](#介面截圖)
- [四柱八字核心能力](#四柱八字核心能力)
- [其他術數模組](#其他術數模組)
- [AI 分析同報告系統](#ai-分析同報告系統)
- [案例管理同匯出](#案例管理同匯出)
- [工程實作能力](#工程實作能力)
- [項目架構](#項目架構)
- [倉庫規模](#倉庫規模)
- [子模組文件導航](#子模組文件導航)
- [安裝同啟動](#安裝同啟動)
- [免責聲明](#免責聲明)

## 核心功能概覽

呢個項目嘅定位係“傳統術數知識庫 + 規則引擎 + 桌面分析系統”，重點係把大量分散在古籍、民間訣法同現代排盤經驗裡嘅規則，轉做可複查、可儲存、可擴充嘅程式輸出。

已經實作嘅實用功能：

| 能力 | 已經實作內容 |
|---|---|
| 四柱八字 | 數字排盤、干支手輸、原局、大運、流年、流月、胎元、命宮、身宮、七柱專題論命、串宮壓運、紫微聯動。 |
| 神煞同格局 | `SZBZ_1Gz.py` 中有 330 個方法，其中約 180 個同神煞、貴格、凶格、刑沖合會、串宮壓運等判定直接相關。 |
| 古籍規則庫 | 四柱模組數據涵蓋《三命通會》《滴天髓》《窮通寶鑑》《神峰通考》《五行精紀》《鬼谷子》《袁天罡稱骨》等。 |
| 紫微斗數 | 十二宮排盤、主輔雜曜、四化、星曜亮度、大限、流年、流月、排盤圖儲存、星曜組合匹配。 |
| 易經六爻 | 時間起卦、三數起卦、玄數起卦、本卦變卦、動爻、六親、六神、世應、納甲、六十四卦資料。 |
| 擇日合婚 | 萬年曆、年曆、主題擇日、婚嫁、求職、開業、求財、出行、求醫、入宅、求學、求子、合婚參考。 |
| 姓名號碼 | 中文姓名學、康熙/新華筆畫、五格三才、八十一數理、個人起名、公司起名、測字、號碼分析。 |
| 西文數理 | Pythagorean、Cheiro/Chaldean、Vedas 三體系合併報告，支援英文姓名同選年分析。 |
| 神數系統 | 鐵板神數、邵子神數、太素/太玄類數字推演，支援條文檢索、原局、大運、流年同綜合分析。 |
| 案例系統 | SQLite 案例庫、分類、搜尋、備註、載入回填、JSON/Excel 匯入匯出、Markdown/TXT 報告匯出。 |
| AI 解讀 | 按報告專題拆分內容，呼叫 OpenAI-compatible、Claude、Gemini、OpenRouter、DeepSeek、Qwen、SiliconFlow 等供應商。 |

項目輸出唔係一句“吉凶如何”嘅短評，而係可展開嘅結構化資料。例如而家倉庫中嘅四柱原局報告樣本已經達到 3 萬字量級，包含排盤資訊、七柱專題、古籍條文、神煞組合、運限同 AI 解讀入口。係否最終採用某條斷語，仍然由使用者結合現實背景判斷。

## 介面截圖

以下截圖來自而家桌面端程式，按主要專題模組展示實際介面形態。

<table>
  <tr>
    <td align="center"><strong>四柱八字</strong><br><img src="../image/four_pillars_destiny.png" alt="四柱八字介面" width="900"></td>
  </tr>
  <tr>
    <td align="center"><strong>紫微斗數</strong><br><img src="../image/purple_star_astrology.png" alt="紫微斗數介面" width="900"></td>
  </tr>
  <tr>
    <td align="center"><strong>易經解卦</strong><br><img src="../image/hexagram_divination.png" alt="易經解卦介面" width="900"></td>
  </tr>
  <tr>
    <td align="center"><strong>擇日合婚</strong><br><img src="../image/auspicious_date.png" alt="擇日合婚介面" width="900"></td>
  </tr>
  <tr>
    <td align="center"><strong>姓名號碼</strong><br><img src="../image/nameology.png" alt="姓名號碼介面" width="900"></td>
  </tr>
  <tr>
    <td align="center"><strong>鐵板神數 / 邵子神數</strong><br><img src="../image/esoteric_numerology.png" alt="鐵板神數同邵子神數介面" width="900"></td>
  </tr>
  <tr>
    <td align="center"><strong>案例管理</strong><br><img src="../image/character_case.png" alt="案例管理介面" width="900"></td>
  </tr>
</table>

## 四柱八字核心能力

四柱八字係而家倉庫最重嘅核心模組：`four_pillars_destiny/` 約 2.88 萬行 Python，15 個 JSON 數據文件。它嘅價值不在“排出八個字”，而在排盤之後嘅大規模規則整理同報告生成。

### 1. 兩套入口

- `四柱八字`：輸入姓名、性別、公曆/農曆年月日時分，自動換算四柱、起運、大運、流年、流月。
- `四柱批命`：手動輸入年柱、月柱、日柱、時柱、大運、流年、小限、流月，適合古籍案例、已知八字反查同課堂推演。

### 2. 干支規則底座

`four_pillars_destiny/SZBZ_1Gz.py` 係四柱系統嘅規則地基，涵蓋：

- 天干、地支、藏干、五行、陰陽、六十甲子、纳音、旬空。
- 十神、十二長生、祿命長生、纳音長生、四貴四平四忌。
- 天乙貴人、福星貴人、太极貴人、文昌貴人、天德、月德、天喜、驛馬、華蓋、金輿、學堂、詞館、截路空亡、鬼門關、沐浴殺、暴敗、自縊、四廢、官符、死符、病符、血光、離鄉、劫煞、亡神、羊刃、元辰、空亡、咸池、天羅地網、孤辰寡宿等大量神煞同格局判定。
- 串宮壓運十二神：太歲、青龍、喪門、六合、官符、小耗、大耗、朱雀、白虎、貴神、吊客、病符，並實現神煞變化規則。
- 盲師神煞同民間經驗規則，例如四窮日、莊殺、羅殺、忌殺、八敗、懸梁殺、胞胎殺、鐵刑殺、天掃星、地掃星、追魂、鏟度等。

呢度適合展示項目實力：呢啲唔係 UI 文案，而係被拆成函式同資料結構嘅規則引擎。

### 3. 七柱論命

`four_pillars_destiny/SZBZ_2Bz.py` 在傳統年月日時四柱之外，继续纳入胎元、命宮、身宮，形成“七柱”分析視角。報告按專題组织：

- 性格信息
- 學業信息
- 事業信息
- 財運信息
- 訣法信息
- 婚姻信息
- 六親信息：父親、母親、兄弟、子女、其他親屬
- 傷災健康
- 陽宅陰宅

呢啲專題唔係單一流派硬套，而係按來源分層拼接，例如蘇氏盲派、民間盲派、五行精紀、三命通會、玉照神應真經、梁派理論、鬼谷子分定經、三世演禽等。README 裡強調“實事求係”：項目提供可追溯嘅規則輸出，不宣稱替代現實決策。

### 4. 古籍同數據來源

四柱模組嘅 `data/` 目錄儲存了多類規則同條文數據：

- `SanMingTongHui.json`：《三命通會》
- `DiTianSui.json`：《滴天髓》
- `QiongTongBaoJian.json`：《窮通寶鑑》
- `ShenFengTongKao.json`：《神峰通考》
- `WuXingJingJi.json`：《五行精紀》
- `GuiGuZi_LTQ.json`、`GuiGuZi_MGB.json`：鬼谷子分定經、鬼谷子命宮表
- `YuanTiangangCG.json`：袁天罡稱骨
- `SanShiYanQin.json`：三世演禽
- `SuShiMangPai.json`：蘇氏盲派
- `DaMoYiZhangJing.json`、`JueFa.json`、`Books.json` 等補充數據

程式碼中也直接引用《淵海子平》《蘭台妙選》《玉照神應真經》《永樂大典》《天元巫咸經》等來源或規則名。展示時可以說：這係一個把多種典籍、訣法同程式規則合併成專題報告嘅工程項目。

### 5. 可生成嘅報告

四柱封裝層 `SZBZ_6BzMs.py` 支援：

- 原局命書：`bzms_num()` / `bzms_gz()`
- 簡斷命書：`bzmss_num()`
- 大運命書：`dyms_num()` / `dyms_gz()`
- 流年命書：`lnms_num()` / `lnms_gz()`
- 流月命書：`lyms_num()` / `lyms_gz()`
- 從而家年份起嘅 10 年流年中批：`zpln_num()`
- 流年同大運交接分段、流月同大運交接分段
- 可選紫微斗數聯動，生成原局、大限、流年排盤圖並儲存圖片

倉庫中已有脫敏範例報告，如 `character_case/CaseReports/範例案例/範例案例_四柱八字_原局分析_20260421_043836.md`，字元量約 3.6 萬；`character_case/CaseReports/A參考模板/範例案例_四柱八字_原局分析_20260421_031317.txt` 約 3.0 萬字符。這說明系統實際可以輸出長篇結構化報告，而唔係停留在功能設想。

## 其他術數模組

### 紫微斗數

`purple_star_astrology/` 實現十二宮排盤、主星辅星雜曜、四化、星曜亮度、大限、流年、流月同排盤圖。`Star_Combination_Matcher.py` 負責從 JSON 數據中匹配單星、組合星同男女差異化解釋。專題數據涵蓋性格、財富、婚姻、事業、健康、父母、母親、兄弟、子女、田宅、遷移、交友等。

### 易經解卦同六爻

`hexagram_divination/` 支援時間起卦、三數起卦、玄機數、玄卦輸入、本卦、變卦、動爻、六親、世應、六神、納甲同流年解卦。`notion/` 下儲存 64 卦 Markdown 文件，`data/` 下儲存《易經》資料、小六壬、諸葛神數、干支神數、太極神數、牙牌神數等映射。

### 擇日合婚

`auspicious_date/` 唔係簡單黃曆查詢，而係按主題篩選日期。已涵蓋婚嫁、納采問名、安床、上官赴任、臨政親民、開業開市、求財、立契交易、提車、宴會、求學、考試、入學、拜師、出行、求醫、入宅、祭祀、求子等場景。規則中可見《協紀辨方書》《玉匣記》同其他民俗擇日條文。

### 姓名學同西文數理

`nameology/` 涵蓋中文姓名學同西文數理：

- 中文姓名學：康熙/新華筆畫、五格、三才、八十一數理、五行、陰陽、生肖、專題斷語。
- 起名：個人起名、公司起名，可按喜用五行、規避五行、行業數據篩選。
- 測字同號碼：三字測字、手機號/車牌/編號數理分析。
- 西文數理：Pythagorean、Cheiro/Chaldean、Vedas 三體系合併輸出。
- 數據層：姓名字庫、康熙/新華筆畫、三才、五格、八十一數理、行業、西文數理資料，以及詩經、楚辭、論語、唐詩、宋詩、宋詞等起名語料。

### 鐵板神數、邵子神數、太素/太玄

`esoteric_numerology/` 提供鐵板神數、邵子神數同太素/太玄類數字推演。它同西文數理不同，更偏向傳統術數中嘅生辰、干支、刻分、卦象、聲音同條文檢索。邵子神數支援原局、大運、流年同综合報告；鐵板神數支援刻分、考刻同條文輸出。

## AI 分析同報告系統

項目没有把 AI 当成“神秘判斷器”，而係把 AI 放在工程链路嘅最後一層：先由規則系統生成可追溯嘅原始報告，再按專題拆分給模型做解釋、歸納同現實建議。

`ai/` 模組嘅能力包括：

- 供應商抽象：OpenAI、Claude、Google Gemini、OpenRouter、DeepSeek、DashScope 千問、SiliconFlow。
- OpenAI-compatible 支援：可接入 OpenRouter、DeepSeek、硅基流動等兼容 chat/completions 嘅服務。
- LangChain/LangGraph 風格工作流：有依賴時使用圖式呼叫，缺依賴時回退 REST。
- 專題拆分：`topic_schema.py` 根據報告模板拆分原局、大運、流年、流月、邵子等不同结構。
- 提示詞管理：`modern_prompts.py` 同 `prompt_manager.py` 將輸出約束到“現實建議、風險邊界、證據來源”，避免純術士化口吻。
- 金鑰管理：真實 API Key 走 `AI/.env` 或環境變數，唔應該提交到倉庫。

這部分嘅展示價值係：項目唔係單純“玄學脚本”，而係傳統規則引擎同現代 LLM 工作流嘅結合。

## 案例管理同匯出

`character_case/` 係統一案例系統，默認資料庫為 `character_case/cases.db`。它让項目從“算一次”升級為“長期研究同歸檔”：

- 按系統儲存案例：四柱八字、四柱批命、紫微斗數、易經解卦、擇日合婚、姓名號碼、鐵板神數、邵子神數。
- 分類、搜尋、備註、排序、拖曳、編輯。
- 從案例管理頁重新載入到對應分析介面。
- JSON 備份同 Excel 匯入匯出。
- `unified_formatter.py` 將分析结果整理為 Markdown 或 TXT，針對八字、紫微、六爻、邵子等系統做格式識別同排版最佳化。

注意：`character_case/cases.db` 係本機使用者數據文件，唔應該随意涵蓋或刪除。

## 工程實作能力

呢個項目能展示嘅技術能力包括：

- PySide6 桌面端：穩定入口 `mainAppUI.py`，現代化外殼 `mainAppUI_modern.py`。
- 模組化架構：術數模組、曆法模組、案例模組、AI 模組、通用 UI 模組分層清晰。
- 規則引擎：大量傳統規則被拆成可讀函式、數據表同 JSON 條文庫。
- 曆法底座：`lunar_solar/` 提供公曆/農曆、節氣、干支、EightChar、大運、流年、流月等基礎能力。
- 背景執行緒：分析過程透過共享 `WorkerThread` 執行，減少 UI 阻塞。
- 數據持久化：SQLite 管理案例，JSON/Excel 做交換格式。
- 報告工程：Markdown/TXT 格式化、專題拆分、AI 分析彈窗、關閉保護。
- Web 預研：`web_platform/` 保留 FastAPI/Vue/部署設定，說明項目具備從桌面端遷移到 Web 平台嘅基礎。

## 項目架構

MetaphysicsQuant 嘅架構重點係“桌面入口統一調度，核心術數模組獨立計算，曆法、案例、AI 同 UI 能力作為共享支撐層”。這让每個術數系統既能單獨執行，又能接入統一案例庫、統一匯出同 AI 專題解讀。

```text
┌────────────────────────────── 表現層 ──────────────────────────────┐
│ mainAppUI.py                                                       │
│ ├─ 案例管理                                                        │
│ ├─ 四柱八字                                                        │
│ ├─ 紫微斗數                                                        │
│ ├─ 易經解卦                                                        │
│ ├─ 擇日合婚                                                        │
│ ├─ 姓名號碼                                                        │
│ ├─ 鐵板神數                                                        │
│ ├─ 邵子神數                                                        │
│ └─ 四柱批命                                                        │
│                                                                    │
│ mainAppUI_modern.py                                                │
│ └─ ModernMainWindow + NavigationSidebar + module_registry          │
└────────────────────────────────────────────────────────────────────┘
                                  │
                                  ▼
┌──────────────────────────── 互動同通用 UI 層 ───────────────────────┐
│ ui_common/                                                          │
│ ├─ shared_ui.py: WorkerThread、TranslationThread、ResultDialog       │
│ ├─ app_shell.py: 現代化主視窗、案例聯動、關閉保護                    │
│ ├─ module_registry.py: 模組注册、分组、案例路由                      │
│ ├─ navigation.py: 側邊欄導航                                        │
│ └─ case_notes.py: 案例備註彈窗                                      │
└────────────────────────────────────────────────────────────────────┘
                                  │
                                  ▼
┌────────────────────────────── 核心業務模組 ─────────────────────────┐
│ four_pillars_destiny/     │ purple_star_astrology/                 │
│ 四柱八字 / 四柱批命       │ 紫微斗數                                │
│                                                                    │
│ hexagram_divination/      │ auspicious_date/                       │
│ 易經解卦                  │ 擇日合婚                                │
│                                                                    │
│ esoteric_numerology/      │ nameology/                             │
│ 鐵板神數 / 邵子神數       │ 姓名號碼 / 西文數理                     │
└────────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌────────────────────────────── 支撐層 ───────────────────────────────┐
│ lunar_solar/                                                        │
│ ├─ 陽曆 / 農曆轉換                                                  │
│ ├─ 節氣、干支、EightChar、大運、流年、流月                          │
│ └─ 為四柱、紫微、擇日、姓名等模組提供底層日期計算                    │
│                                                                    │
│ character_case/                                                     │
│ ├─ database_manager.py: SQLite 資料庫管理                           │
│ ├─ case_manager_widget.py: 案例管理介面                              │
│ ├─ dialogs/: 不同術數系統嘅案例輸入/編輯彈窗                         │
│ └─ unified_formatter.py: Markdown/TXT 匯出                          │
│                                                                    │
│ ai/                                                                │
│ ├─ ai_analysis.py: AI 分析 UI、執行緒、快取同專題流程                  │
│ ├─ config.py / .env: 供應商設定同本地 API Key                       │
│ ├─ analysis_graph.py: LangGraph 風格呼叫流程                        │
│ ├─ modern_prompts.py / prompt_manager.py: Prompt 契約同相容層        │
│ ├─ topic_schema.py: 報告專題拆分規則                                │
│ └─ providers/: OpenAI-compatible / Claude / Gemini / Qwen 客户端     │
└────────────────────────────────────────────────────────────────────┘
```

主流程：

1. `mainAppUI.py` 建立穩定嘅分頁桌面端；`mainAppUI_modern.py` 建立註冊表驅動嘅現代化外殼。
2. 各業務 Widget 收集輸入，呼叫對應核心分析類，例如 `BzMs`、`ZwMs`、`LyMs`、`ZrMs`、`Nm`。
3. 長計算透過 `ui_common.shared_ui.WorkerThread` 放到背景執行，结果進入 `ResultDialog`。
4. 结果可以儲存為案例、匯出 Markdown/TXT、進入 AI 專題解讀，或者透過案例管理再次回填到模組介面。
5. `lunar_solar/` 作為底層曆法引擎，被四柱、紫微、擇日、姓名等多個模組複用。

## 倉庫規模

按而家本地倉庫統計，不含 `.git`、`__pycache__`、`.pytest_cache` 同 `.vscode`：

- Python 文件：`168`
- Python 行數：`95,418`
- JSON 文件：`447`
- `four_pillars_destiny/`：`11` 個 Python 文件，約 `28,844` 行，`15` 個 JSON
- `purple_star_astrology/`：`14` 個 Python 文件，約 `10,439` 行，`20` 個 JSON
- `nameology/`：`11` 個 Python 文件，約 `6,462` 行，`391` 個 JSON
- `ai/`：`15` 個 Python 文件，約 `6,812` 行
- `lunar_solar/`：`42` 個 Python 文件，約 `7,370` 行

### 工程目錄統計

| 模組 | Python 檔案數 | Python 行數 | JSON 檔案數 |
|---|---:|---:|---:|
| 根目錄入口 (`mainAppUI.py` / `mainAppUI_modern.py` / `mainWebUI.py`) | 3 | 3,317 | 0 |
| `ai/` | 15 | 6,812 | 0 |
| `auspicious_date/` | 5 | 6,486 | 0 |
| `character_case/` | 15 | 5,621 | 0 |
| `esoteric_numerology/` | 10 | 8,131 | 5 |
| `four_pillars_destiny/` | 11 | 28,844 | 15 |
| `hexagram_divination/` | 9 | 4,024 | 15 |
| `lunar_solar/` | 42 | 7,370 | 0 |
| `nameology/` | 11 | 6,462 | 391 |
| `purple_star_astrology/` | 14 | 10,439 | 20 |
| `ui_common/` | 7 | 1,766 | 0 |
| `web_platform/` | 14 | 2,632 | 1 |
| `tests/` | 11 | 2,923 | 0 |
| `README/` 工具脚本 | 1 | 591 | 0 |

統計指令範例：

```bash
find . -name '*.py' -not -path './.git/*' -not -path '*/__pycache__/*' -not -path './.pytest_cache/*' | wc -l
find . -name '*.json' -not -path './.git/*' -not -path '*/__pycache__/*' -not -path './.pytest_cache/*' -not -path './.vscode/*' | wc -l
```

## 子模組文件導航

| 模組 | README | 主要職責 | 桌面端入口 |
|---|---|---|---|
| 四柱八字 | `four_pillars_destiny/README.md` | 八字原局、大運、流年、流月、干支手輸同古籍規則數據。 | `四柱八字` / `四柱批命` |
| 紫微斗數 | `purple_star_astrology/README.md` | 紫微排盤、十二宮、星曜組合、大限、流年同排盤圖。 | `紫微斗數` |
| 易經解卦 | `hexagram_divination/README.md` | 六爻起卦、流年解卦、小六壬、諸葛神數等輔助斷法。 | `易經解卦` |
| 擇日合婚 | `auspicious_date/README.md` | 萬年曆、主題擇日、吉凶日篩選、合婚參考。 | `擇日合婚` |
| 姓名號碼 | `nameology/README.md` | 中文姓名學、五格三才、起名、測字、號碼、西文數理。 | `姓名號碼` |
| 數理神數 | `esoteric_numerology/README.md` | 鐵板神數、邵子神數、太素/太玄數字推演。 | `鐵板神數` / `邵子神數` |
| 案例管理 | `character_case/README.md` | SQLite 案例庫、分類、搜尋、備註、JSON/Excel 匯入匯出。 | `案例管理` |
| 陰陽曆引擎 | `lunar_solar/README.md` | 公曆農曆互轉、節氣、干支、八字、九星、佛曆道曆。 | 底層支撑 |
| 通用 UI | `ui_common/README.md` | 共享執行緒、结果彈窗、現代化外殼、模組注册、導航同圖标主題。 | 底層支撑 |
| Web 平台 | `web_platform/README.md` | FastAPI/Vue Web 平台、後端介面、前端頁面同部署结構。 | Web 入口 |

## 安裝同啟動

```bash
pip install -r requirements.txt
python mainAppUI.py
```

其他入口：

```bash
python mainAppUI_modern.py
python mainWebUI.py
python web_platform/backend/app.py
```

測試同檢查：

```bash
python tests/test_jieqi_interval.py
python tests/test_unified_formatter_markdown.py
pytest tests
```

AI 能力需要在 `AI/.env` 或系統環境變數中設定對應供應商金鑰。唔好提交真實 API Key。

## 免責聲明

MetaphysicsQuant 用于傳統文化數碼化、規則工程、軟件架構實踐同研究展示。項目輸出來自程式規則、數據文件同 AI 總結，唔構成醫療、法律、投資、婚姻或其他現實決策建議。傳統術數內容應作為文化研究同個人參考，唔應該替代專業意見或事實調查。
