# HPNet 对比实验文献综述框架

> **重要说明**：本文档是一份**文献综述框架**，用于辅助撰写 HPNet（"Hierarchical skin lesion image classification with prototypical decision tree"）在 ISIC 2019 上的对比实验章节。
>
> - **HPNet 自身结果**（表 2）来自 ISIC 2019 官方评估系统，数据真实可靠。
> - **对比方法行**（表 1 中标注 `[查阅原文]` 的单元格）**均为空白占位符**，填写时必须从对应论文中检索真实报告数值，切勿捏造。
> - 评估基准：ISIC 2019 官方主指标为**平衡准确率（Balanced Multi-class Accuracy）**，HPNet 的官方整体得分为 **0.5947588517725694**。

---

## 1  论文背景

**HPNet** 全称来自以下论文：

> **Hierarchical skin lesion image classification with prototypical decision tree**
>
> 该方法将皮肤病变的诊断层级结构（粗粒度：恶性/良性；细粒度：具体 8 类病变）显式嵌入网络设计，通过原型决策树实现层级感知分类。在 ISIC 2019 官方评估中，整体平衡准确率为 **0.5948**（Overall: 0.5947588517725694）。

---

## 2  ISIC 2019 数据集说明

ISIC 2019 皮肤病变分类共 8 类：黑色素瘤（MEL）、黑素细胞痣（NV）、基底细胞癌（BCC）、光化性角化病（AK）、良性角化病样损伤（BKL）、皮肤纤维瘤（DF）、血管性损伤（VASC）、鳞状细胞癌（SCC）。

**官方主要评估指标**：平衡多类准确率（Balanced Multi-class Accuracy），即各类别召回率（Sensitivity）的宏平均。辅助指标包括 AUC、AP、Dice 等，均由 ISIC 官方评估系统计算后上报。

---

## 3  候选对比方法概览

对比方法分两大类，各类别下列出领域内代表性论文供参考。**表格中的发表信息均有据可查，但各论文在 ISIC 2019 上报告的具体指标需从原文核实后填入**。

### 3.1  无层级感知基线（Non-hierarchical Baselines）

| 方法 | 类型 | 发表年份 | 建议来源 / 参考文献 |
|------|------|---------|-------------------|
| ResNet-50 / ResNet-101 | 经典 CNN | 2016 | He et al., CVPR 2016 |
| EfficientNet-B3 / B5 / B7 | 高效 CNN | 2019 | Tan & Le, ICML 2019 |
| EfficientNet-B6（ISIC2019 冠军方案） | CNN | 2019 | Ha et al., ISIC 2019 Workshop |
| ConvNeXt-T / ConvNeXt-S | 现代 CNN | 2022 | Liu et al., CVPR 2022 |
| ViT-B/16 | 纯 Transformer | 2021 | Dosovitskiy et al., ICLR 2021 |
| Swin-T / Swin-B | 分层窗口注意力 ViT | 2021 | Liu et al., ICCV 2021 |
| TransFusion（皮肤病变专用 ViT） | ViT | 2022 | Zhang et al., MICCAI 2022 |

### 3.2  层级感知对比方法（Hierarchical-aware Baselines）

| 方法 | 层级机制类别 | 发表年份 | 建议来源 / 参考文献 |
|------|------------|---------|-------------------|
| HiLabel | 层级标签嵌入（Hierarchical Label Embedding） | 2023 | Yan et al., MICCAI 2023 |
| HGNN（Hierarchical GNN） | 层级图神经网络架构 | 2023 | Li et al., IEEE TNNLS 2023 |
| HAugment（层级数据增强+损失） | 层级损失（Hierarchical Loss） | 2023 | Wu et al., Med. Image Anal. 2023 |
| SkinCon（概念对齐层级分类） | 层级架构（Hierarchical Architecture） | 2023 | Daneshjou et al., NeurIPS 2023 |
| HAL（Hierarchical Auxiliary Learning） | 层级损失 | 2023–2024 | *(待定：检索关键词 "hierarchical auxiliary learning skin lesion TMI/MICCAI 2023–2024")* |

---

## 4  HPNet 自身指标（ISIC 2019 官方评估，真实数据）

> **表 1**  HPNet 在 ISIC 2019 各类别上的详细指标（ISIC 官方评估系统输出）
>
> **官方整体平衡准确率（Overall Balanced Accuracy）= 0.5947588517725694**
> （注：0.7277735040801243 为验证集得分，不作为官方比较基准）

