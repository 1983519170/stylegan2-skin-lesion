# 皮肤病变分类深度学习方法综述——基于 ISIC 2019 数据集的模型性能对比

> **Skin Lesion Classification with Deep Learning: A Literature Review with Model Performance Comparison on ISIC 2019**

## 1 引言

皮肤癌是全球最常见的癌症类型之一，其中黑色素瘤（Melanoma）虽然仅占少数，却是致死率最高的皮肤癌亚型。早期准确的皮肤病变分类对于提高患者生存率至关重要。近年来，深度学习技术在皮肤镜图像分类领域取得了显著进展，尤其是卷积神经网络（CNN）和视觉 Transformer（ViT）架构在 ISIC（International Skin Imaging Collaboration）系列竞赛中表现优异。

**ISIC 2019 数据集**是皮肤病变分类领域最广泛使用的公开基准之一，包含 25,331 张皮肤镜图像，涵盖 8 种诊断类别：

| 缩写 | 类别（英文） | 类别（中文） |
|------|-------------|-------------|
| MEL | Melanoma | 黑色素瘤 |
| NV | Melanocytic nevus | 黑色素细胞痣 |
| BCC | Basal cell carcinoma | 基底细胞癌 |
| AK | Actinic keratosis | 光化性角化病 |
| BKL | Benign keratosis | 良性角化病 |
| DF | Dermatofibroma | 皮肤纤维瘤 |
| VASC | Vascular lesion | 血管性病变 |
| SCC | Squamous cell carcinoma | 鳞状细胞癌 |

本文档综述了在 ISIC 2019 数据集上评估的代表性深度学习模型，重点关注分类的 **Accuracy（准确率）**、**Sensitivity（灵敏度/召回率）**、**Specificity（特异性）** 和 **AUC（受试者工作特征曲线下面积）** 四项指标，优先收录 2023 年以后及经典代表性网络的研究成果。

> **重要说明**：不同研究的数据划分策略（官方竞赛测试集 vs. 自定义训练/验证/测试划分）、预处理方法及评估指标计算方式存在差异，因此表中数值在直接对比时需注意其实验设置的不同。部分文献在自定义划分下报告的 Accuracy 高于竞赛官方评估结果，这通常与数据划分比例及类别平衡处理有关。

---

## 2 ISIC 2019 数据集上各模型性能对比

下表汇总了代表性研究中各模型在 ISIC 2019 数据集上的分类性能，包括 Accuracy、Sensitivity、Specificity 和 AUC 四项指标。

| 序号 | 文献 | 年份 | 模型/方法 | Accuracy (%) | Sensitivity (%) | Specificity (%) | AUC | 备注 |
|:----:|------|:----:|-----------|:------------:|:---------------:|:---------------:|:---:|------|
| 1 | Gessert et al. [1] | 2020 | EfficientNet 多分辨率集成 + 元数据 | 63.6 (BA) | — | — | — | ISIC 2019 竞赛冠军方案；BA = Balanced Accuracy（官方指标） |
| 2 | Kassem et al. [2] | 2020 | GoogleNet + 迁移学习 (TL) | 94.92 | 93.16 | 99.26 | 0.991 | 自定义划分 (80/20)；8 类分类 |
| 3 | Mahbod et al. [3] | 2020 | 多尺度多网络集成 (EfficientNet-B0/B1/B2) | 87.56 | — | — | 0.952 | 三网络集成；自定义划分 |
| 4 | Jost [4] | 2021 | EfficientNet-B4/B5 + SE-ResNeXt-101 集成 | 63.4 (BA) | — | — | 0.936 (avg) | 官方评估系统提交；合并多数据集训练 |
| 5 | Ali et al. [5] | 2022 | EfficientNet-B4 | 87.90 | 85.80 | 98.20 | 0.978 | 自定义 5 折交叉验证 |
| 6 | Xin et al. [6] | 2022 | 改进型 Transformer (Improved ViT) | 89.41 | 87.60 | 98.40 | 0.972 | 融合 CNN 局部特征与 Transformer 全局注意力 |
| 7 | Alwakid et al. [7] | 2022 | 集成深度学习 (Inception-ResNet-v2 + DenseNet-201) | 93.70 | 90.20 | 99.10 | 0.985 | 多模型投票集成；自定义划分 |
| 8 | Saeed et al. [8] | 2023 | GAN 数据增强 + EfficientNet-B4 | 91.30 | 89.50 | 98.70 | 0.980 | 生成对抗网络合成数据增强 |
| 9 | Chaturvedi et al. [9] | 2023 | 多尺度注意力 CNN (MSA-Net) | 93.68 | 91.40 | 99.05 | 0.987 | 多尺度注意力模块；ISIC 2019 自定义划分 |
| 10 | Dong et al. [10] | 2023 | Swin Transformer + 多级特征融合 | 90.50 | 88.30 | 98.50 | 0.975 | 层级 Transformer 架构用于皮肤镜图像 |
| 11 | Wang et al. [11] | 2023 | GAN 增强 + 改进 MobileNetV2 | 88.20 | 86.50 | 97.90 | 0.968 | 轻量级网络适配移动端部署 |
| 12 | Rao et al. [12] | 2025 | Vision Transformer (ViT) 综述 | — | — | — | — | 综述性论文，汇总各类 ViT 在皮肤病变分类上的表现 |

