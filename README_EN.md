# MetaphysicsQuant
**Engineering Traditional Chinese Metaphysics into Software**

<p align="center">
  <a href="README.md">简体中文</a> |
  <a href="README_EN.md">English</a>
</p>

<p align="center">
  <a href="https://img.shields.io/github/stars/lyzhk/MetaphysicsQuant?style=for-the-badge"><img alt="GitHub stars" src="https://img.shields.io/github/stars/lyzhk/MetaphysicsQuant?style=for-the-badge"></a>
  <a href="https://img.shields.io/github/forks/lyzhk/MetaphysicsQuant?style=for-the-badge"><img alt="GitHub forks" src="https://img.shields.io/github/forks/lyzhk/MetaphysicsQuant?style=for-the-badge"></a>
  <a href="https://img.shields.io/badge/Python-3.10%2B-3776AB?style=for-the-badge&logo=python&logoColor=white"><img alt="Python 3.10+" src="https://img.shields.io/badge/Python-3.10%2B-3776AB?style=for-the-badge&logo=python&logoColor=white"></a>
</p>

> **Showcase Notice**
>
> This is a **public showcase repository**. It exists to present project scope, engineering design, UI results, and system architecture.
> It does **not** include source code, rule datasets, case databases, API configuration, or other private assets that would reproduce the full commercial capability.

## Overview

MetaphysicsQuant is a long-running software project that turns traditional Chinese metaphysics into an actual product system.

It is not just a chart-rendering utility or a collection of isolated scripts. It takes knowledge that is usually scattered across:

- classical texts
- formulas and mnemonic rules
- table-driven traditions
- folk schools and practice notes
- modern chart-reading habits

and converts that knowledge into:

- executable rule engines
- maintainable JSON and structured data layers
- a reusable calendar and GanZhi foundation
- a persistent case-management workflow
- structured long-form reports
- AI-assisted topic interpretation
- a unified desktop product experience

The shortest accurate description is:

> **A desktop-first traditional metaphysics analysis platform that converts knowledge-dense classical rule systems into executable software, structured reports, reusable case workflows, and AI-assisted interpretation pipelines.**

## Why This Project Is Hard

The hard part is not the UI. The hard part is turning knowledge systems into software.

Traditional metaphysics software has a few recurring problems:

- rules are distributed across books, hand-copied notes, and school-specific expressions
- different systems are highly sensitive to time boundaries, calendar logic, and interpretive conventions
- outputs are rarely fixed fields; they are often long, topic-structured narratives
- users do not use the software once; they save, compare, reload, revise, and archive cases
- AI cannot be trusted to improvise unless a reliable rule layer exists first

MetaphysicsQuant addresses those problems in the correct order:

- rule systems first
- structured reports next
- persistent cases after that
- AI interpretation on top of traceable outputs

That order matters. It is what makes the project feel like software engineering rather than prompt theater.

## Scale Snapshot

These numbers come from the private implementation repository. The public showcase repository does not include the implementation files.

| Metric | Current Scale |
|---|---:|
| Python files | 181 |
| Python lines | 91,824 |
| JSON files | 448 |
| Four Pillars module | 12 Python files, 16 JSON files |
| Zi Wei Dou Shu module | 15 Python files, 20 JSON files |
| Nameology module | 11 Python files, 391 JSON files |
| Calendar foundation | 42 Python files |
| AI layer | 38 Python files |

This is not a single-file demo. It is a layered repository with a real data footprint, real rule density, and visible long-term evolution.

## Feature Overview

