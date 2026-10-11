# 考古纺织品残缺纹样数字恢复：初步文献检索

检索日期：2026-10-11（Asia/Shanghai）  
状态：候选文献清单。已核对 DOI 注册、题名和出版信息；相关性仅按摘要初筛，尚未阅读全文或完成系统综述。

## 检索方式与边界

- 数据库：OpenAlex 检索候选记录，Crossref 按 DOI 核对书目元数据；摘要来自 Crossref 或 OpenAlex 索引。
- 查询词：`archaeological textile pattern restoration`、`ancient textile pattern reconstruction digital`、`historical textile image inpainting`、`cultural heritage textile pattern reconstruction`、`archaeological textile image restoration deep learning`、`ancient textile pattern digital restoration`、`heritage textile pattern analysis computer vision`、`cultural heritage image inpainting structural pattern`。
- 上述 OpenAlex 查询返回的记录数依次为 5131、4289、159、10291、2052、3390、6241、632。数字含大量不相关结果，**不是纳入文献数**；本清单是初步定向筛选，尚未进行全文筛选、引用追踪或中文数据库检索。
- 任何摘要中的性能、数据规模和方法结论都只是作者报告；写论文前需核对正文的样本、数据划分、指标定义、基线和局限。

## 直接相关：纹样或纺织文物图像补全

| 年份 | 论文与 DOI | 摘要显示的关联 | 待全文核对 |
|---|---|---|---|
| 2024 | Wang 等，*Context-Encoder-Based Image Inpainting for Ancient Chinese Silk*，*Applied Sciences*，[10.3390/app14156607](https://doi.org/10.3390/app14156607) | 古代丝绸残缺纹样；比较 Context-Encoder 类图像补全方法。摘要报告 6996 个 256×256 样本。 | 样本是否独立、损伤掩码、实物来源、指标和数据可得性。 |
| 2022 | Stoean 等，*On Using Perceptual Loss within the U-Net Architecture for the Semantic Inpainting of Textile Artefacts with Traditional Motifs*，SYNASC，[10.1109/SYNASC57785.2022.00051](https://doi.org/10.1109/SYNASC57785.2022.00051) | U-Net、感知损失、传统纹样的语义补全；OpenAlex 摘要描述了罗马尼亚传统背心图像。 | 训练/测试图像来源、评价设计、感知损失效果和适用于考古纺织品的边界。 |
| 2024 | Sha 等，*Image Classification and Restoration of Ancient Textiles Based on Convolutional Neural Network*，*International Journal of Computational Intelligence Systems*，[10.1007/s44196-023-00381-9](https://doi.org/10.1007/s44196-023-00381-9) | 古代纺织图像的纹样元素分类与 GAN 修复；摘要称使用 YOLOv4–ViT 与改进 GAN。 | 分类与修复实验是否分开评价，真实文物样本及泛化性。 |
| 2026 | Yang 等，*Digital restoration for textile cultural relics via a structure-guided neural network based on CNN-Transformer*，*npj Heritage Science*，[10.1038/s40494-026-02836-6](https://doi.org/10.1038/s40494-026-02836-6) | 古代纺织纹样的结构与纹理协同恢复，使用 CNN–Transformer；OpenAlex 摘要提及模拟数据和真实纺织图像。 | 结构先验的具体实现、数据与对照、真实样本评价；与本项目拟定方案是否实质重合。 |
| 2026 | Wang 等，*Weavega: a deep learning-based “human + AI” Method for the Restoration of Tang Dynasty Hunting-pattern Kesi Silk Fragments*，*npj Heritage Science*，[10.1038/s40494-026-02855-3](https://doi.org/10.1038/s40494-026-02855-3) | 以唐代缂丝残片为案例，摘要提出扩散模型、检索辅助和专家筛选的协同修复。 | 个案数据、专家评分协议、候选生成与可推广性。 |

## 背景与任务边界

| 年份 | 论文与 DOI | 用途 |
|---|---|---|
| 2025 | Ying 等，*Digital image inpainting techniques for damaged textile cultural relics: A review of texture, pattern, and structural restoration*，*Textile Research Journal*，[10.1177/00405175251372973](https://doi.org/10.1177/00405175251372973) | 综述候选；适合追踪原始研究，不能直接替代对所引论文的阅读。 |
| 2023 | Gigilashvili 等，*Computational techniques for virtual reconstruction of fragmented archaeological textiles*，*Heritage Science*，[10.1186/s40494-023-01102-3](https://doi.org/10.1186/s40494-023-01102-3) | 考古纺织品**残片拼接/虚拟重组**综述，与同一图像内缺失纹样补全不同；可用于界定研究任务。 |
| 2026 | Kresović 等，*Puzzle-like virtual reconstruction of fragmented historical textiles using graph-based learning*，*npj Heritage Science*，[10.1038/s40494-026-02992-9](https://doi.org/10.1038/s40494-026-02992-9) | 图学习残片邻接的相邻方向；不宜当作纹样缺损补全的直接基线。 |

## 对当前拟议方案的提示

用户上传的项目迁移记忆提出 U-Net 基线、CNN–Transformer 与纹样结构先验。这是用户提供的**拟议方案**，尚非仓库已确认的实验结果或论文结论。上表已有 U-Net 修补传统纹样、CNN–Transformer 结构引导纺织纹样修复的先例，因此不能仅凭这两个架构宣称创新。下一步应阅读全文，比较数据来源、结构先验、真实残片评价和可复现性，再确定可检验的研究差异。

本文未生成论文正文，未下载或修改原始论文及图像数据。