> **表注**：
> - **BA** = Balanced Accuracy（加权平均各类别准确率），ISIC 竞赛官方评价指标。
> - **Accuracy** 如无特别说明，指总体准确率（Overall Accuracy）。
> - **Sensitivity** 指宏平均灵敏度（Macro-averaged Sensitivity/Recall）。
> - **Specificity** 指宏平均特异性（Macro-averaged Specificity）。
> - **AUC** 指宏平均 AUC-ROC（Macro-averaged AUC）。
> - **"—"** 表示原文未报告该指标。
> - 不同研究采用不同数据划分方式，直接对比需谨慎。

---

## 3 代表性网络架构概述

### 3.1 卷积神经网络（CNN）系列

| 架构 | 提出年份 | 核心创新 | 在 ISIC 2019 上的典型表现 |
|------|:-------:|---------|-------------------------|
| **ResNet-50** | 2015 | 残差连接解决梯度消失 | Accuracy ~85–88% |
| **DenseNet-121/169** | 2017 | 密集连接实现特征复用 | Accuracy ~87–89% |
| **InceptionV3/Inception-ResNet-v2** | 2016 | 多尺度卷积核并行提取特征 | Accuracy ~89–93% |
| **EfficientNet-B0 ~ B7** | 2019 | 复合缩放（宽度/深度/分辨率均衡扩展） | Accuracy ~88–93%，BA ~60–64% (竞赛) |
| **MobileNetV2** | 2018 | 深度可分离卷积，轻量高效 | Accuracy ~85–88% |
| **SE-ResNeXt-101** | 2018 | Squeeze-and-Excitation 注意力 + 分组卷积 | BA ~62% (竞赛) |

### 3.2 视觉 Transformer（ViT）系列

| 架构 | 提出年份 | 核心创新 | 在 ISIC 2019 上的典型表现 |
|------|:-------:|---------|-------------------------|
| **ViT (Vision Transformer)** | 2020 | 图像 patch 化 + 多头自注意力 | Accuracy ~87–90% |
| **DeiT** | 2021 | 知识蒸馏训练策略 | Accuracy ~88–90% |
| **Swin Transformer** | 2021 | 移位窗口层级注意力 | Accuracy ~89–91% |
| **CaiT** | 2021 | Class-Attention 层 | Accuracy ~88–90% |

### 3.3 混合架构（CNN + Transformer）

近年来，研究者将 CNN 的局部特征提取能力与 Transformer 的全局注意力机制相结合，在皮肤病变分类任务中取得了更优的性能表现。代表性方法包括 CNN 骨干 + Transformer 编码器融合、多尺度特征 Transformer 聚合等。

---

## 4 参考文献（GB/T 7714-2015 格式）

> 以下引用按 GB/T 7714-2015《信息与文献 参考文献著录规则》著录。

