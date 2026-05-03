<h1 align="center">MetaphysicsQuant</h1>
<p align="center">
  <a href="README.md">Main</a> |
  <a href="README/README_CN.md">简体中文</a> |
  <a href="README/README_ZH_TW.md">繁體中文</a> |
  <a href="README/README_YUE.md">粵語</a> |
  <a href="README/README_EN.md">English</a>
</p>

<p align="center">
  <a href="https://img.shields.io/github/stars/lyzhk/MetaphysicsQuant?style=for-the-badge"><img alt="GitHub stars" src="https://img.shields.io/github/stars/lyzhk/MetaphysicsQuant?style=for-the-badge"></a>
  <a href="https://img.shields.io/github/forks/lyzhk/MetaphysicsQuant?style=for-the-badge"><img alt="GitHub forks" src="https://img.shields.io/github/forks/lyzhk/MetaphysicsQuant?style=for-the-badge"></a>
  <a href="https://img.shields.io/github/license/lyzhk/MetaphysicsQuant?style=for-the-badge"><img alt="License" src="https://img.shields.io/github/license/lyzhk/MetaphysicsQuant?style=for-the-badge"></a>
  <a href="https://img.shields.io/badge/Python-3.10%2B-3776AB?style=for-the-badge&logo=python&logoColor=white"><img alt="Python 3.10+" src="https://img.shields.io/badge/Python-3.10%2B-3776AB?style=for-the-badge&logo=python&logoColor=white"></a>
</p>

> **展示说明**：本仓库只用于项目介绍与成果展示，不包含任何项目源码、数据文件、案例数据库或 API 配置。

MetaphysicsQuant 不是一个只会显示四柱、星盘或卦盘的排盘工具。它把中国传统术数中最难工程化的部分做成了可运行的软件系统：历法换算、干支推导、神煞与格局规则、古籍条文检索、专题化报告、AI 二次解读、SQLite 案例库、Markdown/TXT 导出和桌面端完整工作流。

当前稳定主线是 `mainAppUI.py` 的 PySide6 桌面应用；`mainAppUI_modern.py` 是注册表驱动的现代化外壳；`mainWebUI.py` 和 `web_platform/` 保留为 Web 方向代码。

最后更新：2026-05-03

## 目录