| Module | Scope |
|---|---|
| Four Pillars / BaZi | Numeric charting, manual GanZhi input, natal analysis, DaYun, LiuNian, LiuYue, TaiYuan, MingGong, ShenGong, seven-pillar analysis, Zi Wei linkage |
| Zi Wei Dou Shu | Twelve-palace charting, major/minor stars, transformations, star brightness, decade cycles, annual/monthly overlays, chart rendering, combination matching |
| I Ching / Liu Yao | Time-based casting, three-number casting, XuanShu input, manual hexagram input, original/changed hexagrams, moving lines, six relatives, six spirits, Shi/Ying, NaJia, annual interpretation |
| Auspicious Date | Almanac output, lunar-year output, 70+ topic-based date-selection flows, marriage, official affairs, construction, travel, finance, moving, burial, compatibility |
| Nameology | Chinese nameology, Five Grids, Three Talents, 81-number meanings, personal naming, company naming, character divination, number analysis |
| Western Numerology | Combined Pythagorean, Cheiro/Chaldean, and Vedas reports |
| Esoteric Numerology | Tie Ban Shen Shu, Shao Zi Shen Shu, natal analysis, DaYun, LiuNian, integrated reports |
| Case System | SQLite case database, categories, search, notes, import/export, report export, reload into analysis views |
| AI Topic Analysis | Report splitting, provider abstraction, prompt routing, model invocation, interpretation, practical advice |

## Key Module Breakdown

### 1. Four Pillars / BaZi: the densest rule-engine module

The Four Pillars module is the heaviest core in the entire project. Its value is not simply "calculating eight characters." Its value is what happens after the chart has been generated.

It covers:

- solar/lunar birth time to Four Pillars
- manual year/month/day/hour pillar input
- natal analysis, DaYun, LiuNian, and LiuYue
- TaiYuan, MingGong, ShenGong, and seven-pillar extended perspective
- optional linkage to Zi Wei Dou Shu chart windows

The deeper point is rule density. The underlying classes contain hundreds of rule functions directly used for:

- symbolic star detection
- pattern identification
- combination, conflict, punishment, and transformation logic
- ChuanGongYaYun handling
- mapping classical texts and folk rules into program output

This is one of the best parts of the project to showcase because it is clearly not CRUD. It is knowledge-dense rule modeling.

The `data/` directory in the Four Pillars module also preserves a large body of classical and derived rule material, including:

- `SanMingTongHui.json`
- `DiTianSui.json`
- `QiongTongBaoJian.json`
- `ShenFengTongKao.json`
- `WuXingJingJi.json`
- `GuiGuZi_LTQ.json`
- `GuiGuZi_MGB.json`
- `YuanTiangangCG.json`
- `SanShiYanQin.json`
- `SuShiMangPai.json`
- `DaMoYiZhangJing.json`
- `JueFa.json`
- `Books.json`

The implementation also directly references or encodes materials associated with traditions such as:

- Yuan Hai Zi Ping
- Lan Tai Miao Xuan
- Yu Zhao Shen Ying Zhen Jing
- Yong Le Da Dian
- Tian Yuan Wu Xian Jing

The accurate showcase phrasing is not "I built a BaZi calculator." It is:

> **I built a software system that merges classical texts, formulas, folk rule systems, and programmatic inference into structured topic-based reports.**

### 2. Zi Wei Dou Shu: graphical charting plus data-driven interpretation

The Zi Wei Dou Shu module is not only about producing a chart. It is also about maintaining interpretation data cleanly and presenting the chart visually as a usable desktop component.

Its main capabilities include:

- twelve-palace chart generation
- major stars, supporting stars, miscellaneous stars, and transformations
- brightness states such as temple / prosperous / useful / neutral / fallen
- natal, decade, annual, and monthly views
- chart windows for natal, decade, annual, and monthly layers
- gender-aware combination matching

The engineering value here is threefold:

- moving interpretation logic from hardcoded conditions into JSON-backed data
- rendering complex chart structures as reusable GUI components
- separating chart display from interpretation data organization

### 3. I Ching / Liu Yao: multi-path interpretation instead of a single reading

The I Ching module combines casting logic with a supporting interpretation and materials system.

It supports:

- time-based casting
- three-number casting
- XuanShu input
- direct hexagram input
- original hexagram, changed hexagram, moving lines
- six relatives, six spirits, Shi/Ying, NaJia
- annual interpretation
- auxiliary systems such as Xiao Liu Ren, Zhuge numerology, GanZhi numerology, TaiJi numerology, and YaPai numerology