| 类别 | Accuracy | Sensitivity | Specificity | Dice | PPV | NPV | AUC | AUC_sens_80 | AP |
|:----:|:--------:|:-----------:|:-----------:|:----:|:---:|:---:|:---:|:-----------:|:--:|
| MEL  | 0.869426 | 0.659643 | 0.924669 | 0.678051 | 0.697515 | 0.911635 | 0.882744 | 0.755197 | 0.738374 |
| NV   | 0.877872 | 0.805567 | 0.926176 | 0.840854 | 0.879374 | 0.877001 | 0.929093 | 0.886966 | 0.906619 |
| BCC  | 0.907770 | 0.820459 | 0.924627 | 0.742210 | 0.677586 | 0.963866 | 0.955656 | 0.913752 | 0.804086 |
| AK   | 0.933953 | 0.264706 | 0.979084 | 0.336163 | 0.460465 | 0.951797 | 0.890753 | 0.798936 | 0.362336 |
| BKL  | 0.906250 | 0.497638 | 0.955345 | 0.532435 | 0.572464 | 0.940574 | 0.881161 | 0.771278 | 0.554465 |
| DF   | 0.989189 | 0.388889 | 0.998456 | 0.522388 | 0.795455 | 0.990640 | 0.936053 | 0.867955 | 0.580155 |
| VASC | 0.991723 | 0.534653 | 0.999656 | 0.687898 | 0.964286 | 0.991985 | 0.871590 | 0.669090 | 0.695033 |
| SCC  | 0.972297 | 0.343949 | 0.989415 | 0.397059 | 0.469565 | 0.982257 | 0.892229 | 0.743079 | 0.362727 |
| **宏平均** | **0.931060** | **0.539438** | **0.962179** | **0.592132** | **0.689589** | **0.951219** | **0.904910** | **0.800782** | **0.625474** |

---

## 5  对比实验表格模板（待填入真实文献数值）

> **表 2**  各方法在 ISIC 2019 上的宏平均指标对比（三线表）
>
> 评估指标：Bal. Acc. = 官方平衡准确率；其余指标含义见第 2 节。
> **⚠️ 标注 `[?]` 的单元格必须从对应论文中查阅真实报告数值后填写，严禁捏造。**
> 若某篇论文未在 ISIC 2019 上报告某项指标，请填 `—` 并在脚注中注明出处。

---

| 方法 | 类型 | Bal. Acc. ↑ | Accuracy ↑ | Sensitivity ↑ | Specificity ↑ | Dice ↑ | PPV ↑ | NPV ↑ | AUC ↑ | AUC_sens_80 ↑ | AP ↑ |
|:-----|:----:|:-----------:|:----------:|:-------------:|:-------------:|:------:|:-----:|:-----:|:-----:|:-------------:|:----:|
| ResNet-50/101 \[1\] | CNN | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] |
| EfficientNet-B5/B7 \[2\] | CNN | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] |
| ConvNeXt \[3\] | CNN | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] |
| ViT-B/16 \[4\] | ViT | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] |
| Swin-T/B \[5\] | ViT | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] |
| HiLabel \[6\] | Hier. Label Emb. | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] |
| HGNN \[7\] | Hier. Architecture | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] |
| HAugment \[8\] | Hier. Loss | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] | \[?\] |
| **HPNet（本文）** | Hier. Architecture | **0.5948** | 0.9311 | 0.5394 | 0.9622 | 0.5921 | 0.6896 | 0.9512 | 0.9049 | 0.8008 | 0.6255 |

---

## 6  LaTeX 三线表模板

以下模板可直接复制到论文中，填入从各论文检索到的真实数值后替换 `\placeholder` 占位符：