- [核心功能概览](#核心功能概览)
- [界面截图](#界面截图)
- [四柱八字核心能力](#四柱八字核心能力)
  - [1. 两套入口](#1-两套入口)
  - [2. 干支规则底座](#2-干支规则底座)
  - [3. 七柱论命](#3-七柱论命)
  - [4. 古籍与数据来源](#4-古籍与数据来源)
  - [5. 可生成的报告](#5-可生成的报告)
- [其他术数模块](#其他术数模块)
  - [紫微斗数](#紫微斗数)
  - [易经解卦与六爻](#易经解卦与六爻)
  - [择日合婚](#择日合婚)
  - [姓名学与西文数理](#姓名学与西文数理)
  - [铁板神数、邵子神数](#铁板神数邵子神数)
- [AI 分析与报告系统](#ai-分析与报告系统)
- [案例管理与导出](#案例管理与导出)
- [工程实现能力](#工程实现能力)
- [项目架构](#项目架构)
- [仓库规模](#仓库规模)
  - [工程目录统计](#工程目录统计)
- [子模块文档导航](#子模块文档导航)
- [安装与启动](#安装与启动)
- [免责声明](#免责声明)

## 核心功能概览

这个项目的定位是“传统术数知识库 + 规则引擎 + 桌面分析系统”，重点是把大量分散在古籍、民间诀法和现代排盘经验里的规则，转成可复查、可保存、可扩展的程序输出。

已实现的实用功能：

| 能力 | 已实现内容 |
|---|---|
| 四柱八字 | 数字排盘、干支手输、原局、大运、流年、流月、胎元、命宫、身宫、七柱专题论命、串宫压运、紫微联动。 |
| 神煞与格局 | `SZBZ_1Gz.py` 中有 330 个方法，其中约 180 个与神煞、贵格、凶格、刑冲合会、串宫压运等判定直接相关。 |
| 古籍规则库 | 四柱模块数据覆盖《三命通会》《滴天髓》《穷通宝鉴》《神峰通考》《五行精纪》《鬼谷子》《袁天罡称骨》等。 |
| 紫微斗数 | 十二宫排盘、主辅杂曜、四化、星曜亮度、大限、流年、流月、排盘图保存、星曜组合匹配。 |
| 易经六爻 | 时间起卦、三数起卦、玄机数起卦、本卦变卦、动爻、六亲、六神、世应、纳甲、六十四卦资料。 |
| 择日合婚 | 万年历、年历、主题择日、婚嫁、求职、开业、求财、出行、求医、入宅、求学、求子、合婚参考。 |
| 姓名号码 | 中文姓名学、康熙/新华笔画、五格三才、八十一数理、个人起名、公司起名、测字、号码分析。 |
| 西文数理 | Pythagorean、Cheiro/Chaldean、Vedas 三体系合并报告，支持英文姓名与选年分析。 |
| 神数系统 | 铁板神数、邵子神数数字推演，支持条文检索、原局、大运、流年和综合分析。 |
| 案例系统 | SQLite 案例库、分类、搜索、备注、加载回填、JSON/Excel 导入导出、Markdown/TXT 报告导出。 |
| AI 解读 | 按报告专题拆分内容，调用 OpenAI-compatible、Claude、Gemini、OpenRouter、DeepSeek、Qwen、SiliconFlow 等供应商。 |

项目输出不是一句“吉凶如何”的短评，而是可展开的结构化资料。例如当前仓库中的四柱原局报告样本已经达到 3 万字量级，包含排盘信息、七柱专题、古籍条文、神煞组合、运限和 AI 解读入口。是否最终采用某条断语，仍由使用者结合现实背景判断。

## 界面截图

以下截图来自当前桌面端程序，按主要专题模块展示实际界面形态。

<table>
  <tr>
    <td align="center"><strong>四柱八字</strong><br><img src="image/four_pillars_destiny.png" alt="四柱八字界面" width="900"></td>
  </tr>
  <tr>
    <td align="center"><strong>紫微斗数</strong><br><img src="image/purple_star_astrology.png" alt="紫微斗数界面" width="900"></td>
  </tr>
  <tr>
    <td align="center"><strong>易经解卦</strong><br><img src="image/hexagram_divination.png" alt="易经解卦界面" width="900"></td>
  </tr>
  <tr>
    <td align="center"><strong>择日合婚</strong><br><img src="image/auspicious_date.png" alt="择日合婚界面" width="900"></td>
  </tr>
  <tr>
    <td align="center"><strong>姓名号码</strong><br><img src="image/nameology.png" alt="姓名号码界面" width="900"></td>
  </tr>
  <tr>
    <td align="center"><strong>铁板神数 / 邵子神数</strong><br><img src="image/esoteric_numerology.png" alt="铁板神数与邵子神数界面" width="900"></td>
  </tr>
  <tr>
    <td align="center"><strong>案例管理</strong><br><img src="image/character_case.png" alt="案例管理界面" width="900"></td>
  </tr>
</table>

## 四柱八字核心能力

四柱八字是当前仓库最重的核心模块：`four_pillars_destiny/` 约 2.88 万行 Python，15 个 JSON 数据文件。它的价值不在“排出八个字”，而在排盘之后的大规模规则整理和报告生成。

### 1. 两套入口

- `四柱八字`：输入姓名、性别、公历/农历年月日时分，自动换算四柱、起运、大运、流年、流月。
- `四柱批命`：手动输入年柱、月柱、日柱、时柱、大运、流年、小限、流月，适合古籍案例、已知八字反查和课堂推演。

### 2. 干支规则底座

`four_pillars_destiny/SZBZ_1Gz.py` 是四柱系统的规则地基，覆盖：

- 天干、地支、藏干、五行、阴阳、六十甲子、纳音、旬空。
- 十神、十二长生、禄命长生、纳音长生、四贵四平四忌。
- 天乙贵人、福星贵人、太极贵人、文昌贵人、天德、月德、天喜、驿马、华盖、金舆、学堂、词馆、截路空亡、鬼门关、沐浴杀、暴败、自缢、四废、官符、死符、病符、血光、离乡、劫煞、亡神、羊刃、元辰、空亡、咸池、天罗地网、孤辰寡宿等大量神煞与格局判定。
- 串宫压运十二神：太岁、青龙、丧门、六合、官符、小耗、大耗、朱雀、白虎、贵神、吊客、病符，并实现神煞变化规则。
- 盲师神煞与民间经验规则，例如四穷日、庄杀、罗杀、忌杀、八败、悬梁杀、胞胎杀、铁刑杀、天扫星、地扫星、追魂、铲度等。

这里适合展示项目实力：这些不是 UI 文案，而是被拆成函数和数据结构的规则引擎。

### 3. 七柱论命

`four_pillars_destiny/SZBZ_2Bz.py` 在传统年月日时四柱之外，继续纳入胎元、命宫、身宫，形成“七柱”分析视角。报告按专题组织：

- 性格信息
- 学业信息
- 事业信息
- 财运信息
- 诀法信息
- 婚姻信息
- 六亲信息：父亲、母亲、兄弟、子女、其他亲属
- 伤灾健康
- 阳宅阴宅

这些专题不是单一流派硬套，而是按来源分层拼接，例如苏氏盲派、民间盲派、五行精纪、三命通会、玉照神应真经、梁派理论、鬼谷子分定经、三世演禽等。README 里强调“实事求是”：项目提供可追溯的规则输出，不宣称替代现实决策。

### 4. 古籍与数据来源

四柱模块的 `data/` 目录保存了多类规则与条文数据：

- `SanMingTongHui.json`：《三命通会》
- `DiTianSui.json`：《滴天髓》
- `QiongTongBaoJian.json`：《穷通宝鉴》
- `ShenFengTongKao.json`：《神峰通考》
- `WuXingJingJi.json`：《五行精纪》
- `GuiGuZi_LTQ.json`、`GuiGuZi_MGB.json`：鬼谷子分定经、鬼谷子命宫表
- `YuanTiangangCG.json`：袁天罡称骨
- `SanShiYanQin.json`：三世演禽
- `SuShiMangPai.json`：苏氏盲派
- `DaMoYiZhangJing.json`、`JueFa.json`、`Books.json` 等补充数据

代码中也直接引用《渊海子平》《兰台妙选》《玉照神应真经》《永乐大典》《天元巫咸经》等来源或规则名。展示时可以说：这是一个把多种典籍、诀法和程序规则合并成专题报告的工程项目。

### 5. 可生成的报告

四柱封装层 `SZBZ_6BzMs.py` 支持：

- 原局命书：`bzms_num()` / `bzms_gz()`
- 简断命书：`bzmss_num()`
- 大运命书：`dyms_num()` / `dyms_gz()`
- 流年命书：`lnms_num()` / `lnms_gz()`
- 流月命书：`lyms_num()` / `lyms_gz()`
- 从当前年份起的 10 年流年中批：`zpln_num()`
- 流年与大运交接分段、流月与大运交接分段
- 可选紫微斗数联动，生成原局、大限、流年排盘图并保存图片

仓库中已有脱敏示例报告，如 `character_case/CaseReports/示例案例/示例案例_四柱八字_原局分析_20260421_043836.md`，字符量约 3.6 万；`character_case/CaseReports/A参考模板/示例案例_四柱八字_原局分析_20260421_031317.txt` 约 3.0 万字符。这说明系统实际可以输出长篇结构化报告，而不是停留在功能设想。

## 其他术数模块

### 紫微斗数

`purple_star_astrology/` 实现十二宫排盘、主星辅星杂曜、四化、星曜亮度、大限、流年、流月和排盘图。`Star_Combination_Matcher.py` 负责从 JSON 数据中匹配单星、组合星和男女差异化解释。专题数据覆盖性格、财富、婚姻、事业、健康、父母、母亲、兄弟、子女、田宅、迁移、交友等。

### 易经解卦与六爻

`hexagram_divination/` 支持时间起卦、三数起卦、玄机数、玄卦输入、本卦、变卦、动爻、六亲、世应、六神、纳甲和流年解卦。`notion/` 下保存 64 卦 Markdown 文档，`data/` 下保存《易经》资料、小六壬、诸葛神数、干支神数、太极神数、牙牌神数等映射。

### 择日合婚

`auspicious_date/` 不是简单黄历查询，而是按主题筛选日期。已覆盖婚嫁、纳采问名、安床、上官赴任、临政亲民、开业开市、求财、立契交易、提车、宴会、求学、考试、入学、拜师、出行、求医、入宅、祭祀、求子等场景。规则中可见《协纪辨方书》《玉匣记》和其他民俗择日条文。

### 姓名学与西文数理

`nameology/` 覆盖中文姓名学和西文数理：

- 中文姓名学：康熙/新华笔画、五格、三才、八十一数理、五行、阴阳、生肖、专题断语。
- 起名：个人起名、公司起名，可按喜用五行、规避五行、行业数据筛选。
- 测字与号码：三字测字、手机号/车牌/编号数理分析。
- 西文数理：Pythagorean、Cheiro/Chaldean、Vedas 三体系合并输出。
- 数据层：姓名字库、康熙/新华笔画、三才、五格、八十一数理、行业、西文数理资料，以及诗经、楚辞、论语、唐诗、宋诗、宋词等起名语料。

### 铁板神数、邵子神数

`esoteric_numerology/` 提供铁板神数、邵子神数数字推演。它与西文数理不同，更偏向传统术数中的生辰、干支、刻分、卦象、声音和条文检索。邵子神数支持原局、大运、流年和综合报告；铁板神数支持刻分、考刻和条文输出。

## AI 分析与报告系统

项目没有把 AI 当成“神秘判断器”，而是把 AI 放在工程链路的最后一层：先由规则系统生成可追溯的原始报告，再按专题拆分给模型做解释、归纳和现实建议。

`ai/` 模块的能力包括：

- 供应商抽象：OpenAI、Claude、Google Gemini、OpenRouter、DeepSeek、DashScope 千问、SiliconFlow。
- OpenAI-compatible 支持：可接入 OpenRouter、DeepSeek、硅基流动等兼容 chat/completions 的服务。
- LangChain/LangGraph 风格工作流：有依赖时使用图式调用，缺依赖时回退 REST。
- 专题拆分：`topic_schema.py` 根据报告模板拆分原局、大运、流年、流月、邵子等不同结构。
- 提示词管理：`modern_prompts.py` 和 `prompt_manager.py` 将输出约束到“现实建议、风险边界、证据来源”，避免纯术士化口吻。
- 密钥管理：真实 API Key 走 `AI/.env` 或环境变量，不应提交到仓库。

这部分的展示价值是：项目不是单纯“玄学脚本”，而是传统规则引擎与现代 LLM 工作流的结合。

## 案例管理与导出

`character_case/` 是统一案例系统，默认数据库为 `character_case/cases.db`。它让项目从“算一次”升级为“长期研究与归档”：

- 按系统保存案例：四柱八字、四柱批命、紫微斗数、易经解卦、择日合婚、姓名号码、铁板神数、邵子神数。
- 分类、搜索、备注、排序、拖拽、编辑。
- 从案例管理页重新加载到对应分析界面。
- JSON 备份和 Excel 导入导出。
- `unified_formatter.py` 将分析结果整理为 Markdown 或 TXT，针对八字、紫微、六爻、邵子等系统做格式识别与排版优化。

注意：`character_case/cases.db` 是本地用户数据文件，不应随意覆盖或删除。

## 工程实现能力

这个项目能展示的技术能力包括：

- PySide6 桌面端：稳定入口 `mainAppUI.py`，现代化外壳 `mainAppUI_modern.py`。
- 模块化架构：术数模块、历法模块、案例模块、AI 模块、通用 UI 模块分层清晰。
- 规则引擎：大量传统规则被拆成可读函数、数据表和 JSON 条文库。
- 历法底座：`lunar_solar/` 提供公历/农历、节气、干支、EightChar、大运、流年、流月等基础能力。
- 后台线程：分析过程通过共享 `WorkerThread` 执行，减少 UI 阻塞。
- 数据持久化：SQLite 管理案例，JSON/Excel 做交换格式。
- 报告工程：Markdown/TXT 格式化、专题拆分、AI 分析弹窗、关闭保护。
- Web 预研：`web_platform/` 保留 FastAPI/Vue/部署配置，说明项目具备从桌面端迁移到 Web 平台的基础。

## 项目架构

MetaphysicsQuant 的架构重点是“桌面入口统一调度，核心术数模块独立计算，历法、案例、AI 和 UI 能力作为共享支撑层”。这让每个术数系统既能单独运行，又能接入统一案例库、统一导出和 AI 专题解读。

```text
┌────────────────────────────── 表现层 ──────────────────────────────┐
│ mainAppUI.py                                                       │
│ ├─ 案例管理                                                        │
│ ├─ 四柱八字                                                        │
│ ├─ 紫微斗数                                                        │
│ ├─ 易经解卦                                                        │
│ ├─ 择日合婚                                                        │
│ ├─ 姓名号码                                                        │
│ ├─ 铁板神数                                                        │
│ ├─ 邵子神数                                                        │
│ └─ 四柱批命                                                        │
│                                                                    │
│ mainAppUI_modern.py                                                │
│ └─ ModernMainWindow + NavigationSidebar + module_registry          │
└────────────────────────────────────────────────────────────────────┘
                                  │
                                  ▼
┌──────────────────────────── 交互与通用 UI 层 ───────────────────────┐
│ ui_common/                                                          │
│ ├─ shared_ui.py: WorkerThread、TranslationThread、ResultDialog       │
│ ├─ app_shell.py: 现代化主窗口、案例联动、关闭保护                    │
│ ├─ module_registry.py: 模块注册、分组、案例路由                      │
│ ├─ navigation.py: 侧边栏导航                                        │
│ └─ case_notes.py: 案例备注弹窗                                      │
└────────────────────────────────────────────────────────────────────┘
                                  │
                                  ▼
┌────────────────────────────── 核心业务模块 ─────────────────────────┐
│ four_pillars_destiny/     │ purple_star_astrology/                 │
│ 四柱八字 / 四柱批命       │ 紫微斗数                                │
│                                                                    │
│ hexagram_divination/      │ auspicious_date/                       │
│ 易经解卦                  │ 择日合婚                                │
│                                                                    │
│ esoteric_numerology/      │ nameology/                             │
│ 铁板神数 / 邵子神数       │ 姓名号码 / 西文数理                     │
└────────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌────────────────────────────── 支撑层 ───────────────────────────────┐
│ lunar_solar/                                                        │
│ ├─ 阳历 / 农历转换                                                  │
│ ├─ 节气、干支、EightChar、大运、流年、流月                          │
│ └─ 为四柱、紫微、择日、姓名等模块提供底层日期计算                    │
│                                                                    │
│ character_case/                                                     │
│ ├─ database_manager.py: SQLite 数据库管理                           │
│ ├─ case_manager_widget.py: 案例管理界面                              │
│ ├─ dialogs/: 不同术数系统的案例输入/编辑弹窗                         │
│ └─ unified_formatter.py: Markdown/TXT 导出                          │
│                                                                    │
│ ai/                                                                │
│ ├─ ai_analysis.py: AI 分析 UI、线程、缓存与专题流程                  │
│ ├─ config.py / .env: 供应商配置与本地 API Key                       │
│ ├─ analysis_graph.py: LangGraph 风格调用流程                        │
│ ├─ modern_prompts.py / prompt_manager.py: Prompt 契约与兼容层        │
│ ├─ topic_schema.py: 报告专题拆分规则                                │
│ └─ providers/: OpenAI-compatible / Claude / Gemini / Qwen 客户端     │
└────────────────────────────────────────────────────────────────────┘
```

主流程：

1. `mainAppUI.py` 创建稳定的标签页桌面端；`mainAppUI_modern.py` 创建注册表驱动的现代化外壳。
2. 各业务 Widget 收集输入，调用对应核心分析类，例如 `BzMs`、`ZwMs`、`LyMs`、`ZrMs`、`Nm`。
3. 长计算通过 `ui_common.shared_ui.WorkerThread` 放到后台执行，结果进入 `ResultDialog`。
4. 结果可以保存为案例、导出 Markdown/TXT、进入 AI 专题解读，或者通过案例管理再次回填到模块界面。
5. `lunar_solar/` 作为底层历法引擎，被四柱、紫微、择日、姓名等多个模块复用。

## 仓库规模

按当前本地仓库统计，不含 `.git`、`__pycache__`、`.pytest_cache` 和 `.vscode`：

- Python 文件：`168`
- Python 行数：`95,418`
- JSON 文件：`447`
- `four_pillars_destiny/`：`11` 个 Python 文件，约 `28,844` 行，`15` 个 JSON
- `purple_star_astrology/`：`14` 个 Python 文件，约 `10,439` 行，`20` 个 JSON
- `nameology/`：`11` 个 Python 文件，约 `6,462` 行，`391` 个 JSON
- `ai/`：`15` 个 Python 文件，约 `6,812` 行
- `lunar_solar/`：`42` 个 Python 文件，约 `7,370` 行

### 工程目录统计

| 模块 | Python 文件数 | Python 行数 | JSON 文件数 |
|---|---:|---:|---:|
| 根目录入口 (`mainAppUI.py` / `mainAppUI_modern.py` / `mainWebUI.py`) | 3 | 3,317 | 0 |
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

统计命令示例：

```bash
find . -name '*.py' -not -path './.git/*' -not -path '*/__pycache__/*' -not -path './.pytest_cache/*' | wc -l
find . -name '*.json' -not -path './.git/*' -not -path '*/__pycache__/*' -not -path './.pytest_cache/*' -not -path './.vscode/*' | wc -l
```

## 子模块文档导航

| 模块 | README | 主要职责 | 桌面端入口 |
|---|---|---|---|
| 四柱八字 | `four_pillars_destiny/README.md` | 八字原局、大运、流年、流月、干支手输和古籍规则数据。 | `四柱八字` / `四柱批命` |
| 紫微斗数 | `purple_star_astrology/README.md` | 紫微排盘、十二宫、星曜组合、大限、流年和排盘图。 | `紫微斗数` |
| 易经解卦 | `hexagram_divination/README.md` | 六爻起卦、流年解卦、小六壬、诸葛神数等辅助断法。 | `易经解卦` |
| 择日合婚 | `auspicious_date/README.md` | 万年历、主题择日、吉凶日筛选、合婚参考。 | `择日合婚` |
| 姓名号码 | `nameology/README.md` | 中文姓名学、五格三才、起名、测字、号码、西文数理。 | `姓名号码` |
| 数理神数 | `esoteric_numerology/README.md` | 铁板神数、邵子神数数字推演。 | `铁板神数` / `邵子神数` |
| 案例管理 | `character_case/README.md` | SQLite 案例库、分类、搜索、备注、JSON/Excel 导入导出。 | `案例管理` |
| 阴阳历引擎 | `lunar_solar/README.md` | 公历农历互转、节气、干支、八字、九星、佛历道历。 | 底层支撑 |
| 通用 UI | `ui_common/README.md` | 共享线程、结果弹窗、现代化外壳、模块注册、导航和图标主题。 | 底层支撑 |
| Web 平台 | `web_platform/README.md` | FastAPI/Vue Web 平台、后端接口、前端页面和部署结构。 | Web 入口 |

## 安装与启动

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

测试和检查：

```bash
python tests/test_jieqi_interval.py
python tests/test_unified_formatter_markdown.py
pytest tests
```

AI 能力需要在 `AI/.env` 或系统环境变量中配置对应供应商密钥。不要提交真实 API Key。

## 免责声明

MetaphysicsQuant 用于传统文化数字化、规则工程、软件架构实践和研究展示。项目输出来自程序规则、数据文件和 AI 总结，不构成医疗、法律、投资、婚姻或其他现实决策建议。传统术数内容应作为文化研究和个人参考，不应替代专业意见或事实调查。