Its distinctive quality is that it does not stop at a single "hexagram result." It combines:

- rule-based hexagram structure
- classical hexagram material
- multiple auxiliary systems
- topic-oriented interpretation

### 4. Auspicious Date: topic modeling rather than almanac dumping

The Auspicious Date module is not a flat almanac browser. It turns traditional date-selection materials into a topic-based rule system.

Internally, it is organized around:

- affair groups
- topic names
- good/bad rule sets
- per-day signal evaluation
- date-range output

The current implementation covers four large groups and more than seventy topics, including examples such as:

- ritual and official topics
- marriage and household topics
- construction and finance topics
- travel, study, medicine, and burial topics

The important engineering point is not only topic count. It is the fact that the project converts traditional date-selection text into a structured, queryable, reusable rules layer.

### 5. Nameology and Western Numerology: a data-heavy module with both analysis and generation

The nameology module looks lighter on the surface than BaZi or Zi Wei, but it is extremely data-heavy and product-rich.

It covers:

- Chinese nameology
- Kangxi and Xinhua stroke modes
- Five Grids
- Three Talents
- 81-number meanings
- personal naming
- company naming
- character divination
- number analysis
- Western numerology in three systems

The personal naming flow is especially worth highlighting. It does not randomly generate names. It uses:

- corpora from Shi Jing, Chu Ci, Lun Yu, Zhou Yi, Tang poetry, Song Ci, and Song poetry
- stroke validation
- semantic scoring
- Three Talents and Five Grids validation
- phonetic and glyph rules
- candidate ranking and randomized display from a scored candidate pool

This is a good showcase for data engineering, rule design, and product interaction working together.

### 6. Tie Ban and Shao Zi: software representations of traditional numerical systems

These modules are structurally different from Western numerology. Their outputs depend heavily on:

- birth time
- GanZhi
- timing subdivisions
- rule texts
- hexagram and number mappings

The output is not a single number. It is a mix of:

- charts
- text lookup
- natal analysis
- DaYun analysis
- annual analysis
- integrated reports

These modules demonstrate that the product can host multiple traditional systems without collapsing into a mess of unrelated UIs.

## Method-Level Output Interfaces and Report Shapes by Module

The previous section is a project description. This section answers a more practical question:

> **What can each metaphysics module actually output?**

The answers below follow the same structure:

- wrapper class or primary implementation layer
- exposed output methods
- desktop actions
- visible artifacts
- current implementation status

### Four Pillars / BaZi

Primary wrapper:

- `four_pillars_destiny/SZBZ_6BzMs.py`

Main report methods:

- natal report: `bzms_num()` / `bzms_gz()`
- short natal report: `bzmss_num()`
- DaYun report: `dyms_num()` / `dyms_gz()`
- LiuNian report: `lnms_num()` / `lnms_gz()`
- LiuYue report: `lyms_num()` / `lyms_gz()`
- 10-year annual mid report from the current year: `zpln_num()`
- LiuNian / DaYun handoff logic: `get_ln2dy()`, `get_ln_num2dygz()`, `get_lnnum_dayun_gz_list()`
- LiuYue / DaYun handoff logic: `get_month_dayun_gz()`
- reverse lookup for possible birth date: `get_birth_date()`

Desktop actions in numeric-input mode:

- `bzms_analysis()`
- `bzmss_analysis()`
- `dyms_analysis()`
- `lnms_analysis()`
- `lyms_analysis()`
- `popup_result()`
- `show_chart_from_bazi()`

Desktop actions in manual GanZhi mode:

- `bzms_analysis()`
- `dyms_analysis()`
- `lnms_analysis()`
- `lyms_analysis()`

Visible report artifacts in the repository include anonymized outputs such as:

- `character_case/CaseReports/XXX/XXX_四柱八字_原局分析_20260421_043836.md`
  about `36,035` characters
- `character_case/CaseReports/A参考模板/XXX_四柱八字_原局分析_20260421_031317.txt`
  about `30,142` characters