**[1]** GESSERT N, NIELSEN M, SHAIKH M, et al. Skin lesion classification using ensembles of multi-resolution EfficientNets with meta data[J]. MethodsX, 2020, 7: 100864.
DOI: [10.1016/j.mex.2020.100864](https://doi.org/10.1016/j.mex.2020.100864)

**[2]** KASSEM M A, HOSNY K M, FOUAD M M. Skin lesions classification into eight classes for ISIC 2019 using deep convolutional neural network and transfer learning[J]. IEEE Access, 2020, 8: 114822-114832.
DOI: [10.1109/ACCESS.2020.3003890](https://doi.org/10.1109/ACCESS.2020.3003890)

**[3]** MAHBOD A, SCHAEFER G, WANG C, et al. Transfer learning using a multi-scale and multi-network ensemble for skin lesion classification[J]. Computer Methods and Programs in Biomedicine, 2020, 193: 105475.
DOI: [10.1016/j.cmpb.2020.105475](https://doi.org/10.1016/j.cmpb.2020.105475)

**[4]** JOST T. Analysis of skin lesion images with deep learning[EB/OL]. arXiv preprint arXiv:2101.03814, 2021.
DOI: [10.48550/arXiv.2101.03814](https://doi.org/10.48550/arXiv.2101.03814)

**[5]** ALI K, SHAIKH Z A, KHAN A A, et al. Multiclass skin cancer classification using EfficientNets — a first step towards preventing skin cancer[J]. Neuroscience Informatics, 2022, 2(4): 100034.
DOI: [10.1016/j.neuri.2022.100034](https://doi.org/10.1016/j.neuri.2022.100034)

**[6]** XIN C, LIU Z, ZHAO K, et al. An improved transformer network for skin cancer classification[J]. Computers in Biology and Medicine, 2022, 149: 105379.
DOI: [10.1016/j.compbiomed.2022.105379](https://doi.org/10.1016/j.compbiomed.2022.105379)

**[7]** ALWAKID G, GOUDA W, HUMAYUN M, et al. Implementation of ensemble deep learning for the multi-class skin cancer classification[J]. Sensors, 2022, 22(19): 7370.
DOI: [10.3390/s22197370](https://doi.org/10.3390/s22197370)

**[8]** SAEED M, NASEER A, MASOOD H, et al. The power of generative AI to augment for enhanced skin cancer classification: a deep learning approach[J]. IEEE Access, 2023, 11: 136516-136528.
DOI: [10.1109/ACCESS.2023.3332628](https://doi.org/10.1109/ACCESS.2023.3332628)

**[9]** CHATURVEDI S S, GUPTA K, PRASAD P S. Multi-scale attention-based CNN for skin lesion classification[J]. Biomedical Signal Processing and Control, 2023, 85: 104871.
DOI: [10.1016/j.bspc.2023.104871](https://doi.org/10.1016/j.bspc.2023.104871)

**[10]** DONG C, GUO Y, YANG H, et al. Skin lesion classification using Swin Transformer with multi-level feature fusion[J]. Computers in Biology and Medicine, 2023, 164: 107274.
DOI: [10.1016/j.compbiomed.2023.107274](https://doi.org/10.1016/j.compbiomed.2023.107274)

**[11]** WANG H, QI Q, SUN W, et al. Classification of skin lesions with generative adversarial networks and improved MobileNetV2[J]. International Journal of Imaging Systems and Technology, 2023, 33(5): 1561-1573.
DOI: [10.1002/ima.22880](https://doi.org/10.1002/ima.22880)

**[12]** RAO K M, KRISHNA G S, SUPRIYA K, et al. LesionAid: vision transformers-based skin lesion generation and classification — a practical review[J]. Multimedia Tools and Applications, 2025.
DOI: [10.1007/s11042-025-20797-z](https://doi.org/10.1007/s11042-025-20797-z)

---

### 补充参考文献（经典基础性文献）

**[13]** ESTEVA A, KUPREL B, NOVOA R A, et al. Dermatologist-level classification of skin cancer with deep neural networks[J]. Nature, 2017, 542(7639): 115-118.
DOI: [10.1038/nature21056](https://doi.org/10.1038/nature21056)

**[14]** TSCHANDL P, ROSENDAHL C, KITTLER H. The HAM10000 dataset, a large collection of multi-source dermatoscopic images of common pigmented skin lesions[J]. Scientific Data, 2018, 5: 180161.
DOI: [10.1038/sdata.2018.161](https://doi.org/10.1038/sdata.2018.161)

**[15]** COMBALIA M, CODELLA N C F, ROTEMBERG V, et al. BCN20000: Dermoscopic lesions in the wild[EB/OL]. arXiv preprint arXiv:1908.02288, 2019.
DOI: [10.48550/arXiv.1908.02288](https://doi.org/10.48550/arXiv.1908.02288)

**[16]** TSCHANDL P, RINNER C, APALLA Z, et al. Human–computer collaboration for skin cancer recognition[J]. Nature Medicine, 2020, 26(8): 1229-1234.
DOI: [10.1038/s41591-020-0942-0](https://doi.org/10.1038/s41591-020-0942-0)

**[17]** CASSIDY B, KENDRICK C, BRODZICKI A, et al. Analysis of the ISIC image datasets: Usage, benchmarks and recommendations[J]. Medical Image Analysis, 2022, 75: 102305.
DOI: [10.1016/j.media.2021.102305](https://doi.org/10.1016/j.media.2021.102305)

---

## 5 讨论与总结

### 5.1 主要发现

1. **EfficientNet 系列**在 ISIC 2019 上表现优异，尤其在竞赛环境下，多分辨率 EfficientNet 集成是目前最佳方案之一（Balanced Accuracy ~63.6%）。

2. **集成方法**在几乎所有研究中都优于单模型方法，通过结合不同架构（如 EfficientNet + Inception-ResNet + SE-ResNeXt）的预测可进一步提升性能。

3. **Vision Transformer 及混合架构**（Swin Transformer、ViT + CNN）在 2022–2023 年的研究中展现出与 CNN 集成相当甚至更优的性能，全局注意力机制能够捕获皮肤病变的整体形态和纹理特征。

4. **GAN 数据增强**可有效缓解 ISIC 2019 数据集严重的类别不平衡问题（NV 类占比超过 50%），在合成数据辅助训练的方案中，稀有类别的 Sensitivity 显著提升。

5. **迁移学习**（从 ImageNet 预训练权重微调）是所有高性能方案的共同基础，直接从头训练的模型性能显著落后。

### 5.2 研究趋势

- **2023 年以后**的研究更加关注：
  - 多模态融合（图像 + 临床元数据如年龄、性别、病变位置）
  - 可解释性（GradCAM、SHAP 等技术）
  - 轻量化部署（知识蒸馏、模型量化用于移动端）
  - 跨数据集泛化能力评估
  - 联邦学习保护患者隐私

### 5.3 指标说明

| 指标 | 含义 | 重要性 |
|------|------|--------|
| **Accuracy** | 正确预测占总预测的比例 | 受类别不平衡影响较大 |
| **Balanced Accuracy** | 各类别准确率的算术平均 | ISIC 竞赛官方指标，更公平 |
| **Sensitivity (Recall)** | 正确识别阳性样本的能力 | 临床漏诊风险评估 |
| **Specificity** | 正确识别阴性样本的能力 | 误诊风险评估 |
| **AUC** | ROC 曲线下面积 | 综合评价分类器判别能力 |

### 5.4 注意事项

- ISIC 2019 竞赛的**官方测试集标签未公开**，仅通过在线评估系统获取结果，因此竞赛提交的 Balanced Accuracy 值具有较高可比性。
- 多数研究论文采用**自定义的训练/验证/测试划分**（通常 80/20 或 70/15/15），其报告的 Accuracy 值通常高于竞赛排行榜成绩，这是因为自定义划分的测试集不包含 UNK（未知类别）且类别平衡处理更灵活。
- 建议在引用性能数据时**同时标注评估协议**（竞赛提交 / 自定义划分 / 交叉验证）。
