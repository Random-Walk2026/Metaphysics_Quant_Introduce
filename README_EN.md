<h1 align="center">MetaphysicsQuant</h1>
<p align="center"><strong>Traditional Chinese Metaphysics, Built as Software · 工程化中国术数分析平台</strong></p>

<p align="center">
  <a href="README.md">简体中文</a> |
  <a href="README_EN.md">English</a>
</p>

<p align="center">
  <a href="https://img.shields.io/github/stars/lyzhk/MetaphysicsQuant?style=for-the-badge"><img alt="GitHub stars" src="https://img.shields.io/github/stars/lyzhk/MetaphysicsQuant?style=for-the-badge"></a>
  <a href="https://img.shields.io/github/forks/lyzhk/MetaphysicsQuant?style=for-the-badge"><img alt="GitHub forks" src="https://img.shields.io/github/forks/lyzhk/MetaphysicsQuant?style=for-the-badge"></a>
  <a href="https://img.shields.io/badge/Python-3.10%2B-3776AB?style=for-the-badge&logo=python&logoColor=white"><img alt="Python 3.10+" src="https://img.shields.io/badge/Python-3.10%2B-3776AB?style=for-the-badge&logo=python&logoColor=white"></a>
  <a href="https://img.shields.io/badge/UI-PySide6-41CD52?style=for-the-badge&logo=qt&logoColor=white"><img alt="PySide6" src="https://img.shields.io/badge/UI-PySide6-41CD52?style=for-the-badge&logo=qt&logoColor=white"></a>
</p>

> **Showcase Notice**
>
> This is a **public showcase repository**, used only to present the project's design, feature scope, engineering challenges, and UI results.
> It contains **no** source code, rule data, case database, API configuration, or any private asset that could reproduce the commercialized capability.
> Every case in this document is an **anonymized sample** and does not refer to any real individual.

---

MetaphysicsQuant turns the hardest-to-engineer parts of traditional Chinese metaphysics into a runnable, traceable, extensible, and long-lived software platform. It covers seven desktop systems — Four Pillars (BaZi), Purple Star Astrology (Zi Wei Dou Shu), I-Ching / LiuYao, Auspicious Date Selection, Nameology, Tie Ban and Shao Zi numerology — plus three standalone engines: YanQin, QinXing, and Tarot. All of them share a calendar core, a SQLite case library, Markdown/TXT export, and an AI topic-analysis pipeline.

### At a Glance

- **One desktop app, many systems**: 7 metaphysics systems + 3 standalone engines, unified in a single PySide6 application with a shared interaction skeleton.
- **Knowledge as data, not hard-code**: ~486 JSON files hold the clauses, corpora, and rules; code matches and assembles rather than embedding logic.
- **A real calendar engine underneath**: an in-house `lunar_solar` package handles solar/lunar conversion, the 24 solar terms, GanZhi, EightChar, and fortune cycles — the single source of time truth.
- **Reports, not verdicts**: output is long structured text (single samples reach the 30K-character range), organized by topic and ready for AI second-pass reading.
- **A research workbench, not a calculator**: a SQLite case library lets every analysis be saved, searched, annotated, exported, and reloaded.
- **AI on top of rules**: the deterministic rule layer always runs first; LLMs only interpret traceable reports, across multiple providers.