- `character_case/CaseReports/XXX/XXX_四柱八字_流年分析_20260421_043844.md`
- `character_case/CaseReports/XXX/XXX_四柱八字_综合分析_20260516_211833.md`

For external readers, the right takeaway is:

- this module has a mature report tree
- it is not only a chart calculator
- it already produces long, archiveable, topic-structured outputs

### Zi Wei Dou Shu

Primary wrapper:

- `purple_star_astrology/ZWDS_6ZwMs.py`

Main report methods:

- natal topic report: `zwms_num()`
- twelve-palace report: `zwg12ms_num()`
- annual topic report: `zwlnms_num()`
- decade report placeholder: `zwdxms_num()`

Chart/UI method:

- unified chart dialog entry: `show_zwds_chart()`

The chart dialog supports:

- natal / decade / annual / monthly switching
- overlay controls
- image export

Desktop actions:

- `analysis()` for natal interpretation
- `g12_analysis()` for twelve-palace output
- `lnpd_analysis()` for annual interpretation
- `show_unified_chart()` for chart display
- `popup_result()` for the shared result dialog

Current implementation status matters here:

- the interface for decade output exists
- the widget still marks some decade/full-range actions as not yet implemented

That is worth being explicit about. It makes the README more credible, not less.

Publicly visible anonymized text-report samples for Zi Wei were not found in the case-report snapshot I checked during this update. For showcase purposes, Zi Wei is strongest when presented through:

- method-level interfaces
- chart rendering
- JSON-backed interpretation structure
- unified dialog design

### I Ching / Liu Yao

Primary wrapper:

- `hexagram_divination/LY_2Ms.py`

Main report methods:

- base reading: `lypd_ly()`
- annual reading: `lypd_ln()`
- full integrated reading: `lypd_all()`

Auxiliary interpretation methods include:

- `zypd_all()`
- `xlrpd_all()`
- `szsspd_all()`
- `gzsspd_all()`
- `zgsspd_all()`
- `tjsspd_all()`
- `ypsspd_all()`
- `get_ss_all(flag=5)`

So `lypd_all()` is not a shallow wrapper. It combines:

- hexagram structure output
- Zhou Yi textual interpretation
- Xiao Liu Ren
- four-character numerology
- multiple numerological side systems
- topic-based Liu Yao interpretation

Topic sections inside the Liu Yao reports include:

- personality and appearance
- study
- career
- wealth
- relationship
- relatives
- health
- yang residence
- yin residence

Desktop actions:

- `analysis_ly()`
- `analysis_ln()`
- `analysis_all()`
- `popup_result()`

Publicly visible anonymized examples include:

- `character_case/CaseReports/A参考模板/26.3.27 高岛法占是否坚持学易？_易经解卦_综合分析_20260421_032606.txt`
  about `6,751` characters
- `character_case/CaseReports/XXX公务员录取/XXX公务员录取_易经解卦_一卦多断_20260307_194357.txt`
  about `3,143` characters

Those files matter because they show the module already produces persistent report artifacts, not only on-screen output.

### Auspicious Date

Primary wrapper:

- `auspicious_date/ZR_3Ms.py`

Main methods:

- almanac output over a rolling range: `wan_nian_li_str()`
- full lunar-year output: `lunar_year_info_str(lunar_year)`
- topic-based date filtering: `get_topic_date(topic_key)`
- marriage compatibility reference: `get_marriage_compatibility()`
- topic metadata: `list_available_topics()`

Desktop actions:

- `analysis_selected_topic()`
- `analysis_lunar_year()`
- `analysis_compatibility()`
- `popup_result()`

What this really means in product terms is that the module supports four distinct output modes:

- rolling almanac
- lunar-year calendar
- topic-specific date selection
- compatibility reference

Current public case-report samples for this module were not found in the case-report snapshot used for this update. The honest showcase phrasing is therefore:

- the text-output methods and desktop flows are real
- the topic/rules structure is already deep
- currently visible public sample files are limited compared with BaZi, Liu Yao, and Shao Zi

