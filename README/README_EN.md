# MetaphysicsQuant - Engineering-Oriented Chinese Metaphysics Analysis Platform

<p align="center">
  <a href="../README.md">Main</a> |
  <a href="./README_CN.md">简体中文</a> |
  <a href="./README_ZH_TW.md">繁體中文</a> |
  <a href="./README_YUE.md">粵語</a> |
  <a href="./README_EN.md">English</a>
</p>

> **Showcase Notice**: This repository is only for project introduction and results showcase. It does not include project source code, data files, the case database, or API configuration.

MetaphysicsQuant is not just a chart-rendering tool for BaZi, Zi Wei Dou Shu, or hexagrams. It turns the hardest parts of traditional Chinese metaphysics into runnable software: calendar conversion, GanZhi derivation, symbolic-rule engines, classical text lookups, topic-based long-form reports, AI-assisted interpretation, SQLite case management, Markdown/TXT export, and a complete desktop workflow.

The stable mainline is the PySide6 desktop app in `mainAppUI.py`. `mainAppUI_modern.py` is a registry-driven modern shell. `mainWebUI.py` and `web_platform/` are retained as Web-oriented code paths.

Last updated: 2026-05-03

## Table of Contents

- [What It Can Do](#what-it-can-do)
- [Interface Screenshots](#interface-screenshots)
- [BaZi: Core Showcase](#bazi-core-showcase)
- [Other Metaphysics Modules](#other-metaphysics-modules)
- [AI Analysis and Reports](#ai-analysis-and-reports)
- [Case Management and Export](#case-management-and-export)
- [Engineering Value](#engineering-value)
- [Architecture](#architecture)
- [Repository Scale](#repository-scale)
- [Subsystem Documentation Index](#subsystem-documentation-index)
- [Installation and Startup](#installation-and-startup)
- [Disclaimer](#disclaimer)

## What It Can Do

The project is best understood as a traditional metaphysics knowledge base plus a rule engine plus a desktop analysis system. Its main value is converting rules scattered across classics, folk formulas, and modern charting practice into reproducible, inspectable, savable program output.

Implemented practical capabilities:

| Capability | Implemented Scope |
|---|---|
| BaZi / Four Pillars | Numeric birth-time charting, manual GanZhi input, natal chart, luck cycles, annual/monthly analysis, TaiYuan, MingGong, ShenGong, seven-pillar topic reports, ChuanGongYaYun, Zi Wei linkage. |
| Symbolic stars and patterns | `SZBZ_1Gz.py` contains 330 methods, about 180 of which directly relate to symbolic stars, auspicious/inauspicious patterns, combinations, conflicts, and ChuanGongYaYun logic. |
| Classical rule data | The BaZi data layer covers San Ming Tong Hui, Di Tian Sui, Qiong Tong Bao Jian, Shen Feng Tong Kao, Wu Xing Jing Ji, Gui Gu Zi, Yuan Tiangang bone-weighting, and more. |
| Zi Wei Dou Shu | Twelve-palace charting, major/minor stars, transformations, star brightness, decade cycles, annual/monthly charts, chart image export, and star-combination matching. |
| I Ching / Liu Yao | Time-based casting, three-number casting, XuanShu casting, original/changed hexagrams, moving lines, six relatives, six spirits, Shi/Ying, NaJia, and 64-hexagram materials. |
| Auspicious Date | Almanac output, yearly calendar output, topic-based date selection, marriage, job/career, business opening, wealth, travel, medical, moving, study, childbirth, and marriage-matching references. |
| Nameology | Chinese nameology, Kangxi/Xinhua stroke modes, Five Grids, Three Talents, 81-number meanings, personal naming, company naming, character divination, and number analysis. |
| English Numerology | Combined Pythagorean, Cheiro/Chaldean, and Vedas reports for English names and selected-year analysis. |
| Esoteric numerology | Tie Ban Shen Shu, Shao Zi Shen Shu, and Tai Su/Tai Xuan-style number derivation, with text lookup, natal analysis, luck cycles, annual analysis, and comprehensive reports. |
| Case system | SQLite case database, categories, search, notes, reload into modules, JSON/Excel import/export, Markdown/TXT report export. |
| AI interpretation | Splits generated reports by topic and calls OpenAI-compatible, Claude, Gemini, OpenRouter, DeepSeek, Qwen, SiliconFlow, and related providers. |

The output is not a short "good or bad" verdict. It is expandable structured material. Existing BaZi natal report samples in the repository reach the 30,000-character range and include chart data, seven-pillar topics, classical excerpts, symbolic-star combinations, luck-cycle material, and AI interpretation entry points. The project provides traceable rule output; users still need to evaluate any interpretation against real-world context.

## Interface Screenshots

The screenshots below come from the current desktop application and show the main topic modules in use.

<table>
  <tr>
    <td align="center"><strong>BaZi / Four Pillars</strong><br><img src="../image/four_pillars_destiny.png" alt="BaZi interface" width="900"></td>
  </tr>
  <tr>
    <td align="center"><strong>Zi Wei Dou Shu</strong><br><img src="../image/purple_star_astrology.png" alt="Zi Wei Dou Shu interface" width="900"></td>
  </tr>
  <tr>
    <td align="center"><strong>I Ching / Liu Yao</strong><br><img src="../image/hexagram_divination.png" alt="I Ching interface" width="900"></td>
  </tr>
  <tr>
    <td align="center"><strong>Auspicious Date</strong><br><img src="../image/auspicious_date.png" alt="Auspicious date interface" width="900"></td>
  </tr>
  <tr>
    <td align="center"><strong>Nameology</strong><br><img src="../image/nameology.png" alt="Nameology interface" width="900"></td>
  </tr>
  <tr>
    <td align="center"><strong>Tie Ban / Shao Zi</strong><br><img src="../image/esoteric_numerology.png" alt="Esoteric numerology interface" width="900"></td>
  </tr>
  <tr>
    <td align="center"><strong>Case Management</strong><br><img src="../image/character_case.png" alt="Case management interface" width="900"></td>
  </tr>
</table>

## BaZi: Core Showcase

BaZi / Four Pillars is the heaviest core module in this repository: `four_pillars_destiny/` has about 28.8k lines of Python and 15 JSON data files. Its value is not merely displaying the eight characters, but organizing the rule system after the chart has been computed.

### 1. Two Workflows

- `四柱八字`: accepts name, gender, solar/lunar date, hour, and minute; computes the Four Pillars, luck-cycle start, DaYun, LiuNian, and LiuYue.
- `四柱批命`: accepts manual year/month/day/hour pillars, DaYun, LiuNian, XiaoXian, and LiuYue; useful for classical case studies, known-chart reverse lookup, and teaching.

### 2. GanZhi Foundation

`four_pillars_destiny/SZBZ_1Gz.py` is the rule foundation of the BaZi system. It covers:

- Heavenly stems, earthly branches, hidden stems, five elements, yin/yang, the 60 JiaZi, NaYin, and XunKong.
- Ten Gods, twelve growth stages, LuMing growth stages, NaYin growth stages, and the four noble/neutral/unfavorable categories.
- A wide range of symbolic-star and pattern checks, including TianYi Nobleman, FuXing Nobleman, TaiJi Nobleman, WenChang Nobleman, TianDe, YueDe, TianXi, YiMa, HuaGai, JinYu, XueTang, CiGuan, JieLu KongWang, GuiMenGuan, MuYu Sha, BaoBai, ZiYi, SiFei, GuanFu, SiFu, BingFu, XueGuang, LiXiang, JieSha, WangShen, YangRen, YuanChen, KongWang, XianChi, TianLuo/DiWang, GuChen/GuaSu, and many more.
- ChuanGongYaYun twelve spirits: TaiSui, QingLong, SangMen, LiuHe, GuanFu, XiaoHao, DaHao, ZhuQue, BaiHu, GuiShen, DiaoKe, and BingFu, including transformation rules.
- Blind-school and folk-experience checks such as SiQiong day, ZhuangSha, LuoSha, JiSha, BaBai, XuanLiangSha, BaoTaiSha, TieXingSha, TianSao, DiSao, ZhuiHun, and ChanDu.

This is one of the strongest project-showcase points: the rules are not UI copy. They are implemented as functions and data structures.

### 3. Seven-Pillar Analysis

`four_pillars_destiny/SZBZ_2Bz.py` goes beyond the traditional year/month/day/hour pillars by adding TaiYuan, MingGong, and ShenGong, forming a seven-pillar analysis perspective. Reports are organized by topic:

- Personality
- Study and education
- Career
- Wealth
- Formula-based rules
- Marriage
- Family and relatives: father, mother, siblings, children, and other relatives
- Injury and health
- Yang residence and Yin residence

These topics are layered by source instead of forcing a single school of interpretation. The code combines Su-style blind school, folk blind-school rules, Wu Xing Jing Ji, San Ming Tong Hui, Yu Zhao Shen Ying Zhen Jing, Liang-school theory, Gui Gu Zi Fen Ding Jing, San Shi Yan Qin, and more. The project emphasizes traceable rule output rather than pretending to replace real-world judgment.

### 4. Classical and Data Sources

The BaZi `data/` directory stores rule and text data from multiple sources:

- `SanMingTongHui.json`: San Ming Tong Hui
- `DiTianSui.json`: Di Tian Sui
- `QiongTongBaoJian.json`: Qiong Tong Bao Jian
- `ShenFengTongKao.json`: Shen Feng Tong Kao
- `WuXingJingJi.json`: Wu Xing Jing Ji
- `GuiGuZi_LTQ.json`, `GuiGuZi_MGB.json`: Gui Gu Zi Fen Ding Jing and Gui Gu Zi Ming Gong table
- `YuanTiangangCG.json`: Yuan Tiangang bone-weighting
- `SanShiYanQin.json`: San Shi Yan Qin
- `SuShiMangPai.json`: Su-style blind school
- `DaMoYiZhangJing.json`, `JueFa.json`, `Books.json`, and other supplementary data

The code also references or implements rule names from Yuan Hai Zi Ping, Lan Tai Miao Xuan, Yu Zhao Shen Ying Zhen Jing, Yong Le Da Dian, Tian Yuan Wu Xian Jing, and related traditions. In practical showcase terms: this is a software project that merges classical texts, formulas, and programmatic rules into topic-based reports.

### 5. Report Types

The BaZi wrapper `SZBZ_6BzMs.py` supports:

- Natal report: `bzms_num()` / `bzms_gz()`
- Short natal report: `bzmss_num()`
- DaYun report: `dyms_num()` / `dyms_gz()`
- LiuNian report: `lnms_num()` / `lnms_gz()`
- LiuYue report: `lyms_num()` / `lyms_gz()`
- Ten-year annual mid report from the current year: `zpln_num()`
- Segmented DaYun/LiuNian handoff logic and LiuYue/DaYun handoff logic
- Optional Zi Wei Dou Shu linkage for natal, decade, and annual chart images

Existing anonymized sample reports include `character_case/CaseReports/sample_case/sample_case_四柱八字_原局分析_20260421_043836.md`, about 36k characters, and `character_case/CaseReports/A参考模板/sample_case_四柱八字_原局分析_20260421_031317.txt`, about 30k characters. This demonstrates that the system can generate long structured reports in practice, not only in design.

## Other Metaphysics Modules

### Zi Wei Dou Shu

`purple_star_astrology/` implements twelve-palace charting, major/minor/miscellaneous stars, transformations, star brightness, decade cycles, annual/monthly charts, and chart rendering. `Star_Combination_Matcher.py` reads JSON data to match single-star, combination-star, and gender-specific interpretations. Topic data covers personality, wealth, marriage, career, health, father, mother, siblings, children, property, migration, friends, and more.

### I Ching and Liu Yao

`hexagram_divination/` supports time-based casting, three-number casting, XuanShu, manual hexagram input, original and changed hexagrams, moving lines, six relatives, Shi/Ying, six spirits, NaJia, and annual hexagram analysis. `notion/` stores 64 Markdown hexagram documents, while `data/` stores I Ching material, Xiao Liu Ren, Zhuge numerology, GanZhi numerology, TaiJi numerology, YaPai numerology, and related mappings.

### Auspicious Date and Marriage Matching

`auspicious_date/` is not a simple almanac lookup. It filters dates by topic. Implemented topics include marriage, proposal/name inquiry, bed placement, taking office, public duty, business opening, wealth seeking, contract/trade, vehicle pickup, banquets, study, examinations, enrollment, apprenticeship, travel, medical treatment, moving, ritual worship, and childbirth. The rules reference Xie Ji Bian Fang Shu, Yu Xia Ji, and other folk date-selection materials.

### Nameology and Numerology

`nameology/` covers Chinese nameology and English numerology:

- Chinese nameology: Kangxi/Xinhua strokes, Five Grids, Three Talents, 81-number meanings, five elements, yin/yang, zodiac, and topic interpretations.
- Naming: personal and company naming with preferred/avoided elements and industry data.
- Character and number analysis: three-character divination plus phone, license plate, and identifier analysis.
- English numerology: combined Pythagorean, Cheiro/Chaldean, and Vedas output.
- Data layer: character dictionaries, Kangxi/Xinhua stroke data, Three Talents, Five Grids, 81-number meanings, industry data, English numerology references, and naming corpora from Shi Jing, Chu Ci, Lun Yu, Tang poetry, Song poetry, and Song Ci.

### Tie Ban, Shao Zi, Tai Su, and Tai Xuan

`esoteric_numerology/` provides Tie Ban Shen Shu, Shao Zi Shen Shu, and Tai Su/Tai Xuan-style number derivation. This differs from English numerology and focuses on birth data, GanZhi, time刻分, hexagrams, sound/number derivation, and text lookup. Shao Zi supports natal, DaYun, LiuNian, and comprehensive reports. Tie Ban supports刻分, calibration, and text output.

## AI Analysis and Reports

The project does not treat AI as a mystical decision maker. AI sits at the end of the engineering pipeline: the rule engine first generates traceable raw material, then the AI layer splits it by topic and helps summarize, interpret, and turn it into practical advice.

The `ai/` module includes:

- Provider abstraction: OpenAI, Claude, Google Gemini, OpenRouter, DeepSeek, DashScope Qwen, and SiliconFlow.
- OpenAI-compatible support for OpenRouter, DeepSeek, SiliconFlow, and compatible chat/completions endpoints.
- LangChain/LangGraph-style workflow when optional dependencies are available, with REST fallback when they are not.
- Topic splitting: `topic_schema.py` handles different report structures for natal charts, luck cycles, annual reports, monthly reports, and Shao Zi reports.
- Prompt management: `modern_prompts.py` and `prompt_manager.py` constrain output toward practical advice, risk boundaries, and evidence grounding instead of fortune-teller-style language.
- Key management: real API keys should live in `AI/.env` or environment variables, not in Git.

The showcase value is clear: this is not just a metaphysics script. It is a traditional rule engine combined with modern LLM workflow design.

## Case Management and Export

`character_case/` is the unified case system. The default database is `character_case/cases.db`. It turns one-off calculation into long-term research and archiving:

- Saves cases for BaZi, BaZi manual input, Zi Wei Dou Shu, I Ching hexagrams, auspicious date, nameology, Tie Ban Shen Shu, and Shao Zi Shen Shu.
- Supports categories, search, notes, ordering, drag-and-drop, and editing.
- Reloads saved cases back into the corresponding analysis module.
- Supports JSON backup and Excel import/export.
- `unified_formatter.py` formats analysis output into Markdown or TXT and includes system-specific formatting for BaZi, Zi Wei, Liu Yao, and Shao Zi.

Note: `character_case/cases.db` is local user data and should not be overwritten or deleted casually.

## Engineering Value

Technical strengths demonstrated by this project:

- PySide6 desktop app: stable entry point `mainAppUI.py`, modern shell `mainAppUI_modern.py`.
- Modular architecture: metaphysics modules, calendar engine, case management, AI layer, and shared UI are separated.
- Rule engine design: large traditional rule sets are represented as readable functions, tables, and JSON data.
- Calendar foundation: `lunar_solar/` provides solar/lunar conversion, solar terms, GanZhi, EightChar, DaYun, LiuNian, and LiuYue foundations.
- Background execution: shared `WorkerThread` avoids blocking the UI during analysis.
- Persistence: SQLite for case management, JSON/Excel for interchange.
- Report engineering: Markdown/TXT formatting, topic splitting, AI analysis dialogs, and close-protection for active result windows.
- Web migration groundwork: `web_platform/` keeps FastAPI, Vue, and deployment configuration for a possible Web platform.

## Architecture

MetaphysicsQuant is structured around one desktop entry layer, independent metaphysics engines, and shared support layers for calendar logic, case management, AI, and UI utilities. Each system can run as an independent module while still sharing case storage, export formatting, and AI topic interpretation.

```text
┌──────────────────────────── Presentation Layer ────────────────────────────┐
│ mainAppUI.py                                                               │
│ ├─ Case Manager                                                            │
│ ├─ BaZi / Four Pillars                                                     │
│ ├─ Zi Wei Dou Shu                                                          │
│ ├─ I Ching / Liu Yao                                                       │
│ ├─ Auspicious Date                                                         │
│ ├─ Nameology                                                               │
│ ├─ Tie Ban Shen Shu                                                        │
│ ├─ Shao Zi Shen Shu                                                        │
│ └─ Manual BaZi Input                                                       │
│                                                                            │
│ mainAppUI_modern.py                                                        │
│ └─ ModernMainWindow + NavigationSidebar + module_registry                  │
└────────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────── Shared Interaction / UI Layer ─────────────────────┐
│ ui_common/                                                                 │
│ ├─ shared_ui.py: WorkerThread, TranslationThread, ResultDialog              │
│ ├─ app_shell.py: modern shell, case linkage, close protection               │
│ ├─ module_registry.py: module registration, grouping, case routing          │
│ ├─ navigation.py: sidebar navigation                                        │
│ └─ case_notes.py: case notes dialog                                         │
└────────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌────────────────────────────── Core Business Modules ───────────────────────┐
│ four_pillars_destiny/        │ purple_star_astrology/                      │
│ BaZi / Manual BaZi Input     │ Zi Wei Dou Shu                              │
│                                                                            │
│ hexagram_divination/         │ auspicious_date/                            │
│ I Ching / Liu Yao            │ Auspicious Date / Marriage Matching         │
│                                                                            │
│ esoteric_numerology/         │ nameology/                                  │
│ Tie Ban / Shao Zi            │ Chinese Nameology / English Numerology      │
└────────────────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────── Support Layer ─────────────────────────────┐
│ lunar_solar/                                                               │
│ ├─ solar / lunar conversion                                                 │
│ ├─ solar terms, GanZhi, EightChar, DaYun, LiuNian, LiuYue                   │
│ └─ shared date foundation for BaZi, Zi Wei, date selection, nameology       │
│                                                                            │
│ character_case/                                                            │
│ ├─ database_manager.py: SQLite database management                          │
│ ├─ case_manager_widget.py: case management UI                               │
│ ├─ dialogs/: case input/edit dialogs for different systems                  │
│ └─ unified_formatter.py: Markdown/TXT export                                │
│                                                                            │
│ ai/                                                                        │
│ ├─ ai_analysis.py: AI analysis UI, threads, cache, topic workflow           │
│ ├─ config.py / .env: provider configuration and local API keys              │
│ ├─ analysis_graph.py: LangGraph-style workflow                              │
│ ├─ modern_prompts.py / prompt_manager.py: prompt contracts and compatibility│
│ ├─ topic_schema.py: report topic splitting rules                            │
│ └─ providers/: OpenAI-compatible / Claude / Gemini / Qwen clients           │
└────────────────────────────────────────────────────────────────────────────┘
```

Main flow:

1. `mainAppUI.py` builds the stable tabbed desktop app. `mainAppUI_modern.py` builds the registry-driven modern shell.
2. Business widgets collect user input and call core classes such as `BzMs`, `ZwMs`, `LyMs`, `ZrMs`, and `Nm`.
3. Long-running calculations execute through `ui_common.shared_ui.WorkerThread`; results are shown in `ResultDialog`.
4. Results can be saved as cases, exported as Markdown/TXT, sent to AI topic analysis, or reloaded from case management.
5. `lunar_solar/` is the shared calendar engine reused by BaZi, Zi Wei, date selection, nameology, and related modules.

## Repository Scale

Current local statistics, excluding `.git`, `__pycache__`, `.pytest_cache`, and `.vscode`:

- Python files: `168`
- Python lines: `95,418`
- JSON files: `447`
- `four_pillars_destiny/`: `11` Python files, about `28,844` lines, `15` JSON files
- `purple_star_astrology/`: `14` Python files, about `10,439` lines, `20` JSON files
- `nameology/`: `11` Python files, about `6,462` lines, `391` JSON files
- `ai/`: `15` Python files, about `6,812` lines
- `lunar_solar/`: `42` Python files, about `7,370` lines

### Directory Metrics

| Module | Python Files | Python Lines | JSON Files |
|---|---:|---:|---:|
| Root entry points (`mainAppUI.py` / `mainAppUI_modern.py` / `mainWebUI.py`) | 3 | 3,317 | 0 |
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
| `README/` tooling | 1 | 591 | 0 |

Example statistics commands:

```bash
find . -name '*.py' -not -path './.git/*' -not -path '*/__pycache__/*' -not -path './.pytest_cache/*' | wc -l
find . -name '*.json' -not -path './.git/*' -not -path '*/__pycache__/*' -not -path './.pytest_cache/*' -not -path './.vscode/*' | wc -l
```

## Subsystem Documentation Index

| Module | README | Scope | Desktop Page |
|---|---|---|---|
| BaZi / Four Pillars | `four_pillars_destiny/README.md` | Natal chart, DaYun, LiuNian, LiuYue, manual pillars, and classical rule data. | `四柱八字` / `四柱批命` |
| Zi Wei Dou Shu | `purple_star_astrology/README.md` | Zi Wei charting, palaces, star combinations, decade cycles, annual charts, chart images. | `紫微斗数` |
| I Ching Hexagram | `hexagram_divination/README.md` | Hexagram casting, Liu Yao, annual analysis, Xiao Liu Ren, and auxiliary numerology. | `易经解卦` |
| Auspicious Date | `auspicious_date/README.md` | Almanac, topic-based date selection, good/bad day filters, marriage matching. | `择日合婚` |
| Nameology | `nameology/README.md` | Chinese nameology, Five Grids, naming, character divination, number analysis, English numerology. | `姓名号码` |
| Esoteric Numerology | `esoteric_numerology/README.md` | Tie Ban Shen Shu, Shao Zi Shen Shu, Tai Su/Tai Xuan number derivation. | `铁板神数` / `邵子神数` |
| Case Manager | `character_case/README.md` | SQLite cases, categories, search, notes, JSON/Excel import and export. | `案例管理` |
| Calendar Engine | `lunar_solar/README.md` | Solar/lunar conversion, solar terms, GanZhi, EightChar, Nine Star, Buddhist/Taoist calendar data. | Foundation |
| Shared UI | `ui_common/README.md` | Shared threads, result dialogs, modern shell, module registry, navigation, icons. | Foundation |
| Web Platform | `web_platform/README.md` | FastAPI/Vue Web platform, backend APIs, frontend, and deployment structure. | Web |

## Installation and Startup

```bash
pip install -r requirements.txt
python mainAppUI.py
```

Other entry points:

```bash
python mainAppUI_modern.py
python mainWebUI.py
python web_platform/backend/app.py
```

Tests and checks:

```bash
python tests/test_jieqi_interval.py
python tests/test_unified_formatter_markdown.py
pytest tests
```

AI features require provider keys in `AI/.env` or environment variables. Do not commit real API keys.

## Disclaimer

MetaphysicsQuant is intended for traditional-culture digitization, rule engineering, software architecture practice, and research demonstration. Outputs come from program rules, data files, and AI summaries. They do not constitute medical, legal, investment, marriage, or other real-world professional advice. Traditional metaphysics content should be treated as cultural research and personal reference, not as a substitute for professional judgment or factual investigation.
