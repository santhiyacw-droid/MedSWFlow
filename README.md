# MedSWFlow

MedSWFlow 是一个面向医务社会工作的案例标准化与个案规划智能工作流框架，让每位医务社工拥有一个懂专业决策流程的 AI 个案助理。

系统首先将非结构化资料转换为五模块标准案例，再依据 ICF、COM-B、BCW 等专业理论，通过六步骤专业工作流自动生成个案计划书。

它不是简单的文本生成工具，而是模拟医务社会工作专业决策过程的 AI 工作流系统。

Python 3.13｜ Open Source

## MedSWFlow 能做什么？

### 标准化案例接入

支持：

- 社工接案记录
- 医院转介单
- 病房日志
- 自由文本案例

自动转换为统一五模块案例格式。

### 五模块案例画像构建

自动提取：

- 服务对象背景与医疗情况
- 社交与家庭背景
- 心理与社会问题
- 资源环境及制度制约因素
- 转介来源

形成后续规划所需的标准案例画像。

### 方案生成

基于标准化案例生成方案：

Step 1. 问题评估（ICF）

Step 2. 问题分析（COM-B + BCW）

Step 3. 服务目标设定

Step 4. 干预方案设计

Step 5. 干预风险预判

Step 6. 成效评估设计

### 多模型适用

支持直接接入API使用，已测试通过：ChatGPT、DeepSeek。

所有模型共享同一案例输入与同一工作流规则。

实现专业契合度对比研究。

## 为什么选择 MedSWFlow？

| 特性  | 说明  |
| --- | --- |
| 不是聊天机器人，而是专业工作流 | AI必须遵循六步骤专业流程 |
| 案例标准化 | 自动构建五模块标准案例 |
| 理论驱动 | ICF + COM-B + BCW |
| 工作流透明 | 每一步均保存结果 |
| 多模型支持 | DeepSeek、GPT 等 |
| 本地运行 | 数据可控 |
| 开源可扩展 | 支持本地部署与二次开发 |

## 双阶段工作流
```text
原始案例
      ↓
┌────────────────────┐
│ Step0 案例标准化    │
└────────────────────┘
      ↓
五模块标准案例
      ↓
┌────────────────────┐
│ Step1 问题评估      │
│ Step2 问题分析      │
│ Step3 目标设定      │
│ Step4 干预设计      │
│ Step5 风险预判      │
│ Step6 成效评估      │
└────────────────────┘
      ↓
个案计划书
```
**第一阶段：案例标准化**

自由文本案例  
↓  
案例标准化  
↓  
医疗背景  
家庭背景  
心理社会问题  
资源与限制因素  
服务需求  
↓  
五模块标准案例

|     |     |
| --- | --- |
| **模块** | **内容** |
| 医疗背景 | 诊断、治疗、病程 |
| 家庭背景 | 家庭结构与照顾情况 |
| 心理社会问题 | 情绪、行为与社会适应 |
| 资源与限制因素 | 支持系统与风险因素 |
| 服务需求 | 转介原因与目标 |

**第二阶段：专业决策**

五模块标准案例  
↓  
Step1 问题评估：基于 ICF 识别功能受限与影响因素。  
↓  
Step2 问题分析：基于 COM-B 分析行为形成机制。  
↓  
Step3 服务目标设定：制定服务目标。  
↓  
Step4 干预方案设计：匹配资源与服务策略。  
↓  
Step5 风险预判：识别服务过程中的潜在风险。  
↓  
Step6 成效评估：过程与结果评估。  
↓  
个案计划书

## 系统架构

为体现 MedSWFlow 从案例输入到专业决策输出的完整过程，系统采用五层架构设计：

```text
┌─────────────────────────┐
│       输出层             │
│ 个案计划书 / 服务方案     │
├─────────────────────────┤
│      工作流执行层         │
│ Step0 ~ Step6           │
├─────────────────────────┤
│      专业推理层           │
│ ICF + COM-B + BCW       │
├─────────────────────────┤
│      案例标准化层         │
│ 五模块案例构建            │
├─────────────────────────┤
│      数据输入层           │
│ 病历 / 访谈 / 转介记录    │
└─────────────────────────┘
```

各层功能说明：

1\. 数据输入层（Input Layer）

负责接收病历记录、访谈记录、转介单、社工接案记录等非结构化案例资料。

2\. 案例标准化层（Case Standardization Layer）

通过 Step0 工作流将原始案例转换为五模块标准案例，包括医疗背景、家庭背景、心理社会问题、资源与限制因素及服务需求。

3\. 专业推理层（Reasoning Layer）

整合 ICF、COM-B、BCW 等理论框架，为后续问题评估、问题分析与干预设计提供理论支撑。

4\. 工作流执行层（Workflow Layer）

执行 Step1 至 Step6 六步骤专业工作流，包括问题评估、问题分析、目标设定、干预设计、风险预判及成效评估。

5\. 输出层（Output Layer）

生成结构化个案计划书、服务方案及过程性记录，实现专业决策结果输出。

## 项目结构
```text
MedSWFlow/
│
├── data/                      # 案例与提示词数据
│   ├── cases.json             # 标准案例库
│   ├── prompts.json           # 六步骤工作流提示词
│   ├── prompts0.json          # Step0 案例标准化提示词
│   └── prompts2.json          # 实验版本提示词
│
├── src/                       # 核心源码
│   ├── run_pipeline.py        # 主工作流入口
│   ├── GPT.py                 # 模型调用封装
│   ├── GPT2.py                # 模型调用封装（实验版）
│   ├── demo.py                # 标准演示脚本
│   ├── demo0.py               # Step0案例标准化测试
│   └── demo2.py               # 工作流实验脚本
│
├── output/                    # 输出结果
│   ├── step0_result.md
│   ├── step1_result.md
│   ├── ...
│   └── step6_result.md
│
├── docs/                      # 开发文档与设计文档
│
├── tests/                     # 测试代码
│
├── .env                       # 模型配置
├── pyproject.toml             # 项目配置
├── uv.lock                    # 依赖锁文件
└── README.md
```