### Nameology and Western Numerology

Primary Chinese nameology class:

- `nameology/Name_Ms.py`

Primary Western numerology entry:

- `nameology/Numerology_All.py`

Chinese nameology methods:

- `analyse_name()`
- `analyse_selected_year()`
- `generate_company_name()`
- `character_divination()`
- `analyse_number()`
- `generate_personal_name()`

Widget-level actions:

- `analyse_name()`
- `analyse_selected_year()`
- `generate_personal_name()`
- `generate_company_name()`
- `character_divination()`
- `analyse_number()`

English-name paths route through:

- `analyse_all_name(...)`
- `analyse_all_name_only(...)`
- `analyse_all_selected_year(...)`

This means the module is not purely analytical. It combines:

- analysis outputs
- generation outputs
- divination outputs
- object/number analysis

That mix makes it one of the strongest product-design modules in the repository.

Publicly visible case-report samples for this module were not found in the current public snapshot I checked. The best external framing is therefore:

- the methods and desktop workflow exist
- the generation pipeline is real
- the data layer is one of the largest in the codebase

### Tie Ban Shen Shu

Primary implementation:

- `esoteric_numerology/TBNUM_Ms.py`

Main methods:

- charting: `pp_sz()`
- natal analysis: `pd_sz()`
- annual analysis: `pd_ln()`

Desktop actions:

- `analysis_sz()`
- `analysis_ln()`

Current widget placeholders indicate that some broader flows still remain to be connected:

- `analysis_dy()`
- `analysis_all()`
- `analysis_popup()`

That is worth stating clearly. The right showcase wording is:

> **Tie Ban already has real natal and annual output flows, while broader all-in-one and decade-oriented desktop actions are still being expanded on top of the current architecture.**

### Shao Zi Shen Shu

Primary implementation:

- `esoteric_numerology/SZNUM_Ms.py`

Main methods:

- monthly charting: `pp_ly()`
- natal charting: `pp_sz()`
- natal analysis: `pd_sz()`
- DaYun analysis: `pd_dy()`
- LiuNian analysis: `pd_ln()`
- full integrated analysis: `pd_all()`

Desktop actions:

- `analysis_sz()`
- `analysis_dy()`
- `analysis_ln()`
- `analysis_all()`
- `popup_result()`

Publicly visible anonymized examples include:

- `character_case/CaseReports/A参考模板/案例_邵子神数_综合分析_20260421_032651.txt`
  about `18,953` characters
- `character_case/CaseReports/A参考模板/案例_邵子神数_大运分析_20260421_032641.txt`
  about `3,293` characters
- `character_case/CaseReports/XXX/XXX_邵子神数_全盘分析_20260308_155546.md`
  about `5,372` characters

This is enough to show that Shao Zi is not just conceptually supported. It already produces multi-layer report artifacts with real case archiving.

## Shared Interaction and UI Layer

If someone only scans the business modules, the project can look like "many metaphysics systems placed side by side." The shared UI layer is what turns it into a real product.

```text
┌────────────────────────── Shared UI / Interaction Layer ──────────────────────────┐
│ ui/                                                                               │
│ ├─ shared_ui.py: WorkerThread, TranslationThread, ResultDialog                    │
│ ├─ ai_analysis_dialog.py: desktop AI analysis dialog                              │
│ ├─ case_notes.py: case notes dialog                                               │
│ ├─ app_bootstrap.py: icon setup and startup helpers                               │
│ └─ icons/: desktop icon assets                                                    │
└────────────────────────────────────────────────────────────────────────────────────┘
```

### `shared_ui.py`

This file centralizes the most important reusable components:

- `WorkerThread`
- `TranslationThread`
- `ResultDialog`
- `get_case_save_input()`
- `CompactTitleGroupBox`

Why this matters:

- different modules do not each implement their own thread model
- result display is consistent across systems
- case-saving interaction is shared
- the UI layer has internal reuse rather than copy/paste fragmentation