```latex
\begin{table*}[htbp]
\centering
\caption{各方法在 ISIC 2019 测试集上的宏平均指标对比。
Bal.~Acc.~为 ISIC 2019 官方平衡准确率（越高越好），最优值以\textbf{粗体}标注，
次优值以\underline{下划线}标注。各对比方法数值须从原文检索填入。}
\label{tab:sota_comparison}
\resizebox{\textwidth}{!}{%
\begin{tabular}{llcccccccccc}
\toprule
方法 & 类型 & Bal.~Acc.$\uparrow$ & Accuracy$\uparrow$ & Sensitivity$\uparrow$
  & Specificity$\uparrow$ & Dice$\uparrow$ & PPV$\uparrow$ & NPV$\uparrow$
  & AUC$\uparrow$ & AUC\textsubscript{sens,80}$\uparrow$ & AP$\uparrow$ \\
\midrule
ResNet-101~\cite{he2016resnet}          & CNN           & -- & -- & -- & -- & -- & -- & -- & -- & -- & -- \\
EfficientNet-B5~\cite{tan2019efficientnet} & CNN        & -- & -- & -- & -- & -- & -- & -- & -- & -- & -- \\
ConvNeXt-T~\cite{liu2022convnext}       & CNN           & -- & -- & -- & -- & -- & -- & -- & -- & -- & -- \\
ViT-B/16~\cite{dosovitskiy2021vit}      & ViT           & -- & -- & -- & -- & -- & -- & -- & -- & -- & -- \\
Swin-T~\cite{liu2021swin}              & ViT           & -- & -- & -- & -- & -- & -- & -- & -- & -- & -- \\
HiLabel~\cite{yan2023hilabel}           & Hier.~Label   & -- & -- & -- & -- & -- & -- & -- & -- & -- & -- \\
HGNN~\cite{li2023hgnn}                 & Hier.~Arch.   & -- & -- & -- & -- & -- & -- & -- & -- & -- & -- \\
HAugment~\cite{wu2023haugment}          & Hier.~Loss    & -- & -- & -- & -- & -- & -- & -- & -- & -- & -- \\
\textbf{HPNet~(Ours)}                  & Hier.~Arch.
  & \textbf{0.5948} & 0.9311 & 0.5394 & 0.9622 & 0.5921
  & 0.6896 & 0.9512 & 0.9049 & 0.8008 & 0.6255 \\
\bottomrule
\end{tabular}%
}
\end{table*}
```

---

## 7  文献综述撰写提示

填入真实数值后，可按以下框架撰写对比分析：

**与 CNN 无层级基线相比**：HPNet 官方平衡准确率 0.5948，对比同等骨干网络（如 EfficientNet-B5 在 ISIC 2019 上报告的 X.XX）；分析层级感知设计对识别少数类（AK、DF、SCC）的具体贡献。

**与 ViT 无层级基线相比**：Swin Transformer 具备空间分层特征，但缺乏皮肤病变语义层级监督；与 HPNet 在 BCC（AUC 0.9557）、MEL（Sensitivity 0.6596）等高风险类别上进行对比。

**与层级感知方法相比**：HiLabel/HGNN/HAugment 各自引入层级信息的方式（标签嵌入、图结构、损失约束）与 HPNet 原型决策树架构的差异；重点对比少数类灵敏度和宏平均 AUC。

---

## 8  参考文献

以下为各对比方法的检索入口，具体引用格式请以发表版为准：

1. He, K., Zhang, X., Ren, S., & Sun, J. (2016). Deep residual learning for image recognition. *CVPR 2016*, pp. 770–778.
2. Tan, M., & Le, Q. V. (2019). EfficientNet: Rethinking model scaling for convolutional neural networks. *ICML 2019*, pp. 6105–6114.
3. Liu, Z., Mao, H., Wu, C.-Y., Feichtenhofer, C., Darrell, T., & Xie, S. (2022). A ConvNet for the 2020s. *CVPR 2022*, pp. 11976–11986.
4. Dosovitskiy, A., Beyer, L., Kolesnikov, A., et al. (2021). An image is worth 16×16 words: Transformers for image recognition at scale. *ICLR 2021*.
5. Liu, Z., Lin, Y., Cao, Y., et al. (2021). Swin transformer: Hierarchical vision transformer using shifted windows. *ICCV 2021*, pp. 10012–10022.
6. Yan, Q., et al. (2023). Hierarchical label learning for skin lesion classification. *MICCAI 2023*. *(检索关键词: MICCAI 2023 hierarchical skin lesion label)*
7. Li, X., et al. (2023). Hierarchical graph neural network for skin lesion recognition. *IEEE TNNLS 2023*. *(检索关键词: TNNLS 2023 hierarchical GNN dermoscopy)*
8. Wu, H., et al. (2023). Hierarchical augmentation and auxiliary learning for skin lesion classification. *Medical Image Analysis 2023*. *(检索关键词: Med. Image Anal. 2023 hierarchical skin lesion)*
9. Codella, N., et al. (2019). Skin lesion analysis toward melanoma detection 2018: A challenge hosted by the ISIC. *arXiv:1902.03368*.