**核心文件说明**

|     |     |
| --- | --- |
| **文件** | **作用** |
| cases.json | 标准案例库 |
| prompts.json | 六步骤提示词模板 |
| run_pipeline.py | 工作流主入口 |
| demo.py | 演示运行脚本 |
| output | 结果输出目录 |
| .env | 模型配置 |
| tests | 测试代码 |

## 安装方法

快速安装：

双击打开名为MedSWFlow_Setup的安装包

点击下一步

点击浏览按钮自行选择合适的安装目录

点击安装

安装完毕后打开前一步选择的安装目录

找到名为MedSWFlow的文件夹双击打开

双击名为MedSWFlow的程序即可开始使用

使用方法：

打开名为MedSWFlow的程序

输入API密钥

输入模型地址URL（默认使用DeepSeek）

点击确认进入案例录入模式选择界面

根据文字提示自行选择合适的录入模式

案例输入完毕后点击生成标准案例按钮

等待标准案例生成

标准案例生成完毕后根据生成内容自行选择是否补充案例内容

如需补充可将信息填写至补充信息下方的文本框中

案例内容补充完毕后点击确认补充→完善案例按钮

可多次重复此过程以补充细节

确认不再补充内容后点击生成计划书按钮

等待个案计划书生成

生成完毕后点击右上角导出word按钮可将计划书导出为word文档

如需输入新案例可点击程序界面上方新案例按钮

使用过程中如需更改模型配置可点击程序界面上方设置按钮

## 核心理论基础

核心理论：

**1、人在情境中（Person-in-Environment, PIE）与人‑环境交互模型**

强调个体问题是人与环境动态互动的结果，既可能源于自身能力不足，也可能源于环境支持缺失或系统性障碍。该模型为本框架的五模块案例标准化提供了分析范式。

**2、生物‑心理‑社会模型（Biopsychosocial Model）**

突破纯生物医学模式，将生理、心理、社会因素视为同等重要的健康转归维度。与PIE模型共同支撑案例的五模块输入设计。

**3、ICF框架（International Classification of Functioning, Disability and Health）**

用于第一步“问题评估”，从身体功能、活动与参与、环境因素、个人因素四个维度系统梳理服务对象功能状态，确保评估全面客观。

**4、COM‑B模型与行为改变轮（Behaviour Change Wheel, BCW）**

用于第二步“问题分析”。从能力、机会、动机三层面剖析问题形成机制，并借助行为改变轮的九类干预功能筛选优先干预方向，同时纳入家庭照护能力、资源可及性等医务社工专属维度。

**5、康复目标制定原则（Goal Setting Principles in Rehabilitation）**

用于第三步“服务目标设定”。要求目标包含目标活动、所需支持、达成标准与时间界限四个要素，并按近期‑中期‑长期分层排序，确保目标可衡量、可执行。

**6、实施规范框架（TIDieR / Implementation Framework）**

用于第四步“干预方案设计”。明确每个干预模块的行动方案、执行主体、目标指标、实施背景、干预强度及监测流程，保证方案的可复现性与落地性。

**7、前瞻性风险预判框架（Proctor 实施结果分类学 + 健康干预非预期后果评估框架）**

用于第五步“干预风险预判”。系统评估干预非预期后果、伦理困境、角色模糊、服务负担、家庭适应性不佳及实施失败等六类核心风险，输出风险预警清单。

**8、双维度效果评估体系（ICF + Proctor 实施成果框架）**

用于第六步“成效评估设计”。基于ICF设计结果评估指标（功能状态、家庭支持等），基于Proctor框架设计过程评估指标（接受度、完成率、一致性等），实现对干预效果与实施质量的全面评价。

参考文献：

Engel, G. L. (1977). The need for a new medical model: A challenge for biomedicine. _Science_, 196(4286), 129–136.

Karls, J. M., & Wandrei, K. E. (1992). PIE: A new language for social work. _Social Work_, 37(1), 80–85.

World Health Organization. (2001). _International classification of functioning, disability and health: ICF_.

Michie, S., van Stralen, M. M., & West, R. (2011). The behaviour change wheel: A new method for characterising and designing behaviour change interventions. _Implementation Science_, 6, Article 42.

Bovend’Eerdt, T. J. H., Botell, R. E., & Wade, D. T. (2009). Writing SMART rehabilitation goals and achieving goal attainment scaling: A practical guide. _Clinical Rehabilitation_, 23(4), 352–361.

Hoffmann, T. C., et al. (2014). Better reporting of interventions: Template for intervention description and replication (TIDieR) checklist and guide. _BMJ_, 348, Article g1687.

Proctor, E., Silmere, H., Raghavan, R., et al. (2011). Outcomes for implementation research: Conceptual distinctions, measurement challenges, and research agenda. _Administration and Policy in Mental Health_, 38(2), 65–76.

Stratil, J. M., Biallas, R. L., Movsisyan, A., Oliver, K., & Rehfuess, E. A. (2024). Development of an overarching framework for anticipating and assessing adverse and other unintended consequences of public health interventions. _BMJ Public Health_, 2(1), Article e000209.

## 关于我们

创作者：毛誉霖、李世裕、宋淑平、张玉玲

作者单位：华东理工大学社会与公共管理学院

指导老师：张晨峰、宋雅君