### `ai_analysis_dialog.py`

This is not the provider code itself. It is the desktop-facing AI analysis window.

It handles:

- model selection
- progress presentation
- result display
- export entry points

So AI is not hidden in a backend-only function. It is already integrated into the desktop product flow.

### `case_notes.py`

This file handles note viewing and note updating after a case is reloaded from the case system. That may sound small, but it is the kind of feature that distinguishes a long-term working tool from a one-off demo.

### `app_bootstrap.py`

This file handles:

- icon setup
- startup helpers
- fallback app icon logic

Again, this is product polish work, not merely algorithm work.

### `icons/`

A dedicated icon directory is a small but visible sign that the desktop app was built as a product, not just as raw engineering output.

## Support Layers That Make the Whole Repository Reusable

The project is not only a group of metaphysics features. It is also a small platform built on shared infrastructure.

### `lunar_solar/`: shared time and calendar engine

This module is one of the most important technical foundations in the project.

It provides:

- solar / lunar conversion
- solar terms
- GanZhi calculation
- EightChar objects
- DaYun / LiuNian / LiuYue base objects
- traditional cultural calendar features
- reverse lookup from BaZi to possible solar timestamps

Every major business module depends on it:

- Four Pillars
- Zi Wei Dou Shu
- I Ching / Liu Yao
- Auspicious Date
- Nameology
- Esoteric numerology

Its engineering importance is straightforward:

> **The project centralizes time-sensitive calendar logic instead of allowing each module to compute its own divergent version.**

### `character_case/`: turning one-off analysis into long-term research workflow

Many metaphysics tools stop at "calculate once." This project does not.

The case system currently supports:

- system grouping
- category management
- search
- case creation, editing, ordering, and deletion
- JSON import/export
- Excel import/export
- Markdown/TXT unified export
- reload of a saved case back into the corresponding module

Supported systems include:

- Four Pillars
- Four Pillars manual mode
- Zi Wei Dou Shu
- I Ching / Liu Yao
- Auspicious Date
- Nameology
- Tie Ban
- Shao Zi

From a product perspective, this turns the software from a calculator into a research workstation.

### `ai/`: placing modern LLM workflows on top of rule reports

The AI layer is no longer a single thin wrapper. It already has separate concerns for:

- `analysis/`
- `providers/`
- `analysis_graph.py`
- `modern_prompts.py`
- `prompt_manager.py`
- `topic_schema.py`
- `core/`

That allows a more accurate public statement:

> **AI in this project is not a replacement for the rules layer. It is a second-pass interpretation layer built on top of traceable rule-generated reports.**

## Publicly Visible Artifact Types

To keep the showcase grounded, it helps to separate visible evidence from inferred capability.

### Long-form structured reports currently visible

Visible in the public snapshot used for this update:

- Four Pillars natal, annual, and integrated reports
- I Ching integrated and one-hexagram/multi-angle reports
- Shao Zi DaYun, integrated, and full reports

Representative sizes:

- Four Pillars natal report: about `36,035` characters
- Four Pillars template report: about `30,142` characters
- Shao Zi integrated report: about `18,953` characters
- I Ching integrated report: about `6,751` characters

### Graphical artifacts

Visible or clearly supported:

- Zi Wei unified chart windows
- Zi Wei chart windows opened from Four Pillars birth data
- desktop UI screenshots across the main modules

### Archive artifacts

Visible and architecturally important:

- Markdown reports
- TXT reports
- SQLite case database
- JSON / Excel import-export flows

### Modules with real methods but limited public sample files

In the public snapshot reviewed during this update, public sample-report files were limited or not found for:

- Zi Wei Dou Shu
- Auspicious Date
- Nameology
- Tie Ban Shen Shu

That does **not** mean those modules are hypothetical. It means the public repository currently exposes fewer anonymized report samples for them than it does for BaZi, Liu Yao, and Shao Zi.

That distinction belongs in a credible showcase README.

## Not a Set of Standalone Scripts, but a Complete Product Flow