> **How to read this repo**: this is a documentation-only showcase. Start with the [screenshots](#screenshots) for the product form, then the [architecture](#architecture-overview) for the layering, then the [method-level interfaces](#method-level-interfaces-and-report-shapes) for what each module actually outputs.

---

## Table of Contents

- [Screenshots](#screenshots)
- [Architecture Overview](#architecture-overview)
- [Project Overview](#project-overview)
- [Why This Project Is Hard](#why-this-project-is-hard)
- [Scale Snapshot](#scale-snapshot)
- [Feature Summary](#feature-summary)
- [Module Deep Dive](#module-deep-dive)
- [Method-Level Interfaces and Report Shapes](#method-level-interfaces-and-report-shapes)
- [Standalone Engines: YanQin, QinXing, Tarot](#standalone-engines-yanqin-qinxing-tarot)
- [Shared Interaction and Common UI Layer](#shared-interaction-and-common-ui-layer)
- [Support Layer: A Reuse Core, Not a Backdrop](#support-layer-a-reuse-core-not-a-backdrop)
- [Real Artifacts Visible in the Public Repo](#real-artifacts-visible-in-the-public-repo)
- [Not a Single-Module Script, but a Complete Product](#not-a-single-module-script-but-a-complete-product)
- [Technical Capabilities Demonstrated](#technical-capabilities-demonstrated)
- [How to Frame It on a Résumé](#how-to-frame-it-on-a-résumé)
- [Design Principles](#design-principles)
- [Recent Refactor Notes](#recent-refactor-notes)
- [Glossary](#glossary)
- [FAQ](#faq)
- [Showcase Boundaries](#showcase-boundaries)
- [Disclaimer](#disclaimer)

---

## Screenshots

The screenshots below come from the current PySide6 desktop app and are shown only to demonstrate the product form — they contain no implementation code. Each tab is an independent metaphysics system, yet they share one interaction skeleton, result dialog, and case-saving flow.

<table>
  <tr>
    <td align="center"><strong>Four Pillars (BaZi)</strong><br><sub>numeric chart / manual GanZhi / natal · decade · annual · monthly / seven-pillar reading</sub><br><img src="image/four_pillars_destiny.png" alt="Four Pillars UI" width="900"></td>
  </tr>
  <tr>
    <td align="center"><strong>Purple Star Astrology</strong><br><sub>12 palaces / main & auxiliary stars / four transformations / 4-layer chart</sub><br><img src="image/purple_star_astrology.png" alt="Purple Star UI" width="900"></td>
  </tr>
  <tr>
    <td align="center"><strong>I-Ching / LiuYao</strong><br><sub>time / 3-number / mystic-number casting / six relatives, six spirits, NaJia / multi-reading</sub><br><img src="image/hexagram_divination.png" alt="Hexagram UI" width="900"></td>
  </tr>
  <tr>
    <td align="center"><strong>Auspicious Date Selection</strong><br><sub>perpetual calendar / lunar-year calendar / 70+ topical date rules / compatibility</sub><br><img src="image/auspicious_date.png" alt="Auspicious Date UI" width="900"></td>
  </tr>
  <tr>
    <td align="center"><strong>Nameology</strong><br><sub>Chinese nameology / five-grid & three-talents / name generation / company naming / Western numerology</sub><br><img src="image/nameology.png" alt="Nameology UI" width="900"></td>
  </tr>
  <tr>
    <td align="center"><strong>Tie Ban / Shao Zi Numerology</strong><br><sub>birth-to-number / quarter-marks & clauses / natal · decade · annual · full</sub><br><img src="image/esoteric_numerology.png" alt="Numerology UI" width="900"></td>
  </tr>
  <tr>
    <td align="center"><strong>Case Management</strong><br><sub>SQLite case library / categorized search / notes / import-export / reload into module</sub><br><img src="image/character_case.png" alt="Case Management UI" width="900"></td>
  </tr>
</table>

---

## Architecture Overview

The project is closer to a **layered desktop product** than a pile of side-by-side scripts. A presentation layer orchestrates everything, core metaphysics modules compute independently, and the calendar, case, AI, and common-UI layers are reused as shared support infrastructure.

```text
┌────────────────────────────────── Presentation ────────────────────────────┐
│ mainAppUI.py  (PySide6 desktop app, 9 tabs in one window)                   │
│ ├─ Case Mgmt     ├─ Four Pillars   ├─ Purple Star                          │
│ ├─ I-Ching       ├─ Date Selection ├─ Nameology                            │
│ ├─ Tie Ban       ├─ Shao Zi        └─ BaZi (manual GanZhi)                  │
└─────────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────── Interaction / Common UI ───────────────────────┐
│ ui/                                                                         │
│ ├─ shared_ui.py        : WorkerThread, TranslationThread, ResultDialog       │
│ ├─ ai_analysis_dialog.py: AI comprehensive-analysis dialog                  │
│ ├─ case_notes.py       : floating case-notes window                         │
│ ├─ app_bootstrap.py    : icon & app startup helpers                         │
│ └─ icons/              : desktop icon assets                                 │
└─────────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────── Core Business Modules ─────────────────────┐
│ destiny_bazi/                    │ destiny_astrology/                       │
│ Four Pillars / manual GanZhi     │ Purple Star Astrology                    │
│                                                                             │
│ divination_iching/ +             │ date_selection/                          │
│ divination_hexagram/             │ Auspicious Date Selection                │
│ I-Ching core + LiuYao orchestr.  │                                          │
│ (+ divination_xiaolr/ganzhi/     │                                          │
│    zhuge/yapai number divination)│                                          │
│                                                                             │
│ destiny_shenshu/                 │ nameology_cn/ + nameology_west/          │
│ Tie Ban / Shao Zi numerology     │ Chinese nameology / Western numerology   │
│                                                                             │
│ Standalone engines (not in the desktop app):                                │
│ destiny_yanqin/ YanQin natal  ·  divination_yanqin/ QinXing event           │
│ divination_tarot/ Waite Tarot (Celtic Cross + 3-card + daily)              │
└─────────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────── Support Layer ─────────────────────────┐
│ lunar_solar/                                                                 │
│ ├─ solar ⇄ lunar conversion                                                 │
│ ├─ solar terms, GanZhi, EightChar, decade/annual/monthly fortune            │
│ └─ provides the time foundation for BaZi, Purple Star, date selection, etc. │
│                                                                             │
│ case_character/                                                             │
│ ├─ database_manager.py : SQLite database management                         │
│ ├─ case_manager.py     : case management UI & tree search                   │
│ ├─ dialogs/            : per-system case input / edit dialogs               │
│ └─ unified_formatter.py: unified Markdown / TXT export                      │
│                                                                             │
│ ai/                                                                         │
│ ├─ analysis/           : AIAnalyzer, per-topic threads, parse retries       │
│ ├─ providers/          : OpenAI-compatible / Claude / Gemini / Qwen          │
│ ├─ analysis_graph.py   : LangGraph-style analysis flow                      │
│ ├─ prompts/ + prompt_manager.py : prompt rules & compatibility layer        │
│ ├─ topic_schema.py     : report topic-split rules                           │
│ └─ config.py / core/   : provider config, cache, token, runtime infra       │
└─────────────────────────────────────────────────────────────────────────────┘
```

Benefits of this structure:

- Rule modules are independent and can evolve separately.
- Shared infrastructure is not reimplemented in every module.
- New features are easier to add as a new module or a new analysis layer.
- UI, data, rules, and AI have relatively clear separation of concerns.

### Module Inventory (by directory)

| Directory | Role | Description |
|---|---|---|
| `mainAppUI.py` | Presentation | PySide6 desktop app, 9 tabs in one window |
| `destiny_bazi/` | Core | Four Pillars / manual GanZhi: rule base + seven-pillar reading + classics |
| `destiny_astrology/` | Core | Purple Star: 12 palaces + four-transformation flying stars + 4-layer chart |
| `divination_iching/` | Core | I-Ching hexagram core + ZhouYi judgments + 64-hexagram corpus |
| `divination_hexagram/` | Core | LiuYao orchestration: ZhouYi + 5 classical books + number divination |
| `divination_xiaolr/` | Number div. | Xiao Liu Ren |
| `divination_ganzhi/` | Number div. | GanZhi numerology |
| `divination_zhuge/` | Number div. | Zhuge numerology + TaiJi numerology |
| `divination_yapai/` | Number div. | Domino numerology (with shuffle & pattern-probability tool) |
| `date_selection/` | Core | Auspicious date selection, a topical rule system |
| `nameology_cn/` | Core | Chinese nameology, name generation, character divination, numbers |
| `nameology_west/` | Core | Western numerology (Pythagorean / Cheiro / Vedas) |
| `destiny_shenshu/` | Core | Tie Ban / Shao Zi numerology |
| `destiny_yanqin/` | Engine | YanQin natal-chart system |
| `divination_yanqin/` | Engine | QinXing event divination |
| `divination_tarot/` | Engine | Waite Tarot |
| `lunar_solar/` | Support | Calendar engine (solar/lunar, terms, GanZhi, EightChar) |
| `case_character/` | Support | SQLite case library, unified formatter, import/export |
| `ai/` | Support | Multi-provider LLM analysis, topic split, prompt management |
| `ui/` | Support | Shared threads, result dialog, case notes, icon startup |

### Tech Stack

| Layer | Choice |
|---|---|
| Desktop UI | PySide6 (Qt for Python), Fusion style |
| Language | Python 3.10+ |
| Concurrency | `QThread` background threads (`WorkerThread`) to keep the UI responsive |
| Storage | SQLite (cases), JSON (rules & clauses), Excel (interchange) |
| Calendar | In-house `lunar_solar` engine (solar / lunar / terms / GanZhi / EightChar) |
| AI | Multi-provider (OpenAI-compatible / Claude / Gemini / Qwen), LangGraph-style flow |
| Export | Unified Markdown / TXT formatter |

### Main Data Flow

```text
birth time / casting numbers / name
        │
        ▼
lunar_solar calendar conversion (solar⇄lunar, terms, GanZhi, EightChar, fortune)
        │
        ▼
each core module's rule engine (shensha, structures, stars, hexagrams, numbers, date rules)
        │
        ▼
wrapper layer *_Ms.py produces structured topical reports (☆ topic / § sub-item)
        │
        ├──▶ ResultDialog (copy / export / translate)
        ├──▶ case_character saves a case (SQLite) → reloadable, searchable
        ├──▶ unified_formatter exports Markdown / TXT
        └──▶ ai splits by topic → multi-provider LLM second-pass reading → real-world advice
```

---

## Project Overview

MetaphysicsQuant is a long-term engineering project that turns traditional Chinese metaphysics into a software system.

It is not a simple "chart tool" or a "bag of divination scripts." It takes knowledge scattered across classics, oral formulas, and human experience — across astrology, calendars, hexagrams, date selection, nameology, and number systems — and breaks it down into:

- executable rule engines
- maintainable data structures and JSON clause libraries
- a reusable calendar foundation
- a case system that can be saved, searched, exported, and reloaded
- a topic-analysis workflow that plugs into large language models
- a unified desktop product experience across modules

In one sentence, the core value is:

> **Turn the hardest-to-engineer knowledge of traditional metaphysics into a runnable, traceable, extensible, long-lived software platform.**

Importantly, the project does not sell "accuracy." What it really solves is an engineering problem: **how to translate unstructured traditional knowledge into structured, reviewable, versionable, collaboratively maintainable rules and data.** Whether to adopt any particular judgment is left to the user's real-world discretion.

---

## Why This Project Is Hard

The difficulty is not the UI — it is the "softwarization of a knowledge system."

Traditional metaphysics systems usually suffer from:

- rules scattered across classics, tables, formulas, and human experience, with no unified expression
- extreme sensitivity to time, calendar, and school-of-thought conventions, with very little margin for error
- output that is not fixed fields but long structured text, topical judgments, and contextual combinations
- the same user repeatedly analyzing, comparing, and revising, requiring case retention and reload
- if AI is layered on top, a reliable rule layer must come first — the model cannot "improvise"

MetaphysicsQuant deals with exactly these hard parts:

- rule system first, interaction layer second
- structured output first, AI interpretation second
- a reviewable report pipeline first, then result presentation

A few concrete "devil-in-the-details" examples that decide whether the system is actually usable:

1. **Early/late Zi hour**: for the 23:00–24:59 hour, schools differ on the day pillar. The calendar core exposes a switch (e.g. `setSect(1)`) so upper layers choose the convention explicitly, instead of silently hard-coding it.
2. **Leap months**: lunar leap months are represented internally as negative month numbers (e.g. leap 3rd month = `-3`); every month-pillar derivation must recognize this.
3. **Solar-term month boundaries**: the month pillar switches at the precise moment of one of the 24 solar terms, not at the lunar first-of-month — a few hours off can change the pillar.
4. **Layered topical assembly**: a single "marriage" topic may simultaneously cite multiple sources (Su-school blind method, Wu Xing Jing Ji, San Ming Tong Hui, Yu Zhao Shen Ying Zhen Jing, Liang-school theory) and must be organized by source rather than crammed into one blob.
5. **Personalized shensha overlay**: in date selection, beyond generic inauspicious stars, personal ones are overlaid based on the querent's own BaZi (e.g. clashing the host's year/day fate, arrow-blade star, turn-back star).

Each detail alone is not hard, but keeping them consistent, maintainable, and extensible across seven systems requires distilling them into a shared foundation and shared data structures — which is exactly where the engineering value lies.

---

## Scale Snapshot

The following is a scale snapshot of the **private source repository** (this public showcase contains none of those implementation files):

| Metric | Scale |
|---|---:|
| Python files | 210 |
| Python lines of code | ~109,175 |
| JSON data files | 486 |
| Four Pillars module | 12 Python files, 16 JSON files |
| Purple Star module | 15 Python files, 20 JSON files |
| Chinese nameology module | 10 Python files, 419 JSON files (incl. name-generation corpus) |
| Western numerology module | 5 Python files, 6 JSON files |
| Calendar foundation | 42 Python files |
| AI analysis layer | 38 Python files |
| Case system | 16 Python files |
| Common UI layer | 5 Python files |

Rule density also shows at the file level: the natal BaZi class `SZBZ_2Bz.py` is ~14,500 lines, and the GanZhi rule base `SZBZ_1Gz.py` is ~4,000 lines with 330 methods. This is not a "single-file demo" but a complete software project with clear layering, accumulated rules, and traces of long-term evolution.

> Note: all cited numbers are a point-in-time snapshot and change as the main repo iterates; they convey scale, not an exact count.

---

## Feature Summary

| Module | Scope |
|---|---|
| Four Pillars (BaZi) | numeric chart, manual GanZhi, natal, decade, annual, monthly, fetal/life/body palaces, seven-pillar reading, palace-pressure method, Purple Star linkage |
| Purple Star | 12-palace chart, main/auxiliary/minor stars, four transformations, star brightness, decade, annual, monthly, 4-layer chart, combination judgments |
| I-Ching / LiuYao | time / 3-number / mystic-number / hexagram-input casting, primary & changed hexagrams, six relatives, six spirits, world-response, NaJia, annual reading, multi-reading |
| Auspicious Date | perpetual calendar, full-year lunar calendar, 70+ topical date rules, marriage, governance/military, construction, travel/wealth, medicine/move-in, burial, compatibility |
| Nameology | Chinese nameology, five-grid & three-talents, 81-number theory, name generation, company naming, character divination, number analysis |
| Western numerology | combined report across Pythagorean, Cheiro/Chaldean, Vedas |
| Tie Ban / Shao Zi | birth-to-number, quarter-marks, clause lookup, natal, decade, annual, comprehensive reports |
| YanQin / QinXing / Tarot | YanQin natal reading, QinXing event divination, Waite Tarot (standalone engines) |
| Case system | SQLite case library, categorization, search, notes, import/export, report export, reload into module |
| AI topic analysis | report split, topical prompts, provider abstraction, model calls, interpretation and real-world advice |

The output is not a one-line "good or bad" verdict but expandable structured material. A single BaZi natal report sample reaches the 30,000-character range, including chart info, seven-pillar topics, classical clauses, shensha combinations, fortune cycles, and an AI-reading entry point.

---

## Module Deep Dive

### 1. Four Pillars (BaZi): the highest rule-density core module

The Four Pillars module (`destiny_bazi/`) is the heaviest part of the whole system. It is not just "deriving four pillars" — it programmatizes the post-charting rule judgments, topical splitting, and report generation.

Its capabilities include:

- converting solar/lunar birth time into four pillars
- manual entry of year/month/day/hour pillars ("BaZi manual")
- multi-layer analysis of natal, decade, annual, monthly
- fetal, life, and body palaces plus the seven-pillar perspective
- linkage with the Purple Star chart

More importantly, the base rule volume is huge. The GanZhi rule base `SZBZ_1Gz.py` contains **330 methods**, many of which directly drive:

- shensha recognition: Tian Yi noble, Fu Xing noble, Tai Ji noble, Wen Chang noble, Tian De, Yue De, Tian Xi, Yi Ma, Hua Gai, Jin Yu, Xue Tang, Ci Guan, Jie Lu void, Gui Men gate, Mu Yu star, blood-light, robbery star, death star, Yang Blade, Yuan Chen, void, Xian Chi, Tian Luo Di Wang, Gu Chen Gua Su, and many more
- structure (geju) judgments: noble structures, inauspicious structures, follower/transformation structures
- punishment/clash/combination/meeting relationships
- the twelve palace-pressure deities: Tai Sui, Qing Long, Sang Men, Liu He, Guan Fu, Xiao Hao, Da Hao, Zhu Que, Bai Hu, Gui Shen, Diao Ke, Bing Fu
- blind-school shensha and folk-experience rules: four-poverty days, Zhuang Sha, Luo Sha, Ji Sha, eight-defeat, hanging-beam star, womb star, iron-punishment star, sky-broom, earth-broom, soul-chasing, and more

This is where the project's engineering substance shows most, because what is handled here is not CRUD but **highly knowledge-dense rule-system modeling**.

The module's `data/` directory also accumulates a large amount of classical and rule data, e.g.:

- `SanMingTongHui.json`: *San Ming Tong Hui*
- `DiTianSui.json`: *Di Tian Sui*
- `QiongTongBaoJian.json`: *Qiong Tong Bao Jian*
- `ShenFengTongKao.json`: *Shen Feng Tong Kao*
- `WuXingJingJi.json`: *Wu Xing Jing Ji*
- `GuiGuZi_LTQ.json`, `GuiGuZi_MGB.json`: Gui Gu Zi tables
- `YuanTiangangCG.json`: Yuan Tian Gang weighing-bones
- `SanShiYanQin.json`: San Shi Yan Qin
- `SuShiMangPai.json`: Su-school blind method
- `LanTaiMiaoXuan.json`: Lan Tai Miao Xuan
- `DaMoYiZhangJing.json`, `JueFa.json`, `Books.json`: supplementary data

The code also directly references sources such as *Yuan Hai Zi Ping*, *Yu Zhao Shen Ying Zhen Jing*, *Yong Le Da Dian*, and *Tian Yuan Wu Xian Jing*. The most accurate way to describe this is not "a BaZi tool" but:

> **An executable topical report system that merges many classics, formulas, blind-school experience, and program rules.**

### 2. Purple Star: visual chart + data-driven judgments

The Purple Star module (`destiny_astrology/`) emphasizes a "maintainable judgment system" and a "graphical chart expression" beyond charting itself.

Its characteristics include:

- 12-palace chart generation
- placement of main / auxiliary / minor stars and the four transformations
- star brightness states (temple, prosperous, gain, benefit, even, not, fallen)
- multi-layer boards: decade, annual, monthly
- a 4-layer chart: natal / decade / annual / monthly
- combination-star and gender-specific judgment matching

The engineering value of this module is:

- migrating judgment maintenance from hard-coded `if-else` to a JSON-driven data layer
- turning complex boards into switchable, exportable, displayable desktop graphics
- splitting "data organization" and "chart display" into independently evolving capability layers

Its core engine, `Star_Matcher.py`'s `StarCombinationMatcher`, uses set theory for unordered combination subset matching; multi-star combinations automatically outrank single stars; four-transformation stars are joined with "且", regular stars with "、"; the twelve longevity shensha use "坐" instead of "落"; and empty descriptions are auto-filtered. Adding a judgment only edits JSON, not code.

### 3. I-Ching / LiuYao: layered hexagram core and orchestration

The I-Ching system was refactored into two layers:

- `divination_iching/`: the hexagram core. `IC_Ly.py` handles hexagrams, NaJia, six relatives, world-response, six spirits, and casting; `IC_Ms.py` handles ZhouYi line judgments; `website/` keeps a Markdown document for each of the 64 hexagrams.
- `divination_hexagram/`: the orchestration layer. `Divination.py` (`LyMs`) integrates ZhouYi, five classical books (*Bu Shi Zheng Zong*, *Huang Jin Ce*, *Huo Zhu Lin*, *Zeng Shan Bu Yi*, *Yi Yin*), and Xiao Liu Ren / GanZhi / Zhuge / TaiJi / domino numerology into one multi-perspective report.

It supports:

- time casting, 3-number casting, mystic-number and hexagram input, moving-line input
- primary hexagram, changed hexagram, moving lines, six relatives, six spirits, world-response, NaJia
- annual reading
- multi-reading (one hexagram, many parallel reading paths)

What stands out is that **analysis logic and reference material coexist**: the small number-divination systems are each their own package (`divination_xiaolr`, `divination_ganzhi`, `divination_zhuge`, `divination_yapai`) and are invoked on demand by the orchestration layer rather than piled into one file.

### 4. Auspicious Date: modeled by topic, not a flat almanac

The date module (`date_selection/`) is not a plain almanac lookup; it reorganizes date-selection clauses from sources such as *Xie Ji Bian Fang Shu* and *Yu Xia Ji* into a **filterable, categorizable, batch-output** topical system.

The implementation is organized as "event category → topic → shensha rules → per-day auspicious/inauspicious signal → date-range output." The UI switches topics by category; the backend uses:

- `ZR_2Rules.py`: topic groups, source appendices, topic descriptions, and rule data
- `ZR_3Ms.py`: per-topic good/bad shensha signals, rule dispatch, per-day judgment, and interval output
- `ZR_Widget.py`: category selection, date-range computation, and compatibility inputs

It currently covers 4 major categories and 70+ topics, far beyond common labels like "marriage / moving / opening." Displayable topic ranges include:

- **Governance & military**: sacrifice, blessing, seeking-heir, submitting memorials, edicts, amnesty, conferring grace, summoning the worthy, proclaiming policy, banquets, school entry, examinations, learning a craft, taking a master, capping, dispatching envoys, pacifying borders, training troops, marching, taking office, governing the people
- **Daily affairs**: marriage, betrothal, wedding, taking in people, moving, moving home, return, bed-setting, dissolving, bathing, grooming, nail-trimming, seeking medicine, eye treatment, acupuncture, tailoring
- **Construction & earthwork**: building palaces, repairing rooms, repairing city walls, building dikes, breaking ground, raising pillars and beams, repairing warehouses, casting, thatching, weaving, brewing, opening market, contracts, taking delivery of a vehicle, gathering wealth, releasing goods, travel, travel for wealth, lending, collecting debt, dividing property, buying land/houses, building a birthing room, digging canals and wells, installing mills, sealing holes, sweeping the house, decorating walls, leveling roads, demolishing
- **Agriculture, livestock & funerals**: felling, trapping, hunting, fishing, crossing water by boat, planting, herding, taking in livestock, breaking earth, burial, re-interment

Beyond the topic count, the real engineering substance is the rule organization:

- topics are not dead text but map to good / bad shensha lists
- per-day judgment is dispatch + fallback rule matching, not a fixed template
- the system auto-overlays generic inauspicious stars (ten-evil great-defeat days, Yang-Gong taboo days, monthly-taboo days)
- given the querent's BaZi, it overlays personalized inauspicious stars (clashing the host's year/day fate, arrow-blade star, turn-back star, Tian-Gang four-sha)
- it supports the perpetual calendar, full-year lunar calendar, single-topic selection, and compatibility analysis simultaneously

> **The date module converts traditional date-selection clauses into a groupable, filterable, computable, explainable rule system.**

### 5. Nameology & Western numerology: high data-density modules

The naming module looks light but is the heaviest in data — it is split into two packages: `nameology_cn/` (Chinese nameology) and `nameology_west/` (Western numerology). The desktop "Nameology" tab routes by input language automatically.

It covers:

- Chinese nameology, Kangxi / Xinhua strokes, five-grid & three-talents, 81-number theory
- personal name generation and company naming
- character divination, number analysis
- English numerology integrated across three systems (Pythagorean, Cheiro/Chaldean, Vedas)

The personal name generation in particular is not random character stitching but a full filtering pipeline:

- corpora from *Shi Jing*, *Chu Ci*, *Lun Yu*, *Zhou Yi*, the Four Books & Five Classics, primers, Tang poems, Song ci, Five-Dynasties poetry, Song poems, *You Meng Ying*
- five-grid number filtering (enumerate stroke pairs, exclude inauspicious numbers, require at least 3 of 4 grids auspicious)
- three-talents five-element validation
- per-character meaning scoring (blacklist, function words, negative meaning, positive keywords, radicals, strokes, Kangxi luck, multi-factor add/subtract)
- pronunciation and glyph rules (initial/final/tone differences, radical de-duplication)
- candidate-pool ranking and randomized display (a different subset each time for variety)

Company naming follows chapter 6 of *Yi Jing Nameology*: it filters usable brand strokes via a three-level "brand auspicious → subject auspicious → whole auspicious" scheme, then aligns the brand's five elements with the legal person's chart.

### 6. Tie Ban & Shao Zi: software expression of traditional number systems

The characteristics of this group (`destiny_shenshu/`) are:

- input and rules depend heavily on birth time, quarter-marks, GanZhi, and clause systems
- output is not a single number but multi-layer text: chart, clauses, natal / decade / annual
- it also contains hexagram mapping and traditional number lookup logic

They demonstrate the project's ability to keep a unified product structure even when multiple systems coexist.

---

## Method-Level Interfaces and Report Shapes

The section above is more "project intro." From an engineering / résumé perspective, an external reader usually cares about a more concrete question:

> **What can these modules actually output? Is it conceptual support, or already method-level interfaces, UI actions, and exportable real reports?**

This section answers that, organized by "wrapper class / output methods / desktop action / visible artifacts / current status."

### Four Pillars: the most complete method-level backbone

The current wrapper core is `destiny_bazi/SZBZ_6BzMs.py`. This is not a single charting function but a set of output interfaces around "natal - decade - annual - monthly - batch - linked chart."

#### 1. Main text output interfaces

- Natal report: `bzms_num()` / `bzms_gz()`
- Brief report: `bzmss_num()`
- Decade report: `dyms_num()` / `dyms_gz()`
- Annual report: `lnms_num()` / `lnms_gz()`
- Monthly report: `lyms_num()` / `lyms_gz()`
- 10-year annual batch from the current year: `zpln_num()`
- Annual-to-decade and monthly-to-decade transition segments
- Birth-time reverse lookup

The `num` and `gz` entry points correspond to:

- `num`: solar/lunar year-month-day-hour-minute input, for real birth data
- `gz`: manual year/month/day/hour pillars, for classical cases, classroom practice, and reverse-lookup of known charts

#### 2. Desktop actions and button semantics

`SZBZ_Widget_Num.py` (the "Four Pillars" tab) directly maps natal / brief / decade / annual / monthly analysis, the unified result dialog, and a direct linkage to open the Purple Star chart from birth data. `SZBZ_Widget_Gz.py` (the "BaZi manual" tab) maps natal / decade / annual / monthly analysis for the GanZhi-input scenario.

In other words, the module is not "one button outputs everything" but is split by the practitioner's actual workflow into multiple analysis layers.

#### 3. Real artifacts and verifiable samples (anonymized)

Anonymized samples in the repo show these interfaces have landed as real artifacts, not design goals:

- Four Pillars · natal · Markdown: ~`36,035` chars
- Four Pillars · natal · TXT (reference template): ~`30,142` chars
- Four Pillars · annual · TXT: ~`10,246` chars
- Four Pillars · comprehensive · Markdown (multiple)

> All samples are anonymized and refer to no real individual; any name in a filename is replaced with "Sample Case."

These samples matter not because "export files exist," but because they show the system can stably output long, topical, archivable, reviewable structured results.

### Purple Star: text reports, 12-palace info, and a unified chart

The wrapper core is `destiny_astrology/ZWDS_6ZwMs.py`, which already produces "natal topics + 12-palace overview + annual topics + a graphical chart."

#### 1. Main text output interfaces

- Natal topical report: `zwms_num()`
- 12-palace info: `zwg12ms_num()`
- Annual topical report: `zwlnms_num()`
- Decade report interface (reserved): `zwdxms_num()`

To be candid: `zwdxms_num()` exists in the wrapper, but the desktop "all-decade / all-annual analysis" is still a placeholder. That is a very honest engineering signal: the project does not max out every claim with copy — it clearly distinguishes what has landed from what is still evolving.

#### 2. Graphical output interface

A key showcase point is not only text but the **unified chart dialog** `ZwdsUnifiedChartDialog`:

- four-layer switching: natal / decade / annual / monthly
- floating center controls: year, month, decade navigation overlaid on the chart center
- cascading placement: multiple chart dialogs auto-offset and do not overlap
- image saving: PNG / JPG
- reused by the Four Pillars module to open directly from birth data

This shows Purple Star is not "a backend that computes a wall of text" but already a graphical product form.

#### 3. Data layer and judgment layer

Purple Star is worth showcasing not only because "it draws charts" but because it makes judgments data-driven:

- main / auxiliary / four-transformation base data: `star_zx.json`, `star_fx.json`, `star_4h.json`
- palace and topical judgments: `topic_*.json` (character, wealth, career, marriage, health, property, relatives, etc.)
- four-transformation flying-star judgments: `topic_4h.json` (793 clauses of "palace-A transforms into palace-B," in 12 topic categories)
- combination-star matching engine: `StarCombinationMatcher`

The judgment data is organized roughly like this (illustrative, not real clauses):

```jsonc
{
  "ZWDS": {
    "cbg": {                       // Wealth palace
      "single_star": {
        "紫微": "…single-star judgment…",
        "火星m": "…male-specific judgment…",   // star+m / star+f gender split
        "火星f": "…female-specific judgment…"
      },
      "combination_star": [
        {
          "stars": ["紫微", "天府"],     // unordered set, subset matching
          "description": "…combination judgment (outranks single star)…"
        }
      ]
    }
  }
}
```

Engineering highlights of the matching engine:

1. **Unordered subset matching**: `_match_stars()` uses set theory to test whether the board's stars hit a combination, order-independent.
2. **Priority ordering**: multi-star combinations outrank single stars; more specific judgments output first.
3. **Gender routing**: auto-detects `star+m` / `star+f` and picks the clause by the querent's gender.
4. **Smart connectors**: "且" between four-transformation stars, "、" between regular stars, "坐" (not "落") for the twelve longevity shensha.
5. **Empty-value filtering**: drops empty descriptions and malformed entries.

> **Purple Star is no longer a pile of if-else but layers of maintainable star data, topical judgments, and graphical charts.** Adding a judgment only edits JSON — the core advantage of "data-driven" over "hard-coded."

### I-Ching / LiuYao: multi-reading, multi-path parallel analysis

The orchestration core is `divination_hexagram/Divination.py` (`LyMs`). Its strength is not a single "one-hexagram reading" but parallelizing multiple reading paths into one multi-perspective report.

#### 1. Main text output interfaces

- Natal analysis: `lypd_ly()`
- Annual analysis: `lypd_ln()`
- Full comprehensive analysis: `lypd_all()`
- Single-topic report: `get_topic_report(topic)` / `lypd_topic(topic)`
- All-topic classified reading: `lypd_topic_all()`

#### 2. Integrated multi-path reading

`lypd_all()` is not simple text concatenation; it integrates hexagram charting, ZhouYi judgments, five classical books (Bu Shi Zheng Zong / Huang Jin Ce / Huo Zhu Lin / Zeng Shan Bu Yi / Yi Yin), Xiao Liu Ren, GanZhi numerology, Zhuge numerology, TaiJi numerology, and domino numerology into one report.

#### 3. Topical structure

`lypd_ly()` / `lypd_all()` show clear topical splitting: character & appearance, study, career, wealth, relationships, relatives (parents / siblings / children), health, yang dwelling, yin dwelling. This matches the project's "topical organization" style across modules.

#### 4. Desktop actions

`LY_Widget.py` maps natal / annual / full analysis and the unified result dialog; casting input supports 3-number, mystic-number, hexagram input, time casting, and moving-line input.

#### 5. Visible samples (anonymized)

- I-Ching · comprehensive · TXT: ~`6,751` chars
- I-Ching · multi-reading · TXT: ~`3,143` chars

So the LiuYao module already has comprehensive export, multi-reading export, and anonymized sample archiving.

### Auspicious Date: topical selection, calendars, and compatibility

The wrapper core is `date_selection/ZR_3Ms.py`. It is more like a date-analysis engine organized around event topics than a common almanac lookup.

#### 1. Main text output interfaces

- perpetual calendar output
- full-year lunar info
- topical date selection (by topic key)
- compatibility reference
- topic metadata enumeration

These correspond to four output modes: a continuous calendar from the start date to the same date next year, a year-range lunar calendar, single-topic date filtering, and two-BaZi compatibility reference.

#### 2. Rule organization

The real value is the backend layering: groups (`_RAW_TOPIC_GROUPS`), display order (`TOPIC_GROUPS`), topic-to-rule normalization (`TOPIC_RULES`), per-topic good/bad signals (`_TOPIC_SIGNALS`), and a rule dispatch table (`_TOPIC_RULE_DISPATCH`).

> **The date module converts traditional clauses into a groupable, filterable, computable, explainable rule system.**

### Nameology / numerology: Chinese nameology, generation, divination, three-system numerology

The wrapper centers are `nameology_cn/Name_Ms.py` (`Nm`) and the Western entry `nameology_west/Numerology_All.py`. Its output types are more varied than other systems, which is exactly why it shows product-design ability.

#### 1. Chinese nameology interfaces

- Name analysis: `analyse_name()`
- Selected-year analysis: `analyse_selected_year()`
- Personal name generation: `generate_personal_name()`
- Company naming: `generate_company_name()`
- Character divination: `character_divination()`
- Number analysis: `analyse_number()`

#### 2. English numerology interfaces

For an English name, it auto-routes to a combined report across three systems: `analyse_all_name(...)`, `analyse_all_name_only(...)`, `analyse_all_selected_year(...)`, covering Pythagorean, Cheiro / Chaldean, Vedas.

#### 3. Where the engineering substance is

The point worth emphasizing is not "it analyzes names" but: it has both rule judgment and generation tasks; naming is candidate-pool generation with a filtering pipeline, not random stitching; Chinese and English capability lines coexist; the data layer is very heavy (poetry corpora, stroke systems, industry data, 81-number theory, three-talents mapping).

### Tie Ban: natal and annual entries landed, more layers evolving

The Tie Ban module centers on `destiny_shenshu/TBNUM_Ms.py`. The desktop leans toward "natal + annual" output (chart, natal analysis, annual analysis), with placeholder entries for full / decade / professional reading.

> **Tie Ban already has two core output paths — natal and annual — with full/decade layers continuing to extend on the existing architecture.**

### Shao Zi: the most complete numerology module — natal, decade, annual, full

Shao Zi is currently the most complete numerology branch; the wrapper core is `destiny_shenshu/SZNUM_Ms.py`, with natal charting, natal analysis, decade analysis, annual analysis, and full comprehensive analysis.

Anonymized samples include:

- Shao Zi · comprehensive · TXT: ~`18,953` chars
- Shao Zi · decade · TXT: ~`3,293` chars
- Shao Zi · full · Markdown: ~`5,372` chars

From the "is it already an engineering artifact" angle, it is quite solid.

### Desktop Actions at a Glance (seven systems)

Collapsing the scattered method-level interfaces into one table makes it clearer which actions each system actually exposes, which wrapper method backs them, and what status they are in.

| System | Desktop action | Wrapper method | Status |
|---|---|---|---|
| Four Pillars | natal / brief / decade / annual / monthly | `bzms_num` / `bzmss_num` / `dyms_num` / `lnms_num` / `lyms_num` | Landed |
| Four Pillars | open Purple Star chart from birth data | `show_chart_from_bazi` → `ZwdsUnifiedChartDialog` | Landed |
| BaZi manual | natal / decade / annual / monthly (GanZhi input) | `bzms_gz` / `dyms_gz` / `lnms_gz` / `lyms_gz` | Landed |
| Purple Star | natal topics / 12 palaces / annual topics | `zwms_num` / `zwg12ms_num` / `zwlnms_num` | Landed |
| Purple Star | unified chart (4-layer + save) | `show_unified_chart` → `ZwdsUnifiedChartDialog` | Landed |
| Purple Star | all-decade / all-annual analysis | `zwdxms_num` (reserved) | Evolving (placeholder) |
| I-Ching | natal / annual / full analysis | `lypd_ly` / `lypd_ln` / `lypd_all` | Landed |
| I-Ching | single / all-topic classified reading | `get_topic_report` / `lypd_topic` / `lypd_topic_all` | Landed |
| Date Selection | topical date / calendar / compatibility | `get_topic_date` / `wan_nian_li_str` / `get_marriage_compatibility` | Landed |
| Nameology | analysis / year / generate / company / character / number | `analyse_name` / `analyse_selected_year` / `generate_personal_name` / `generate_company_name` / `character_divination` / `analyse_number` | Landed |
| Nameology | English three-system numerology | `analyse_all_name` / `analyse_all_selected_year` | Landed |
| Tie Ban | chart / natal / annual | `pp_sz` / `pd_sz` / `pd_ln` | Landed |
| Tie Ban | full / decade / professional reading | — | Evolving (placeholder) |
| Shao Zi | natal / decade / annual / full | `pd_sz` / `pd_dy` / `pd_ln` / `pd_all` | Landed |

This table itself shows the project's engineering attitude: capability boundaries are explicit — what has landed is marked landed, what is a placeholder is marked so — rather than the README claiming every button is "done."

---

## Standalone Engines: YanQin, QinXing, Tarot

Beyond the seven desktop systems, the project has distilled three **standalone library engines**. They currently exist as extension capabilities, not yet integrated into the desktop app, and they show that the rule-modeling ability transfers horizontally to new metaphysics systems.

### YanQin natal reading (`destiny_yanqin/`)

A natal system based on *Yan Qin Tong Zuan* (Siku Quanshu edition) and *Qin Xing Yi Jian*:

- year/month/day/hour birds, the 28 lunar mansions
- five-star reading: main, fetal, life, body, longevity
- decade and shooting-star quick lookup
- classical lookups: devour, gaining-ground, structure matching, prosperity/taboo, ancient cases, judgments, annotations
- topical reports: character, career, wealth, marriage, health, relatives; plus natal, decade, annual reports

### QinXing event divination (`divination_yanqin/`)

An event-divination system based on *Qin Xing Yi Jian* (Ming dynasty, by Chi Benli), using the **seven-cycle JiaZi board and the flip-bird turn-general method**:

- time-bird board setting: seven cycles × seven luminaries determine the starting mansion at the Zi hour
- flip-bird turn-general: deriving primary/secondary generals and one's own bird via forward/reverse sequencing
- event topics: marriage, wealth, career, health, travel, lost items, childbirth, planning, war
- the seven-cycle anchor is validated against an actual calendar date

### Tarot (`divination_tarot/`)

Based on *The Pictorial Key to the Tarot* (A. E. Waite, 1910):

- deck: 78 cards (22 Major + 56 Minor Arcana), with upright/reversed meanings, image descriptions, Major-Arcana astral correspondences, and suit-element themes
- spreads: Celtic Cross (10 cards, with inner/outer tension and timeline synthesis), the Waite original Celtic Cross, three-card (past / present / future), daily single card
- reports follow the project's ☆ topic / § sub-item structure, compatible with the AI analysis interface
- a `seed` reproduces a given draw

---

## Shared Interaction and Common UI Layer

Looking only at business modules, it is easy to read the project as "a lot of metaphysics code glued together." What truly makes it a product is the shared UI layer (`ui/`). This layer is very worth discussing on a résumé because it shows the project is not "feature stacking" but has a unified interaction skeleton.

### 1. `shared_ui.py`

It centralizes the most core common components:

- `WorkerThread`: runs heavy analysis on a background thread so the main UI does not freeze
- `TranslationThread`: multilingual translation operations
- `ResultDialog`: unified result display, copy, export, and an AI-reading entry
- `get_case_save_input()`: category and notes input before saving a case
- `CompactTitleGroupBox`: unified local-container visual style

It is easy to overlook this layer, but for software engineering it means: modules do not each write their own thread model or result dialog, case-saving interaction is unified, and UI details are not scattered across every widget.

### 2. `ai_analysis_dialog.py`

This file is not "the model call itself" but the desktop AI comprehensive-analysis dialog, carrying model selection, analysis progress, result display, and export. AI is not hidden in a backend function — it is brought into the product interaction layer.

### 3. `case_notes.py`

A floating case-notes window, used to view, edit, and overwrite-save notes after loading a case from case management. Not flashy, but it strongly reflects long-term use rather than a one-off demo.

### 4. `app_bootstrap.py` and `icons/`

Handles icon setup, app-startup helpers, and default fallback icon logic; a dedicated icons directory shows the desktop already has recognizable visual assets, not a dev-only window.

---

## Support Layer: A Reuse Core, Not a Backdrop

When showcasing, many only look at "metaphysics features." But what truly makes this a software platform is the support infrastructure below.

### `lunar_solar/`: the time engine shared by nearly all modules

This directory is not a corner piece but the foundational calendar library every module depends on. It provides:

- solar / lunar conversion
- solar terms, GanZhi, EightChar
- decade / annual / monthly base objects
- traditional cultural calendars (Buddhist, Taoist, the Nine-Nines, the dog days, etc.)
- reverse lookup of solar time from four pillars

For BaZi, Purple Star, LiuYao, date selection, nameology, and numerology, if this layer is wrong, all upper logic drifts with it. So its engineering meaning is not "a utility library" but:

> **The project converges high-sensitivity primitives — time, solar terms, GanZhi — into one shared foundation, instead of letting each module compute its own.**

### `case_character/`: turning "one analysis" into "long-term research and archiving"

The case module deserves separate emphasis, because many divination programs end up stuck at "compute once and done." This one does not. It already supports:

- system grouping, categorization, keyword search
- case add / edit / delete
- JSON import/export, Excel import/export
- unified Markdown / TXT export
- reload a case back into its module to continue analysis

Supported systems cover Four Pillars, BaZi manual, Purple Star, I-Ching, Date Selection, Nameology, Tie Ban, and Shao Zi. From a product view, this upgrades the repo from a "calculator" to a "research workbench."

> Note: the case database `cases.db` is local user data, a private asset, and is not in this public showcase.

### `ai/`: connecting rule reports to a modern LLM workflow

The AI layer is no longer a single `call_openai()` file but is split into:

- `analysis/`: AIAnalyzer, per-topic analysis threads, parse retries
- `providers/`: OpenAI-compatible, Claude, Gemini, Qwen provider abstractions
- `analysis_graph.py`: LangGraph-style analysis flow
- `prompts/` + `prompt_manager.py`: prompt rules and a compatibility layer
- `topic_schema.py`: report topic-split rules
- `core/`: cache, token, runtime infrastructure

> **In this project, AI does not replace the rule system — it is a second analysis layer built on top of rule reports.** The rule layer first produces a traceable raw report; the model then splits it by topic (☆ markers) for interpretation, synthesis, and real-world advice. Real API keys go through environment variables / `.env` and never enter the repo.

---

## Real Artifacts Visible in the Public Repo

To avoid the intro looking like "all capability description, no evidence," here is a summary of the artifact types actually visible in the repo. All samples are anonymized.

### 1. Long structured report samples

Currently visible: Four Pillars natal / annual / comprehensive, I-Ching comprehensive / multi-reading, Shao Zi decade / comprehensive / full.

Sample character counts:

- Four Pillars natal: ~`36,035` chars
- Four Pillars template: ~`30,142` chars
- Shao Zi comprehensive: ~`18,953` chars
- Four Pillars annual: ~`10,246` chars
- I-Ching comprehensive: ~`6,751` chars

### 2. Graphical artifacts

Clearly displayable: the Purple Star unified chart, the Purple Star chart opened via Four Pillars linkage, and desktop module screenshots.

### 3. Case-archive artifacts

Clearly present: Markdown reports, TXT reports, the SQLite case library, and the JSON / Excel import-export pipeline.

### 4. Modules with few public samples but existing capability interfaces

Modules with fewer or no retained public samples include Purple Star, Date Selection, Nameology, and Tie Ban. This does not mean they lack output capability — it means the anonymized samples retained in the public repo are mainly concentrated in Four Pillars, LiuYao, and Shao Zi. This distinction belongs in the showcase README because it is more credible than claiming "all modules already have public samples."

---

## Not a Single-Module Script, but a Complete Product

The most worth-emphasizing point is not "how many divination types it supports" but that it already has a complete product pipeline.

### Unified desktop experience

- 9 main pages in one PySide6 desktop app
- modules share threads, dialogs, save logic, and the icon-startup mechanism
- despite very different rules, the interaction experience stays unified

### Unified case system

- all main modules can save cases
- cases can be categorized, searched, annotated, sorted, imported, exported
- a case can be reloaded into its module to continue analysis

### Unified report output

- Markdown / TXT export
- a unified formatter per content type
- output is both human-readable and usable as AI input

### Unified AI analysis layer

- the rule layer produces the raw report
- it is split into structured topical segments
- different models then do interpretation, synthesis, and real-world advice

This pipeline means the project is not "rule system" and "AI calls" fighting separately but organized into one complete workflow.

---

## Technical Capabilities Demonstrated

As a résumé project, it fairly completely demonstrates the following.

### 1. Complex rule-system modeling

Breaking a large body of traditional knowledge into executable functions, clause data, topic mappings, report templates, and multi-layer derivation logic. The biggest difference from ordinary business systems is that it requires **translating unstructured knowledge into structured rules**.

### 2. High-complexity desktop app development

Not a one-off script but a multi-page, long-pipeline, continuously usable desktop app: PySide6 UI organization, background threads with result callbacks, non-modal result dialogs, graphical chart display, and shared cross-module interaction.

### 3. Data-driven design

Heavy use of JSON and structured data instead of hard-coded logic, especially in Purple Star judgments, BaZi classical clauses, I-Ching reference mapping, nameology corpora and number data, and date-selection topic rules. It shows a focus on long-term maintainability.

### 4. AI system integration

AI here is not "call one API and done" but a full middle layer: provider abstraction, OpenAI-style compatibility, prompt management, topic splitting, analysis flow, and result validation. Closer to AI integration in a real product than a demo.

### 5. Local data and workflow design

The SQLite case library, JSON/Excel import-export, report export, and case reload show: the project considers long-term use rather than a single run, balances research, archiving, comparison, and reuse, and has clear "desktop productivity tool" properties.

### 6. Organizing and refactoring a large codebase

~109K lines of Python, 210 files, 486 JSON, inheritance up to 5 levels deep (`Gz → Bz → BzDy → BzLn → BzLy`). The project recently completed a modularization refactor: unified English domain prefixes, splitting the I-Ching core from orchestration, splitting Chinese/Western nameology, and isolating small number-divination packages. That itself is hands-on experience in "sustainably evolving a large legacy codebase."

---

## How to Frame It on a Résumé

As a résumé project, it can be framed as:

> **A desktop-first traditional metaphysics analysis platform that converts knowledge-dense classical rule systems into executable software, structured reports, reusable case-management workflows, and AI-assisted interpretation pipelines.**

Quantifiable highlights:

- 7 desktop metaphysics systems + 3 standalone engines, unified in a single PySide6 app
- ~109K lines of Python, 486 JSON data files
- up to 330 rule methods in a single module (the BaZi GanZhi base)
- data-driven judgment libraries (793 flying-star clauses in Purple Star + 1000+ star-combination clauses)
- a complete pipeline: rule engine → structured report → case archive → multi-provider AI reading

---

## Design Principles

Several design principles run through all modules and are the root reason the codebase stays consistent across seven systems.

1. **Rules first, AI second**: every topical report is first produced by the deterministic rule engine as traceable raw text; AI only interprets and synthesizes on top, never "improvising" new conclusions.
2. **Separate data from logic**: judgments, clauses, and corpora are distilled into JSON / corpora; code only matches, assembles, and orchestrates — new content does not change code.
3. **Converge the calendar into one foundation**: high-sensitivity capabilities (time, terms, GanZhi, EightChar) are implemented once in `lunar_solar` and reused everywhere, avoiding convention drift.
4. **Topical output**: all reports use the unified ☆ topic / § sub-item structure, easy for humans to read and for AI to split.
5. **Unified interaction skeleton**: thread model, result dialog, case save, notes, and icon startup live in `ui/`; business modules do not reinvent the wheel.
6. **Honestly distinguish "landed" from "evolving"**: the wrapper may reserve interfaces, but the desktop clearly marks what is done versus a placeholder — capabilities are not maxed out by copy.
7. **Long-term use over one-off demo**: cases can be saved, searched, reloaded, and exported; the system is a "research workbench," not a "compute-once calculator."

---

## Recent Refactor Notes

The project recently completed a sizable modularization refactor — itself a demonstration of engineering ability, safely renaming, splitting, and migrating modules across a ~109K-line codebase without functional regression.

- **Unified English domain prefixes**: core directories became `destiny_*`, `divination_*`, `nameology_*` for consistent, clear naming.
- **Calendar engine cleanup**: unified into the lowercase package `lunar_solar`, imported uniformly by all modules.
- **I-Ching layering**: split into `divination_iching` (hexagram core + ZhouYi + 64-hexagram corpus) and `divination_hexagram` (LiuYao orchestration + 5 classical books).
- **Small number-divination packages isolated**: Xiao Liu Ren, GanZhi, Zhuge/TaiJi, and domino numerology each their own package, invoked on demand by the orchestration layer.
- **Nameology split East/West**: `nameology_cn` and `nameology_west` decoupled; the desktop routes by input language.
- **YanQin split**: `destiny_yanqin` (natal reading) and `divination_yanqin` (event divination) each take their role.
- **Docs synced**: the main repo's `CLAUDE.md`, root `README.md`, and 20 sub-module `README.md` files were all aligned to the new structure.

---

## Glossary

For readers without a metaphysics background, here are minimal explanations of frequent terms (functional, engineering-context explanations only, not full doctrinal definitions).

| Term | One-line understanding |
|---|---|
| GanZhi | 10 Heavenly Stems × 12 Earthly Branches form a 60-cycle, used for year/month/day/hour |
| Four Pillars / BaZi | the four GanZhi pairs of birth (8 characters), the input for chart computation |
| Natal chart | the base chart fixed at birth |
| Decade fortune | life stages of roughly 10 years each |
| Annual / monthly | fortune of a given year / month |
| Shensha | symbolic markers with specific auspicious/inauspicious meaning (e.g. Tian Yi noble, Yang Blade) |
| Geju (structure) | the overall structural type of a chart |
| Twelve palaces | Purple Star divides the chart into 12 life domains (self, wealth, career, etc.) |
| Four transformations | Lu / Quan / Ke / Ji — four transformation states of stars |
| LiuYao | casting with three coins or numbers to get a hexagram of six lines |
| Primary / changed hexagram | the initial hexagram and the one after moving lines change |
| Six relatives / six spirits / world-response / NaJia | systems annotating line relations and attributes in LiuYao |
| Date selection | choosing an auspicious date for an event (marriage, groundbreaking, travel) |
| Five-grid / three-talents | the numeric structure computed from strokes in nameology |
| Numerology (shenshu) | traditional systems (Tie Ban, Shao Zi) that derive fate from numbers |

---

## FAQ

**Q: Can this repo run directly?**
A: No. This is a public showcase repo with only documentation and screenshots — no source, data, or config.

**Q: Why build metaphysics as software?**
A: The project focuses on the engineering problem — translating unstructured traditional knowledge into reviewable, versionable, maintainable structured rules and data, layered with modern calendar computation, case management, and an AI workflow.

**Q: Does the AI "make up" conclusions?**
A: It does not bypass the rule layer. AI only interprets, synthesizes, and advises on top of traceable rule-engine reports; it does not produce the raw judgments.

**Q: Is it accurate?**
A: Accuracy is not the selling point; the project provides traceable, reviewable rule output. Whether to adopt any judgment is the user's call. It is not real-world decision advice (see disclaimer).

**Q: Are the cases real people?**
A: No. Every case in this document and the screenshots is an anonymized sample referring to no real individual.

**Q: Which language does the desktop app use?**
A: The desktop UI and reports are primarily in Chinese (the domain is Chinese metaphysics), with an English numerology path and a translation entry in the result dialog. The Western numerology module produces English reports directly.

**Q: How are the seven systems kept consistent?**
A: Through shared infrastructure — one calendar engine, one case system, one result-dialog and thread model, and one ☆ topic / § sub-item report convention. Each system differs in rules but not in product shape.

**Q: Is the project still evolving?**
A: Yes. The desktop honestly marks placeholder actions (e.g. all-decade analysis in Purple Star and Tie Ban), and the codebase recently went through a modularization refactor (see [Recent Refactor Notes](#recent-refactor-notes)).

---

## Showcase Boundaries

For the protection of knowledge assets, commercialized implementation, and user data, the public showcase repo does **not** provide:

- project source code
- rule data and clause libraries
- the SQLite case database
- API configuration or keys
- implementation details that could directly reproduce the full capability

The goal of this repo is to demonstrate: project scope, product capability, engineering depth, system architecture, and UI results. Every case, name, and report sample in this document is an **anonymized sample** referring to no real individual, used only to illustrate the system's output form and scale.

---

## Disclaimer

This project is for the demonstration of traditional-culture digitization, rule engineering, desktop software design, and AI workflow practice.
Its output comes from program rules, structured data, and AI summaries, and does not constitute medical, legal, investment, marital, or any other real-world decision advice.
Traditional metaphysics content should be used for cultural research and personal reference, and should not replace professional opinion or factual investigation.
