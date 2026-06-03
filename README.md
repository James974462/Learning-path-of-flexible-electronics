# 柔性电子 / 柔性传感器方向学习路线与技术栈

> 面向新入门柔性电子方向硕士研究生  
> 建议使用方式：作为课题组新人培训、GitHub README、个人学习计划或组会考核清单。  
> 更新时间：2026-06-04  
>
> 核心目标：在 1 年内形成完整研究闭环：  
> **提出传感需求 → 结构设计 → 力学/多物理场仿真 → 器件制备 → 读出电路 → 嵌入式采集 → 数据建模/神经网络解耦 → 应用验证 → 论文表达。**

---

## 目录

1. [领域总览：柔性电子到底学什么](#1-领域总览柔性电子到底学什么)  
2. [第一阶段：柔性传感基础知识](#2-第一阶段柔性传感基础知识)  
3. [第二阶段：结构设计与力学仿真](#3-第二阶段结构设计与力学仿真)  
4. [第三阶段：多物理场耦合](#4-第三阶段多物理场耦合)  
5. [第四阶段：柔性电子工艺与微纳加工](#5-第四阶段柔性电子工艺与微纳加工)  
6. [第五阶段：嵌入式硬件与软件](#6-第五阶段嵌入式硬件与软件)  
7. [第六阶段：神经网络与数据算法](#7-第六阶段神经网络与数据算法)  
8. [科研工具软件技术栈](#8-科研工具软件技术栈)  
9. [B站、GitHub 与官方教程清单](#9-b站github-与官方教程清单)  
10. [一年训练路线](#10-一年训练路线)  
11. [推荐入门课题模板](#11-推荐入门课题模板)  
12. [学生需要形成的最终能力](#12-学生需要形成的最终能力)  
13. [附录](#附录)

---

## 使用说明

这份路线不是要求新生在一年内精通所有软件和工艺，而是帮助学生建立**研究闭环意识**。柔性电子的入门难点在于，它不像纯算法或纯材料方向那样边界清晰。一个看似简单的柔性压力传感器，背后同时涉及材料、结构、工艺、电路、采样、算法、封装和应用验证。

建议采用下面的学习策略：

| 学习原则 | 具体做法 |
|---|---|
| 先闭环，再深入 | 先做出一个能采集数据的最小系统，再逐步提高性能 |
| 先 baseline，再 neural network | 不要一开始就上复杂深度学习，先用线性回归、随机森林等建立基准 |
| 先可重复，再高性能 | 如果实验不能重复，灵敏度再高也没有说服力 |
| 先结构机理，再应用展示 | 应用 demo 必须服务于机理和性能论证，而不是单纯“好看” |
| 先规范记录，再追求结果 | 每次实验都要记录样品编号、材料批次、测试条件、加载程序和数据路径 |

---

## 1. 领域总览：柔性电子到底学什么

柔性电子 / 柔性传感器不是一个单一学科，而是一个典型的交叉研究方向：

> **材料 + 结构力学 + 微纳制造 + 电子电路 + 嵌入式系统 + 数据算法 + 应用场景**

一个好的柔性传感器研究，不应只停留在“材料电阻变化明显”或“神经网络准确率很高”，而应该回答完整系统问题：

1. 传感需求是什么？
2. 外界物理量如何传递到敏感层？
3. 器件结构如何放大有效信号、抑制串扰？
4. 制备工艺是否稳定、可重复？
5. 信号如何稳定读出？
6. 算法如何校准、解耦和泛化？
7. 应用场景是否真正需要柔性传感器？

### 1.1 常见研究方向

| 方向 | 典型对象 | 重点能力 | 适合新生切入吗 |
|---|---|---|---|
| 柔性应变传感 | 关节运动、皮肤拉伸、软机器人形变 | Gauge factor、拉伸范围、疲劳、漂移 | 适合，入门门槛较低 |
| 柔性压力/触觉传感 | 电子皮肤、机器人手指、足底压力 | 灵敏度、检测限、响应时间、空间分辨率 | 很适合，容易形成闭环 |
| 多维力/力矩传感 | 三轴力、六轴力、剪切力、接触力 | 解耦、标定、结构对称性、神经网络 | 适合进阶，论文空间较大 |
| 生理信号传感 | ECG、EMG、EEG、汗液、温度 | 皮肤界面、低噪声电路、生物兼容性 | 需要医学/伦理/低噪声基础 |
| 柔性混合电子系统 | FPC、柔性互连、贴片芯片、无线模块 | 封装、低功耗、系统集成、可靠性 | 适合工程能力强的学生 |
| 软机器人传感 | 气动手、软体执行器、触觉皮肤 | 大变形、嵌入式布线、实时反馈 | 适合有机器人基础的学生 |
| 生物力学/牙科/医疗力学传感 | 口腔、牙齿、关节、康复器械 | 多轴力、复杂几何、有限元映射 | 适合结合课题组特色深入 |

### 1.2 对新生的基本要求

硕士生在入门阶段不必每个方向都深入，但至少要建立以下判断：

- 不同传感机制各有什么优劣；
- 哪些性能指标是真的重要，哪些只是论文包装；
- 器件结构如何影响灵敏度、线性范围、滞后和串扰；
- 柔性传感器为什么经常需要算法补偿；
- 工艺、封装、电路和算法为什么同样重要；
- 论文中“高灵敏度”“宽量程”“低检测限”是否在同一测试条件下比较；
- 数据集划分是否存在样品泄漏、时间泄漏或同一循环重复出现在训练集和测试集的问题。

### 1.3 柔性传感器研究的完整闭环

建议学生把每个课题都拆成下面 8 个层级：

| 层级 | 关键问题 | 常见输出 |
|---|---|---|
| 需求层 | 要测什么？力、压力、应变、温度、生理信号还是多轴力？ | 应用场景定义、目标指标 |
| 结构层 | 力如何传递到敏感区域？是否有应变集中或解耦设计？ | CAD、结构示意图、FEM |
| 材料层 | 敏感材料、基底、封装材料如何选择？ | 材料表征、配方、工艺参数 |
| 工艺层 | 能否稳定做出多个样品？ | 工艺流程、样品照片、良率 |
| 电路层 | 信号如何读出？噪声是否可控？ | 原理图、PCB、采集系统 |
| 数据层 | 数据是否同步、可复现、有标签？ | raw data、processed data、metadata |
| 算法层 | 是否需要非线性校准、解耦或漂移补偿？ | baseline、模型、误差分析 |
| 应用层 | 为什么这个器件适合该场景？ | demo、对照实验、论文图 |

---

## 2. 第一阶段：柔性传感基础知识

### 2.1 传感机制

常见柔性力学传感机制包括：

| 机制 | 基本原理 | 优点 | 局限 | 入门建议 |
|---|---|---|---|---|
| 压阻式 | 形变导致导电网络、电阻或接触电阻变化 | 读出简单、成本低、容易阵列化 | 易受滞后、漂移、温度影响 | 最适合新生第一代器件 |
| 电容式 | 形变导致电极距离、面积或介电常数变化 | 功耗低、稳定性较好 | 对寄生电容、屏蔽和布线敏感 | 适合有电路基础后学习 |
| 压电式 | 动态应变产生电荷 | 适合动态力和振动 | 不适合静态力长期保持 | 适合动态监测、步态、振动 |
| 摩擦电式 | 接触分离产生电荷转移和静电感应 | 可自供能、信号幅值高 | 受湿度、频率、接触状态影响 | 注意测试标准化 |
| 光学式 | 形变改变光路、光强或反射图像 | 抗电磁干扰、空间信息丰富 | 系统复杂、封装难度较高 | 适合机器人触觉方向 |
| 磁感式 | 柔性结构形变改变磁场分布 | 适合三维触觉和软体机器人 | 需要磁体与磁传感芯片 | 适合多轴力/剪切力 |
| 离子导体式 | 离子迁移、界面电容或电化学阻抗变化 | 适合皮肤界面和水凝胶器件 | 稳定性、干燥、封装是难点 | 适合生物/可穿戴方向 |

### 2.2 必须掌握的性能指标

| 指标 | 含义 | 推荐表达方式 | 常见错误 |
|---|---|---|---|
| Sensitivity | 输出变化量对输入变化量的斜率 | `S = ΔSignal / ΔPressure` 或 `S = δ(ΔR/R0)/δP` | 不说明压力区间 |
| Gauge factor | 应变传感中相对电阻变化对应变的比值 | `GF = (ΔR/R0) / ε` | 脱离应变范围比较 |
| Linear range | 近似线性的有效测量范围 | 给出拟合区间和 R² | 只给曲线不说明范围 |
| Limit of detection | 最小可检测输入 | 通常结合噪声水平和 3σ | 用肉眼可见代替定量检测限 |
| Response/recovery time | 响应/恢复速度 | 说明采样率、滤波和判定标准 | 采样率太低却声称毫秒响应 |
| Hysteresis | 加载/卸载曲线差异 | 给出最大滞后误差或面积差 | 只展示加载曲线 |
| Repeatability | 重复加载下输出一致性 | 多循环曲线 + 误差条 | 只测一次 |
| Drift | 长时间保持载荷时输出漂移 | 恒定载荷保持 10 min、30 min 或更长 | 把短时稳定当长期稳定 |
| Creep | 恒定应力下材料继续变形 | 与粘弹性模型结合解释 | 忽略软材料时间效应 |
| Crosstalk | 多轴或多点信号相互干扰 | 串扰矩阵或误差百分比 | 多维传感不做串扰分析 |
| SNR | 信噪比 | 给出噪声 RMS、滤波前后对比 | 不区分器件噪声和电路噪声 |
| Durability | 循环耐久性 | 1000、5000、10000 次循环曲线 | 只说“稳定”不说明循环数 |
| Spatial resolution | 阵列分辨率 | taxel pitch、有效接触面积 | 只给像素数不说明间距 |

### 2.3 结构放大机制

柔性传感器性能提升常常来自结构，而不仅是材料。常见结构包括：

| 结构 | 作用 | 适合传感器 |
|---|---|---|
| 微圆顶 | 增强局部压缩和接触面积变化 | 压阻、电容压力传感 |
| 微金字塔 | 低压区灵敏度高，接触逐步增加 | 高灵敏压力传感 |
| 多孔泡沫 | 大压缩变形、低密度、可穿戴 | 压力/应变传感 |
| 表面裂纹 | 小应变引起大电阻变化 | 高灵敏应变传感 |
| 蛇形互连 | 降低金属互连应变 | 可拉伸电极和互连 |
| kirigami 剪纸结构 | 通过几何展开实现大变形 | 大拉伸柔性器件 |
| island–bridge 结构 | 刚性器件岛 + 柔性互连桥 | 柔性混合电子系统 |
| 中性层设计 | 将脆弱层放在低应变位置 | 金属薄膜/芯片集成 |
| 梯度模量结构 | 缓解软硬界面应力集中 | 封装、皮肤贴附 |
| 多层封装结构 | 防水、防汗液、机械保护 | 可穿戴长期监测 |

学生需要理解：结构设计的本质不是“画得复杂”，而是控制**应力/应变分布、接触面积变化、导电通路变化和力传递路径**。

### 2.4 推荐入门阅读（使用Web of Science检索论文）

| 类型 | 推荐资源(关键词) | 用法 |
|---|---|---|
| 领域路线图 | Technology Roadmap for Flexible Sensors | 了解柔性传感器未来瓶颈和系统化挑战 |
| 柔性压力传感综述 | Flexible and Stretchable Pressure Sensors: From Basic Principles to Applications | 学机制、指标、材料和应用 |
| 柔性触觉系统综述 | Recent progress in flexible tactile sensor systems | 学触觉阵列、多维力和系统集成 |
| 可穿戴柔性传感综述 | Research on Flexible Sensors for Wearable Devices: A Review | 了解可穿戴应用场景 |
| 微结构压力传感综述 | Flexible pressure sensors with microstructures | 重点学习微结构如何提高灵敏度和线性区 |
| 软机器人触觉论文 | tactile sensing for soft robotics | 学系统集成和应用验证 |
| 柔性互连/封装论文 | stretchable interconnect / neutral mechanical plane | 学长期可靠性和工程实现 |

### 2.5 新生第一周应完成的小任务

1. 用 Excel 或 Notion 建一个文献表；
2. 选 10 篇柔性压力/应变传感论文；
3. 每篇论文提取：材料、结构、机制、指标、测试条件、应用、缺点；
4. 用一页 PPT 讲清楚“为什么这个器件有效”；
5. 写出 5 个自己看不懂的概念，下周逐个解决。

---

## 3. 第二阶段：结构设计与力学仿真

### 3.1 结构设计要回答的问题

一个柔性传感结构必须回答：

1. 外力从哪里输入？
2. 应力和应变集中在哪里？
3. 敏感层应该放在哪里？
4. 柔性封装是否改变了力传递？
5. 多轴力之间是否会发生串扰？
6. 弯曲、拉伸、压缩和剪切耦合时，信号是否可解耦？
7. 器件贴到曲面后，标定是否仍然有效？
8. 循环加载后结构是否疲劳或失效？

### 3.2 力学基础模块

| 模块 | 需要掌握 | 最小学习目标 |
|---|---|---|
| 连续介质力学 | 应力、应变、本构关系、边界条件 | 能解释 von Mises stress、principal strain、contact pressure |
| 材料模型 | 线弹性、超弹性、粘弹性、塑性、各向异性 | 能给 PDMS/Ecoflex 设置合理材料参数 |
| 大变形 | PDMS、Ecoflex、TPU、硅胶等软材料 | 知道几何非线性和材料非线性区别 |
| 接触力学 | 压头-传感器、皮肤-器件、机器人手指-物体 | 能设置接触、摩擦和加载位移 |
| 层合结构 | PI/金属/PDMS、多层封装、中性层 | 能判断金属薄膜是否处于高应变区域 |
| 可靠性 | 循环加载、裂纹、界面脱粘、疲劳 | 能从最大主应变判断潜在失效位置 |
| 多轴解耦 | 正压力、剪切力、弯矩之间的响应矩阵 | 能建立输入-输出矩阵或神经网络映射 |

### 3.3 推荐软件路线

| 软件 | 适合做什么 | 新生建议 | 典型练习 |
|---|---|---|---|
| Abaqus | 大变形、接触、超弹性、非线性力学 | 柔性力学结构首选之一 | PDMS 压缩、微结构接触、蛇形互连拉伸 |
| COMSOL | 力-电、热-力、电磁-热-结构等多物理场耦合 | 适合解释传感机理 | 电容压力传感、压阻耦合、热-力耦合 |
| MATLAB | 后处理、信号处理、拟合、优化 | 适合传感数据分析 | 参数拟合、滤波、响应曲线 |
| Python | 参数扫描、批处理、数据可视化、机器学习 | 必学 | 自动画图、批量处理 CSV、训练模型 |

### 3.4 建议练习项目

| 练习 | 目标 | 验收标准 |
|---|---|---|
| PDMS 方块受压仿真 | 学会超弹性材料、接触和网格敏感性 | 能输出力-位移曲线，并说明网格收敛 |
| 微圆顶压力传感结构 | 理解微结构应变集中与灵敏度关系 | 能比较平面与微圆顶的接触压力分布 |
| 微金字塔压力传感结构 | 比较不同高度、间距、模量对响应的影响 | 能做 3 个以上参数扫描 |
| PI/金属蛇形互连拉伸 | 理解中性层、最大主应变、疲劳风险 | 能判断金属层最大应变位置 |
| 三轴力传感器结构 | 建立响应矩阵，分析串扰 | 能输出不同方向加载下的通道响应 |
| 曲面贴附传感器 | 分析预应变、曲率和封装对标定的影响 | 能说明平面标定和曲面应用的差异 |

### 3.5 仿真图建议

论文或组会中，建议至少输出以下图：

1. 几何模型和边界条件图；
2. 网格图；
3. 位移云图；
4. 最大主应变云图；
5. 接触压力云图；
6. 敏感层局部放大图；
7. 力-位移曲线；
8. 参数扫描结果；
9. 仿真与实验趋势对比图。

### 3.6 常见仿真错误

| 错误 | 后果 | 建议 |
|---|---|---|
| 只给云图，不给边界条件 | 结果不可判断 | 每张仿真图必须说明加载和约束 |
| 网格过粗 | 应变集中区域不可信 | 对关键区域局部加密 |
| 材料参数随便填 | 结果只有“示意意义” | 尽量用实验或文献参数 |
| 不做接触收敛检查 | 接触压力可能异常 | 检查接触算法、摩擦系数和时间步 |
| 把仿真当作定量预测 | 容易过度解释 | 入门阶段优先强调趋势和机理 |
| 忽略封装层 | 实验和仿真差异大 | 把封装层纳入模型 |

---

## 4. 第三阶段：多物理场耦合

柔性传感器不能只描述“压力变大，电阻变小”。更完整的逻辑是：

> 外力 / 形变 → 应力应变分布 → 微结构接触变化 → 导电通路 / 电容 / 电荷 / 磁场变化 → 电路读出 → 数字信号 → 算法输出

### 4.1 常见多物理场链条

| 传感类型 | 多物理场链条 | 可建模输出 |
|---|---|---|
| 压阻式 | 力学变形 + 接触电阻 + 隧穿效应 / 渗流网络 | ΔR/R0、GF、压力-电阻曲线 |
| 电容式 | 力学压缩 + 介电层厚度变化 + 边缘电场 / 寄生电容 | ΔC/C0、电场分布、寄生误差 |
| 压电式 | 应变场 + 极化电荷 + 动态电荷放大 | 电荷、电压、频率响应 |
| 摩擦电式 | 接触分离 + 表面电荷 + 静电感应 | 开路电压、短路电流 |
| 温度/热流 | 热传导 + 热阻 + 电阻温度系数 | 温度场、响应时间、热漂移 |
| 生理电极 | 皮肤界面 + 电化学阻抗 + 运动伪迹 | 阻抗谱、噪声、接触稳定性 |
| 磁触觉 | 柔性结构形变 + 磁场变化 + Hall sensor 读出 | Bx/By/Bz、三维力映射 |
| 光学触觉 | 柔性层形变 + 图像变化 + 视觉算法 | 位移场、接触形状、力分布 |

### 4.2 推荐掌握的模型

#### 4.2.1 压阻模型

入门必须理解：

```text
Relative resistance change: ΔR/R0 = (R - R0) / R0
Gauge factor: GF = (ΔR/R0) / ε
```

进阶需要理解：

- 渗流网络；
- 隧穿效应；
- 接触电阻；
- 裂纹开合；
- 导电填料取向；
- 温度对电阻的影响。

#### 4.2.2 电容模型

入门必须理解：

```text
C = εr ε0 A / d
```

但柔性电容传感器中，真实问题通常比平行板模型复杂，因为：

- 微结构导致等效面积变化；
- 介电层压缩不是均匀的；
- 电极边缘有 fringing field；
- 长导线和阵列扫描会带来寄生电容；
- 皮肤、手指、水汽和封装也可能改变等效电场。

#### 4.2.3 动态系统模型

软材料有明显时间效应，因此要关注：

- response time；
- recovery time；
- creep；
- relaxation；
- drift；
- frequency response；
- loading rate dependence。

建议学生至少做一次**阶跃加载实验**和一次**正弦加载实验**，观察传感器是否存在明显相位滞后。

### 4.3 多物理场学习路线

| 阶段 | 学习目标 | 推荐练习 |
|---|---|---|
| 初级 | 理解“力学场如何影响电信号” | 压阻式单点传感器：力-位移-电阻曲线 |
| 中级 | 能把力学仿真结果和电学模型联系起来 | 用接触面积或应变均值预测 ΔR/R0 |
| 进阶 | 建立力-电耦合或热-力耦合模型 | COMSOL 中建立电容式压力传感器模型 |
| 高级 | 结合数据驱动模型 | 用仿真数据辅助神经网络训练或数据增强 |

---

## 5. 第四阶段：柔性电子工艺与微纳加工

### 5.1 工艺分层

| 层级 | 工艺 | 适合程度 | 典型用途 |
|---|---|---|---|
| 入门可做 | PDMS/Ecoflex 倒模、砂纸模板、激光切割、喷涂、丝网印刷、导电胶、FPC 打样 | 最适合快速做第一代器件 | 快速验证结构与读出 |
| 中级 | 旋涂、软光刻、转印、等离子处理、磁控溅射、蒸镀、湿法刻蚀 | 需要实验室条件 | 微结构和薄膜器件 |
| 高级 | 光刻、电子束曝光、DRIE、RIE、LIGA、纳米压印、飞秒激光直写 | 需要平台训练 | 微纳结构、高精度图形 |
| 系统集成 | FPC、ACF bonding、wire bonding、封装、低模量胶粘接 | 很关键，容易被忽略 | 可靠连接和实际应用 |

### 5.2 常见材料

| 类别 | 材料 | 主要优势 | 常见问题 |
|---|---|---|---|
| 柔性基底 | PDMS、Ecoflex、PI、PET、TPU、PU、水凝胶、织物 | 柔软、可拉伸、易贴附 | 表面能低、粘接难、吸附污染 |
| 导电材料 | Au、Pt、Ag、Cu、CNT、graphene、MXene、PEDOT:PSS、液态金属 | 导电、可图形化 | 氧化、裂纹、迁移、界面失效 |
| 介电材料 | PDMS、Ecoflex、PVDF、PI、离子凝胶 | 可用于电容/压电器件 | 介电损耗、吸水、稳定性 |
| 粘接/封装 | Silbione、PDMS、Parylene、PU film、medical adhesive | 保护器件、提高可穿戴性 | 封装改变力传递 |
| 微结构模板 | 砂纸、硅模具、SU-8、3D 打印模具、激光加工模板 | 可构建微结构 | 模板重复性和脱模问题 |

### 5.3 常见工艺路线

#### 路线 A：低成本快速原型

适合新生快速入门。

1. 设计电极结构；
2. FPC 或铜箔激光切割；
3. 加入 Velostat、导电泡棉、碳黑/PDMS、CNT/PDMS 等敏感层；
4. 用 PDMS/Ecoflex 封装；
5. 用 Arduino/STM32 读取电阻信号；
6. 做基础标定。

优点：快、便宜、容易形成闭环。  
缺点：精度、重复性和长期稳定性有限。  
适合论文前期：可用于验证结构思路、读出电路和算法流程。

#### 路线 B：软光刻微结构

适合压力传感、触觉阵列。

1. 制备 SU-8 或硅微结构模板；
2. PDMS 旋涂或倒模；
3. 固化后剥离；
4. 转印导电层或组装电极；
5. 封装测试。

优点：微结构可控，论文表达清楚。  
缺点：需要光刻平台和模板制备经验。  
关键参数：SU-8 厚度、曝光剂量、显影时间、PDMS 配比、脱模剂、固化温度。

#### 路线 C：金属薄膜柔性器件

适合应变传感、柔性互连和高稳定器件。

1. PI/PET/PDMS 基底处理；
2. 溅射或蒸镀金属；
3. 光刻图形化；
4. 湿法刻蚀或 lift-off；
5. 转印或封装；
6. 电学和力学测试。

优点：图形精细，重复性较好。  
缺点：工艺门槛较高，界面可靠性需要重点处理。  
关键问题：金属与柔性基底之间的附着力、裂纹扩展、弯折疲劳。

#### 路线 D：激光加工

适合快速图形化和碳化导电结构。

1. 设计图案；
2. 激光切割 PI、PET、PDMS 或金属箔；
3. 或激光诱导石墨烯 / 碳化结构；
4. 组装成传感器；
5. 测试机械和电学性能。

优点：无需掩膜，速度快。  
缺点：边缘热影响、重复性和分辨率需要控制。  
关键参数：功率、扫描速度、频率、线间距、焦距、气氛。

### 5.4 新生必须学会的工艺记录方式

每个样品必须有独立编号，例如：

```text
PS-2026-001
PS-2026-002
```

建议记录字段：

| 字段 | 示例 |
|---|---|
| 样品编号 | PS-2026-001 |
| 基底材料 | PDMS, 10:1 |
| 敏感材料 | CNT/PDMS, 3 wt% |
| 电极材料 | FPC Cu electrode |
| 微结构 | sandpaper template, P800 |
| 封装 | Ecoflex 00-30 |
| 固化条件 | 80°C, 2 h |
| 测试日期 | 2026-06-04 |
| 测试设备 | motorized stage + force gauge |
| 数据路径 | data/raw/PS-2026-001/ |

没有样品记录，后续所有数据都很难追溯。

---

## 6. 第五阶段：嵌入式硬件与软件

柔性传感器真正能不能用，很大程度取决于读出系统。学生不能只依赖万用表或台式设备。

### 6.1 硬件基础

| 模块 | 必学内容 | 最小实战任务 |
|---|---|---|
| 基础电路 | 分压、电桥、滤波、运放、仪表放大器 | 用分压电路读取一个电阻式传感器 |
| 传感读出 | 电阻读出、电容读出、电荷放大、电压/电流采样 | 比较分压、电桥和恒流源读出差异 |
| ADC | 分辨率、采样率、噪声、参考电压、有效位数 ENOB | 计算 12-bit ADC 的理论分辨率 |
| 多通道采集 | MUX、扫描频率、串扰、同步采样 | 读取 8 个以上通道 |
| PCB/FPC | 原理图、布局、地线、屏蔽、柔性排线、连接器 | 用 KiCad 画一块采集板 |
| 通信 | UART、I2C、SPI、USB、BLE、Wi-Fi | 串口实时发送数据到 Python |
| 电源 | LDO、DC-DC、电池、充电管理、低功耗 | 设计 USB 供电和电池供电方案 |
| 封装 | 焊盘、引线应力释放、防水、防汗液、机械保护 | 做一次弯折后的连接可靠性测试 |

### 6.2 软件基础

| 层级 | 内容 | 最小实战任务 |
|---|---|---|
| MCU 编程 | GPIO、ADC、Timer、DMA、I2C、SPI、UART | 固定采样率读取 ADC 并串口输出 |
| 上位机 | Python 串口读取、实时绘图、数据保存 | 实时画出 4 通道传感曲线 |
| 数据格式 | CSV、JSON、HDF5、时间戳同步 | 每条数据包含 timestamp 和 channel values |
| 实时系统 | 采样频率控制、缓存、丢包检测 | 记录采样间隔并统计 jitter |
| 无线传输 | BLE GATT、ESP32 Wi-Fi、MQTT | ESP32 无线发送传感器数据 |
| TinyML | 模型压缩、量化、MCU 推理 | 部署一个小型 MLP 分类或回归模型 |

### 6.3 推荐硬件平台

| 平台 | 适合用途 | 推荐学习顺序 |
|---|---|---|
| Arduino UNO/Nano | 零基础入门、单通道传感器读取 | 第 1 个 demo |
| ESP32 | Wi-Fi/BLE、无线采集、低成本原型 | 第 2 个 demo |
| STM32 | 多通道高速采样、较正式的科研系统 | 正式系统 |
| Raspberry Pi | 上位机、图像处理、复杂数据存储 | 视觉触觉/机器人方向 |
| Teensy | 高速采样、音频/触觉信号处理 | 进阶 |
| NI DAQ | 高精度实验室标定系统 | 论文标定平台 |
| 自制 PCB/FPC | 论文级系统集成 | 课题后期 |

### 6.4 采集系统的基本架构

```text
Flexible sensor
      ↓
Analog front-end
      ↓
ADC / MCU
      ↓
Serial / USB / BLE / Wi-Fi
      ↓
Python upper computer
      ↓
Raw data storage
      ↓
Filtering / calibration / model inference
      ↓
Visualization / application demo
```

### 6.5 最小上位机功能

建议每个学生至少写出一个 Python 上位机，包含：

1. 串口选择；
2. 采样频率显示；
3. 实时曲线；
4. 开始/停止采集；
5. CSV 保存；
6. 实验备注输入；
7. 自动生成数据文件夹；
8. 简单滤波和基线归零。

---

## 7. 第六阶段：神经网络与数据算法

柔性传感器的数据问题通常不是简单分类，而是：

1. 多通道信号解耦；
2. 非线性标定；
3. 滞后补偿；
4. 漂移补偿；
5. 个体差异 / 器件差异迁移；
6. 曲面贴附后的重新标定；
7. 低数据量下的泛化；
8. 嵌入式端实时推理。

### 7.1 算法路线

| 阶段 | 模型 | 用途 | 注意事项 |
|---|---|---|---|
| 入门 | 线性回归、Ridge、Lasso | 建立最基本标定曲线 | 必须作为 baseline |
| 入门 | Random Forest、XGBoost、SVR | 处理非线性但数据量不大 | 注意交叉验证方式 |
| 中级 | MLP | 多通道静态力/压力解耦 | 适合表格数据 |
| 中级 | 1D-CNN | 多通道时序信号 | 适合窗口数据 |
| 中级 | LSTM/GRU | 滞后、动态响应、时序依赖 | 需要足够时序数据 |
| 高级 | Transformer | 长时序、多模态 | 数据量不足时容易过拟合 |
| 高级 | Gaussian Process | 低样本、不确定性估计 | 适合小数据但计算量较大 |
| 高级 | Physics-informed NN | 结合物理约束 | 需要明确物理模型 |
| 嵌入式 | TinyML、量化 MLP/CNN | MCU 端实时识别/回归 | 注意 RAM、Flash、推理延迟 |
| 可靠性 | Domain adaptation、Transfer learning | 不同器件、不同曲率、不同用户迁移 | 要设计独立测试集 |

### 7.2 推荐数据处理流程

1. 原始信号读取；
2. 时间戳同步；
3. 去除异常点；
4. 滤波；
5. 基线校正；
6. 分段；
7. 特征提取；
8. 训练/验证/测试集划分；
9. baseline 模型；
10. 神经网络模型；
11. 误差分析；
12. 泛化测试；
13. 嵌入式部署。

### 7.3 常见评价指标

| 任务 | 推荐指标 |
|---|---|
| 回归 | MAE、RMSE、R²、Max error、Normalized error |
| 分类 | Accuracy、Precision、Recall、F1-score、Confusion matrix |
| 多轴力估计 | 各轴 MAE/RMSE、角度误差、串扰矩阵 |
| 时序预测 | Delay、动态响应误差、频域误差 |
| 嵌入式部署 | 推理时间、模型大小、功耗、RAM/Flash 占用 |

### 7.4 传感器算法最容易犯的错误

| 错误 | 为什么严重 | 正确做法 |
|---|---|---|
| 只报告神经网络准确率 | 无法证明算法真的优于简单方法 | 必须和线性回归、Random Forest 等 baseline 比较 |
| 随机打乱所有数据点 | 同一次加载循环可能同时进入训练集和测试集 | 按样品、循环、日期或受试者划分数据 |
| 没有独立样品测试 | 模型只记住某个样品特性 | 至少留出一个样品做外部测试 |
| 不记录加载条件 | 无法判断模型泛化范围 | 记录力、速度、角度、曲率、温度 |
| 只给平均误差 | 掩盖极端误差 | 给误差分布、最大误差和失败案例 |
| 过度依赖深度学习 | 小数据下容易过拟合 | 小数据先用传统机器学习和物理解释 |

### 7.5 推荐算法项目

| 项目 | 输入 | 输出 | 目标 |
|---|---|---|---|
| 单点压力标定 | 电压/电阻 | 压力 | 比较线性拟合和随机森林 |
| 4×4 阵列接触位置识别 | 16 通道信号 | x-y 位置 | 做热图和位置误差 |
| 三轴力解耦 | 多通道信号 | Fx, Fy, Fz | 建立串扰矩阵和 MLP |
| 动态手势识别 | 时序信号 | 手势类别 | 1D-CNN 或 LSTM |
| 曲面贴附补偿 | 信号 + 曲率 | 校正后的压力/力 | 做 domain adaptation |
| MCU 端推理 | 传感器实时数据 | 分类/回归结果 | TinyML 部署 |

---

## 8. 科研工具软件技术栈

### 8.1 数据分析与科研绘图

| 工具 | 用途 | 建议 | 学到什么程度 |
|---|---|---|---|
| Python | 数据处理、自动画图、机器学习 | 必学 | 能批量处理 CSV、自动出图、训练模型 |
| NumPy / Pandas | 数组、表格、数据清洗 | 必学 | 能做数据筛选、分组统计、缺失值处理 |
| OriginPro | 快速画实验图、拟合、统计 | 必学 | 能完成传感器性能曲线和拟合 |
| MATLAB | 信号处理、系统建模、滤波 | 建议掌握 | 能做滤波、FFT、系统辨识 |
| ImageJ / Fiji | 显微图、SEM 图、尺寸统计 | 建议掌握 | 能统计微结构尺寸和孔径分布 |
| Adobe Illustrator | 论文示意图、矢量图 | 必学 | 能整理论文 figure panel |

### 8.2 三维建模与渲染

| 工具 | 用途 | 建议 | 学到什么程度 |
|---|---|---|---|
| SolidWorks | 结构设计、模具设计、装配 | 必学 | 能画传感器结构、夹具、模具 |
| KeyShot | 快速工业渲染 | 必学 | 能做论文示意图和展示图 |
| Blender | 复杂渲染、动画、TOC 图 | 建议掌握 | 能做更高质量三维示意图 |
| Rhino | 曲面结构、可穿戴贴合形态 | 建议掌握 | 适合复杂曲面和可穿戴贴附 |
| AutoCAD | 掩膜版、二维图纸 | 必学 | 能画 mask、激光切割图、二维工程图 |

### 8.3 编程与版本管理

| 工具 | 用途 | 建议 | 学到什么程度 |
|---|---|---|---|
| Python | 数据、算法、自动化 | 必学 | 能写可复现分析脚本 |
| C/C++ | MCU、驱动、底层通信 | 必学 | 能写 ADC、串口、I2C/SPI 驱动 |
| MATLAB | 信号处理、建模 | 建议掌握 | 能做滤波、拟合和数据可视化 |
| Git/GitHub | 代码版本管理、论文复现、项目发布 | 必学 | 能 commit、branch、写 README |
| VS Code | 写代码、Markdown、Python、嵌入式 | 必学 | 作为主力编辑器 |
| Jupyter Notebook | 数据探索和可视化 | 必学 | 用于初步分析，不替代正式脚本 |
| LaTeX / Overleaf | 论文、公式、排版 | 建议掌握 | 至少能改模板和公式 |
| Markdown | README、实验记录、文档 | 必学 | 能维护项目文档 |

### 8.4 工具学习优先级

| 优先级 | 必须掌握 |
|---|---|
| P0：所有学生必须会 | Python、Origin、ImageJ、SolidWorks、Git/GitHub、Markdown |
| P1：根据课题必须会 | Abaqus/COMSOL、STM32/ESP32、KiCad、Adobe Illustrator |
| P2：进阶提升 | Blender、KeyShot、Rhino、TinyML、MkDocs/docsify |

---

## 9. B站、GitHub 与官方教程清单

> 注：B站课程和网页链接可能会更新或下架。建议按课程名或关键词检索，而不是只依赖固定链接。  
> 建议优先顺序：**官方文档负责准确性，B站负责快速上手，GitHub 项目负责复现和工程习惯。**

### 9.1 柔性电子与微纳加工

| 方向 | 推荐检索关键词 / 资源 | 学习目标 |
|---|---|---|
| 微纳加工总览 | “微纳加工 光刻 刻蚀 薄膜沉积” | 理解 cleanroom 基本流程 |
| 光刻 | “光刻工艺 匀胶 曝光 显影 SU-8” | 理解图形转移 |
| 电子束曝光 | “E-Beam Lithography 电子束曝光 微纳加工” | 了解纳米级图形加工 |
| 软光刻 | “Soft lithography PDMS microstructure” | 学会 PDMS 微结构复制 |
| 激光加工 | “激光直写 柔性电子 PI 激光诱导石墨烯” | 理解无掩膜快速图形化 |
| 微纳平台课程 | MIT Decoders: Introduction to Microfabrication | 系统了解清洗、沉积、刻蚀、转印 |
| 平台 SOP | 所在学校/学院微纳平台 SOP | 实际操作必须以本校 SOP 为准 |

### 9.2 仿真

| 方向 | 推荐资源 | 学习目标 |
|---|---|---|
| COMSOL 入门 | COMSOL 官方 Learning Center 案例库 | 学建模流程、网格、求解器、后处理 |
| COMSOL 中文教程 | B站搜索“COMSOL 多物理场仿真 技术应用 专题培训” | 快速熟悉界面 |
| Abaqus 入门 | B站搜索“Abaqus 非线性 接触 超弹性 PDMS” | 学会软材料接触仿真 |
| Abaqus 官方 | Dassault Systèmes SIMULIA Abaqus 文档 | 查材料模型和单元设置 |
| 多物理场耦合 | 搜索“COMSOL 低频电磁场 MEMS 机电耦合” | 学力-电/热-力耦合 |
| 后处理 | Python + ParaView / MATLAB | 批量提取曲线和云图数据 |

### 9.3 嵌入式与硬件

| 方向 | 推荐资源 | 学习目标 |
|---|---|---|
| 微机原理 | B站：微机原理相关教程 |了解嵌入式系统架构
| STM32 入门 | B站：江协科技 STM32 入门教程 | GPIO、ADC、串口、定时器 |
| ESP32 | Espressif ESP-IDF 官方 Get Started | Wi-Fi/BLE 数据采集 |
| 上位机设计| C#语言与VS设计上位机 |界面功能设计与上下位机通讯
| 可穿戴电子 | Adafruit Learning System / Wearables | 学可穿戴电路和导线连接 |
| PCB 设计 | KiCad 官方 Getting Started | 原理图、PCB、Gerber |
| KiCad 中文教程 | B站搜索“KiCad 画电路板 入门” | 快速完成第一块板 |

### 9.4 Python / 数据分析 / 机器学习

| 方向 | 推荐资源 | 学习目标 |
|---|---|---|
| Python 入门 | 菜鸟教程 Python 部分 | 语法、文件读写、基础数据结构 |
| Python 数据科学 | Python Data Science Handbook | NumPy、Pandas、Matplotlib、Scikit-learn |
| 机器学习 | 吴恩达机器学习 / scikit-learn User Guide | 回归、分类、交叉验证、评价指标 |
| 深度学习 | 跟李沐学 AI / 动手学深度学习 | MLP、CNN、RNN、训练流程 |
| PyTorch | PyTorch 官方 Tutorials | 数据集、模型、训练、保存 |
| TinyML | TensorFlow Lite Micro GitHub | MCU 端模型部署 |
| Jupyter | Jupyter 官方文档 | 数据探索和图表展示 |
| 科研绘图 | B站搜索 Origin 教程 / Matplotlib Tutorials | 论文级数据图 |

### 9.5 柔性触觉 / 机器人触觉开源项目

| 项目 | 用途 | 适合学习什么 |
|---|---|---|
| Awesome-Touch | 触觉传感、触觉学习、机器人触觉论文和代码合集 | 建立论文地图 |
| FEATS | 有限元生成标签，训练神经网络预测触觉力分布 | 仿真 + 神经网络 |
| TACTO | 视觉触觉仿真器 | 机器人触觉仿真 |
| FlexiTac | 开源低成本柔性压阻触觉平台 | FPC 触觉阵列、读出电路、软件接口 |
| Open-source Magnetic Tactile Sensor | 磁触觉传感器设计与标定 | 三维力和自动标定 |
| eFlesh | 3D 打印磁触觉传感方案 | 低成本可定制触觉 |

---

## 10. 一年训练路线

### 阶段 1：建立基础认知

目标：知道柔性传感器是什么、怎么评价、论文怎么读。

任务：

1. 精读 3 篇综述；
2. 整理 30 篇本方向论文表格；
3. 用 Arduino/STM32 读取一个商业 flex sensor 或 FSR；
4. 用 Python 画出力-电信号曲线；
5. 学会 sensitivity、hysteresis、repeatability 的计算；
6. 完成一次 15 分钟组会汇报。

输出：

- 一份 20 页左右的文献汇报；
- 一个简单传感器读出 demo；
- 一套 Python 数据处理脚本；
- 一个文献表格；
- 一页“本方向关键问题总结”。

验收标准：

- 能说清 3 种传感机制；
- 能解释 5 个性能指标；
- 能独立读懂一篇柔性传感论文的图 1–图 4；
- 能用 Python 画出标准传感曲线。

---

### 阶段 2：结构设计 + 仿真入门

目标：能提出一个结构设计，并用有限元解释为什么它有效。


任务：

1. 学 Abaqus 或 COMSOL；
2. 建立 PDMS/Ecoflex 压缩模型；
3. 比较平面、微圆顶、微金字塔、孔隙结构的应变分布；
4. 做参数扫描：高度、间距、厚度、模量、封装层厚度；
5. 输出灵敏度趋势预测；
6. 设计第一版传感器结构和测试夹具。

输出：

- 一个传感结构 CAD；
- 一套 FEM 图；
- 一份结构设计报告；
- 一份参数扫描表；
- 一个可加工的样品设计文件。

验收标准：

- 能说明边界条件；
- 能解释最大应变区域；
- 能说明结构为什么提高灵敏度或降低串扰；
- 能把仿真结果转化为下一步制备参数。

---

### 阶段 3：制备第一代器件

目标：做出可测试的柔性传感器，而不是只停留在仿真。


任务：

1. 选择一种低门槛路线：PDMS + 导电复合材料，或 FPC + Velostat，或激光切割 PI/Cu；
2. 做 3–5 个不同结构参数的样品；
3. 建立基本测试平台；
4. 测灵敏度、响应时间、滞后、循环稳定性；
5. 和仿真结果对照；
6. 建立样品编号和实验记录规范。

输出：

- 第一代柔性传感器；
- 完整性能测试图；
- 失败样品记录；
- 初版工艺流程图；
- 样品照片和显微图。

验收标准：

- 至少 3 个样品可以重复测试；
- 有加载/卸载曲线；
- 有循环测试；
- 有误差条或样品间差异；
- 能解释失败样品的原因。

---

### 阶段 4：读出电路与系统集成

目标：从“半导体分析仪/万用表测试”升级到“可复现数据采集系统”。


任务：

1. 设计分压 / 电桥 / 电容读出电路；
2. 用 KiCad 画 PCB；
3. STM32/ESP32 实现多通道采集；
4. Python 上位机实时显示；
5. 加入滤波、校准、温漂记录；
6. 做 FPC 或柔性排线连接；
7. 整理硬件 BOM 和电路说明。

输出：

- 一块 PCB；
- 一套嵌入式采集程序；
- 一套上位机程序；
- 一份电路噪声和采样率分析；
- 一份硬件连接图；
- 一份采集系统 README。

验收标准：

- 能稳定采集 4–16 通道；
- 每条数据有 timestamp；
- 能保存 raw data；
- 能实时显示曲线；
- 能说明采样率和噪声来源。

---

### 阶段 5：算法建模与标定

目标：能处理非线性、串扰、漂移和多通道解耦。


任务：

1. 建立标定平台；
2. 采集力 / 位移 / 角度 / 曲率与传感信号同步数据；
3. 先做线性回归、Random Forest、SVR；
4. 再做 MLP、1D-CNN 或 LSTM；
5. 比较模型误差、泛化性、不同样品迁移；
6. 做消融实验：是否需要某些通道、是否需要曲率输入、是否需要历史窗口；
7. 设计外部测试集。

输出：

- 一套训练数据集；
- 一套 baseline 模型；
- 一套神经网络解耦模型；
- 误差分析和可解释性图；
- 数据集说明文档；
- 模型训练脚本。

验收标准：

- 有 baseline；
- 有独立测试集；
- 有误差分布；
- 有失败案例分析；
- 神经网络不是唯一结果，而是与物理/结构解释相互支持。

---

### 阶段 6：应用验证与论文成型

目标：把器件变成一个有说服力的系统。


可选应用：

| 应用 | 验证重点 |
|---|---|
| 可穿戴关节监测 | 贴附稳定性、运动伪迹、长期佩戴 |
| 机器人触觉 | 正压力/剪切力解耦、抓取控制 |
| 医疗康复 | 生物兼容性、舒适性、重复使用 |
| 牙科/口腔/生物力学 | 小空间集成、多轴力、复杂几何映射 |
| 软机器人 | 大变形、嵌入式柔性互连、实时反馈 |

输出：

- 一个完整系统 demo；
- 一篇论文初稿；
- 一套可复现代码和数据；
- 一个 GitHub 仓库；
- 一份图表清单；
- 一份投稿目标期刊/会议分析。

验收标准：

- 应用验证与传感器优势直接相关；
- 不只是展示视频，而有定量评价；
- 论文主线清楚：问题—设计—机理—性能—系统—应用；
- 数据和代码可追溯。

---


## 11. 学生需要形成的最终能力

柔性电子最容易走偏的地方，是把它当成单纯的“材料论文”或“算法论文”。真正有发展潜力的柔性传感研究应该做到：

> **结构上可解释，工艺上可重复，电路上可稳定读出，算法上能泛化，应用上能证明不可替代。**

一个合格硕士毕业时，不一定要精通所有工具，但至少要能独立完成：

1. 设计一个柔性传感器；
2. 做出可测试样品；
3. 搭建采集系统；
4. 完成标定实验；
5. 处理和分析数据；
6. 用模型解释传感机理；
7. 用应用场景证明器件价值；
8. 用论文图和文字讲清楚完整逻辑。

### 12.1 新生一年后应达到的能力等级

| 能力 | 合格标准 | 优秀标准 |
|---|---|---|
| 文献阅读 | 能读懂综述和典型论文 | 能总结领域空白并提出新问题 |
| 结构设计 | 能画出可加工结构 | 能用 FEM 支撑设计逻辑 |
| 工艺制备 | 能重复做出样品 | 能控制良率和参数一致性 |
| 电路采集 | 能稳定采集数据 | 能设计 PCB/FPC 并分析噪声 |
| 数据分析 | 能画性能曲线 | 能建立规范数据管线 |
| 算法建模 | 能训练 baseline 模型 | 能做泛化测试和误差解释 |
| 论文表达 | 能描述实验结果 | 能形成完整故事线 |

---

# 附录

## 附录 A：建议学生建立的文件夹结构

```text
flexible-sensor-project/
├── README.md
├── docs/
│   ├── literature_review.md
│   ├── design_notes.md
│   └── experiment_log.md
├── cad/
│   ├── solidworks/
│   └── stl/
├── simulation/
│   ├── abaqus/
│   ├── comsol/
│   └── results/
├── fabrication/
│   ├── process_flow.md
│   ├── mask_design/
│   └── photos/
├── hardware/
│   ├── schematic/
│   ├── pcb/
│   └── bom.xlsx
├── firmware/
│   ├── stm32/
│   └── esp32/
├── data/
│   ├── raw/
│   ├── processed/
│   └── calibration/
├── analysis/
│   ├── notebooks/
│   ├── scripts/
│   └── figures/
├── models/
│   ├── baseline/
│   └── neural_network/
└── manuscript/
    ├── figures/
    └── draft/
```

---

## 附录 B：建议学生每周记录的问题

每周组会前，学生至少回答以下问题：

1. 本周解决了什么技术问题？
2. 哪个结果可复现？
3. 哪个结果不可复现？
4. 失败样品的原因是什么？
5. 数据是否有完整时间戳和实验条件记录？
6. 下一步实验的变量是什么？
7. 当前结果能否支持论文中的一个具体论点？
8. 是否有对照组？
9. 是否有 baseline？
10. 是否有误差分析？
11. 本周新增了哪些数据或代码？
12. 是否把原始数据备份到指定位置？
13. 本周有没有更新 README 或实验记录？
14. 下周最重要的一个风险是什么？

---

## 附录 C：推荐新生第一批阅读主题

建议按以下顺序阅读，而不是随机读论文：

1. 柔性压力传感综述；
2. 柔性应变传感综述；
3. 电子皮肤和触觉传感综述；
4. 多维力/剪切力传感论文；
5. 微结构压力传感论文；
6. 柔性互连和封装论文；
7. 柔性传感器可靠性论文；
8. 柔性传感器神经网络标定论文；
9. 机器人触觉传感论文；
10. 与自己课题应用场景最接近的论文。

### 文献表格模板

| 编号 | 年份 | 期刊/会议 | 传感类型 | 材料 | 结构 | 机制 | 指标 | 测试条件 | 应用 | 优点 | 局限 |
|---|---|---|---|---|---|---|---|---|---|---|---|
| P001 | 2026 |  |  |  |  |  |  |  |  |  |  |

---

## 附录 D：常用英文关键词

### 传感机制

- flexible pressure sensor
- flexible strain sensor
- wearable sensor
- tactile sensor
- electronic skin
- piezoresistive sensor
- capacitive sensor
- piezoelectric sensor
- triboelectric sensor
- magnetic tactile sensor
- optical tactile sensor
- iontronic sensor
- hydrogel sensor

### 结构设计

- microstructured elastomer
- micropyramid
- microdome
- porous structure
- serpentine interconnect
- island-bridge structure
- neutral mechanical plane
- kirigami electronics
- stretchable interconnect
- soft-hard interface
- strain isolation
- mechanical metamaterial

### 工艺

- soft lithography
- photolithography
- spin coating
- sputtering
- evaporation
- wet etching
- dry etching
- reactive ion etching
- laser direct writing
- transfer printing
- nanoimprint lithography
- screen printing
- aerosol jet printing
- inkjet printing
- laser-induced graphene

### 算法

- sensor calibration
- force decoupling
- crosstalk compensation
- neural network calibration
- time-series regression
- domain adaptation
- transfer learning
- TinyML
- embedded machine learning
- tactile learning
- sensor fusion
- drift compensation
- hysteresis compensation

### 应用

- wearable health monitoring
- soft robotics
- robotic tactile sensing
- prosthetic hand
- rehabilitation monitoring
- human-machine interface
- gait analysis
- electronic skin
- oral biomechanics
- dental force sensing

---

## 附录 E：推荐资源链接索引

### 官方 / 教程

- COMSOL Learning Center: https://www.comsol.com/support/learning-center  
- COMSOL Structural Mechanics Module: https://www.comsol.com/structural-mechanics-module  
- Abaqus / SIMULIA: https://www.3ds.com/products/simulia/abaqus  
- Arduino Getting Started: https://docs.arduino.cc/learn/starting-guide/getting-started-arduino/  
- ESP-IDF Get Started: https://docs.espressif.com/projects/esp-idf/en/stable/esp32/get-started/index.html  
- STM32CubeIDE Quick Start: https://www.st.com/resource/en/user_manual/um2553-stm32cubeide-quick-start-guide-stmicroelectronics.pdf  
- KiCad Getting Started: https://docs.kicad.org/  
- FreeCAD Getting Started: https://wiki.freecad.org/Getting_started  
- Blender Manual: https://docs.blender.org/manual/en/latest/index.html  
- Matplotlib: https://matplotlib.org/  
- scikit-learn User Guide: https://scikit-learn.org/stable/user_guide.html  
- PyTorch Tutorials: https://docs.pytorch.org/tutorials/  
- Python Data Science Handbook: https://jakevdp.github.io/PythonDataScienceHandbook/  
- TensorFlow Lite Micro: https://github.com/tensorflow/tflite-micro  
- OriginLab Tutorials: https://www.originlab.com/doc/Tutorials  
- ImageJ / Fiji: https://imagej.net/software/fiji/  
- D2L 动手学深度学习: https://zh.d2l.ai/  
- 菜鸟教程 Python: https://www.runoob.com/python3/python3-tutorial.html  

### GitHub / 开源项目

- Awesome-Touch: https://github.com/linchangyi1/Awesome-Touch  
- FEATS: https://github.com/feats-ai/feats  
- TACTO: https://github.com/facebookresearch/tacto  
- TensorFlow Lite Micro Arduino Examples: https://github.com/tensorflow/tflite-micro-arduino-examples  
- Python Data Science Handbook GitHub: https://github.com/jakevdp/PythonDataScienceHandbook  
- Open-source Magnetic Tactile Sensor: https://github.com/LowiekVDS/Open-source-Magnetic-Tactile-Sensor  
- FlexiTac project page: https://flexitac.github.io/  

### B站建议检索

- 江协科技 STM32 入门教程  
- 正点原子 STM32 HAL 库开发全集  
- KiCad 画电路板 入门  
- COMSOL 多物理场仿真 技术应用 专题培训  
- Abaqus 超弹性 接触 PDMS 仿真  
- 微纳加工 光刻 显影 刻蚀  
- 电子束曝光 E-Beam Lithography  
- 软光刻 PDMS 微结构  
- 激光直写 柔性电子  
- 跟李沐学 AI  
- 吴恩达机器学习  
- Origin 科研绘图 教程  
- ImageJ 图像分析 教程  

---

## 附录 F：GitHub README 发布建议

如果这份文件作为 GitHub 仓库首页，建议仓库结构如下：

```text
flexible-electronics-learning-roadmap/
├── README.md
├── LICENSE
├── resources/
│   ├── papers.md
│   ├── tutorials.md
│   └── datasets.md
├── templates/
│   ├── literature_table.xlsx
│   ├── experiment_log_template.md
│   └── weekly_report_template.md
└── figures/
    └── roadmap.png
```

建议 README 开头加入：

```markdown
# Flexible Electronics / Flexible Sensor Learning Roadmap

This repository provides a practical learning roadmap for new graduate students entering flexible electronics and flexible sensor research. It covers sensor fundamentals, mechanical design, multiphysics simulation, fabrication, embedded systems, data analysis, neural-network-based calibration, and research tools.
```

推荐 license：

- 内容文档：CC BY-NC 4.0；
- 代码：MIT License；
- 数据：根据是否公开和是否包含受试者信息单独决定。

---

## 附录 G：最小实验记录模板

```markdown
# Experiment Log

## Basic Information

- Date:
- Operator:
- Sample ID:
- Project:
- Data folder:

## Sample Information

- Substrate:
- Sensitive material:
- Electrode:
- Encapsulation:
- Fabrication date:
- Key process parameters:

## Test Setup

- Instrument:
- Force sensor:
- Displacement stage:
- Sampling rate:
- Loading protocol:
- Temperature / humidity:

## Data

- Raw data path:
- Processed data path:
- Code version:
- Notes:

## Observations

- What worked:
- What failed:
- Possible reasons:
- Next step:
```

---

## 附录 H：组会汇报模板

```markdown
# Weekly Report

## 1. This week's goal

## 2. What I did

## 3. Key results

## 4. Problems

## 5. Data and files generated

## 6. What I learned

## 7. Plan for next week
```

---

## 结语

柔性电子研究的真正难点不在于某一个软件或某一种材料，而在于能否把**结构、材料、工艺、电路、数据和应用**连成一个可信的系统。对新生来说，最重要的不是一开始就追求顶级性能，而是先完成一个可复现的小闭环，然后不断把每个环节做扎实。

最终目标不是“做出一个能变电阻的材料”，而是：

> **做出一个可解释、可制备、可采集、可标定、可应用、可发表、可复现的柔性传感系统。**