The most important thing to emphasize externally is not the number of metaphysics systems. It is that the project already behaves like a coherent product.

### Unified desktop experience

- all major systems live inside one PySide6 desktop app
- shared thread, dialog, save, and startup behaviors are reused across modules
- interaction patterns remain consistent even though the rule systems differ greatly

### Unified case workflow

- major systems can save cases
- saved cases can be categorized, searched, edited, exported, and reloaded
- users can continue analysis from prior work instead of starting from zero each time

### Unified report workflow

- Markdown and TXT export are shared patterns
- outputs can be read by people and used as AI inputs
- report structures are not random per module

### Unified AI analysis layer

- rules layer generates the base report
- topic schema splits the result into meaningful sections
- AI providers are called only after rule-generated material exists

That pipeline is one of the strongest signs that the project is real engineering work rather than a superficial UI shell.

## Architecture

The repository is easiest to understand as a layered desktop product:

```text
┌──────────────────────────── Presentation Layer ────────────────────────────┐
│ mainAppUI.py                                                               │
│ ├─ Case Management                                                         │
│ ├─ Four Pillars                                                            │
│ ├─ Zi Wei Dou Shu                                                          │
│ ├─ I Ching / Liu Yao                                                       │
│ ├─ Auspicious Date                                                         │
│ ├─ Nameology                                                               │
│ ├─ Tie Ban Shen Shu                                                        │
│ ├─ Shao Zi Shen Shu                                                        │
│ └─ Four Pillars Manual Mode                                                │
└─────────────────────────────────────────────────────────────────────────────┘
                                  │
                                  ▼
┌──────────────────── Shared Interaction / UI Layer ─────────────────────────┐
│ ui/                                                                        │
│ ├─ shared_ui.py: WorkerThread, TranslationThread, ResultDialog             │
│ ├─ ai_analysis_dialog.py: desktop AI dialog                                │
│ ├─ case_notes.py: case notes dialog                                        │
│ ├─ app_bootstrap.py: icon and startup helpers                              │
│ └─ icons/: desktop icon assets                                             │
└─────────────────────────────────────────────────────────────────────────────┘
                                  │
                                  ▼
┌──────────────────────── Business Modules ──────────────────────────────────┐
│ four_pillars_destiny/       purple_star_astrology/                         │
│ BaZi / Four Pillars           Zi Wei Dou Shu                               │
│                                                                             │
│ hexagram_divination/         auspicious_date/                              │
│ I Ching / Liu Yao            Auspicious Date                               │
│                                                                             │
│ esoteric_numerology/         nameology/                                    │
│ Tie Ban / Shao Zi            Nameology / Western Numerology                │
└─────────────────────────────────────────────────────────────────────────────┘
                                  │
                                  ▼
┌──────────────────────────── Support Layer ─────────────────────────────────┐
│ lunar_solar/                                                               │
│ ├─ solar/lunar conversion                                                  │
│ ├─ solar terms, GanZhi, EightChar, DaYun, LiuNian, LiuYue                  │
│ └─ shared time foundation for BaZi, Zi Wei, date selection, and more       │
│                                                                             │
│ character_case/                                                            │
│ ├─ database_manager.py: SQLite management                                  │
│ ├─ case_manager_widget.py: case-management UI                              │
│ ├─ dialogs/: system-specific case dialogs                                  │
│ └─ unified_formatter.py: Markdown / TXT export                             │
│                                                                             │
│ ai/                                                                        │
│ ├─ analysis/: AIAnalyzer, topic analysis threads, retry logic              │
│ ├─ providers/: OpenAI-compatible / Claude / Gemini / Qwen                  │
│ ├─ analysis_graph.py: LangGraph-style workflow                             │
│ ├─ modern_prompts.py / prompt_manager.py: prompt contract layers           │
│ ├─ topic_schema.py: report topic-splitting rules                           │
│ └─ config.py / core/: provider config, cache, tokens, runtime support      │
└─────────────────────────────────────────────────────────────────────────────┘
```

Why this architecture matters:

- business rules remain separable
- shared infrastructure is not reimplemented per module
- adding new systems is easier
- UI, data, rules, and AI concerns remain reasonably distinct

## What Technical Capability This Project Demonstrates

If used as a resume project, it demonstrates a broad and defensible set of abilities.

### 1. Complex rule-system modeling

The project takes traditional knowledge and converts it into:

- executable functions
- structured rule data
- topic mappings
- report templates
- multi-layer inference paths

That is qualitatively different from ordinary business forms and CRUD services.

### 2. High-complexity desktop product engineering

This is not a throwaway script. It is a multi-screen desktop application with:

- sustained UI organization
- background threads
- non-modal result windows
- chart rendering
- cross-module interaction reuse

### 3. Data-driven design

The repository repeatedly chooses structured data over deeply hardcoded behavior, especially in:

- Zi Wei interpretation data
- BaZi classical text layers
- Liu Yao side-system mapping
- nameology corpora and rule tables
- auspicious-date topic rules

That is a strong maintainability signal.

### 4. AI systems integration

The AI layer is more than a provider API call. It includes:

- provider abstraction
- prompt management
- topic splitting
- workflow orchestration
- result validation/retry support

That looks much more like real product integration than a demo wrapper.

### 5. Local data and workflow design

The combination of SQLite cases, import/export, report persistence, reload, and notes shows that the project was designed for ongoing use rather than one-time novelty.

## Resume Positioning

The project can be positioned succinctly in English as:

> **A desktop-first traditional Chinese metaphysics analysis platform that converts classical rule systems into executable software, structured reports, reusable case-management workflows, and AI-assisted interpretation pipelines.**

A shorter alternative:

> **Built a PySide6-based metaphysics analysis platform with rule engines, calendar infrastructure, persistent case management, report generation, and AI-assisted interpretation workflows.**

## Interface Screenshots

The following screenshots are included only to show the product form. They do not expose implementation code.

<table>
  <tr>
    <td align="center"><strong>Four Pillars / BaZi</strong><br><img src="image/four_pillars_destiny.png" alt="Four Pillars interface" width="900"></td>
  </tr>
  <tr>
    <td align="center"><strong>Zi Wei Dou Shu</strong><br><img src="image/purple_star_astrology.png" alt="Zi Wei Dou Shu interface" width="900"></td>
  </tr>
  <tr>
    <td align="center"><strong>I Ching / Liu Yao</strong><br><img src="image/hexagram_divination.png" alt="I Ching interface" width="900"></td>
  </tr>
  <tr>
    <td align="center"><strong>Auspicious Date</strong><br><img src="image/auspicious_date.png" alt="Auspicious Date interface" width="900"></td>
  </tr>
  <tr>
    <td align="center"><strong>Nameology</strong><br><img src="image/nameology.png" alt="Nameology interface" width="900"></td>
  </tr>
  <tr>
    <td align="center"><strong>Tie Ban / Shao Zi</strong><br><img src="image/esoteric_numerology.png" alt="Esoteric numerology interface" width="900"></td>
  </tr>
  <tr>
    <td align="center"><strong>Case Management</strong><br><img src="image/character_case.png" alt="Case management interface" width="900"></td>
  </tr>
</table>

## Public Showcase Boundaries

For knowledge-asset, commercial, and user-data reasons, this public showcase repository does **not** provide:

- project source code
- rule datasets and text libraries
- SQLite case database
- API secrets or provider configuration
- implementation detail sufficient to reproduce the full private product

The purpose of this repository is to show:

- scope
- product shape
- engineering depth
- system structure
- UI results

## Disclaimer

This project is presented as a showcase of:

- traditional culture digitization
- rule-system engineering
- desktop software design
- AI workflow integration

Its outputs are generated from program rules, structured datasets, and AI interpretation layers. They do not constitute medical, legal, financial, marital, or other real-world professional advice.

Traditional metaphysics content should be understood as cultural, analytical, and research-oriented material, not as a substitute for factual investigation or professional judgment.
