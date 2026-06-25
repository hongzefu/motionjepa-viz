# Motion-JEPA · Motion Embedding 交互式可视化

**在线访问（GitHub Pages）：https://hongzefu.github.io/motionjepa-viz/**

Motion-JEPA 学到的**潜在运动向量（motion token）**的交互式散点图：t-SNE / UMAP 投影，可按 task / episode / variant 着色，悬停任一点即播放对应的视频 clip，用来直观检查 motion token 是否按动作语义聚类。公网永久托管，无需在本地起服务即可查看。

## 当前可用的可视化

同一套 4 环境数据、不同**特征流配置**的 Motion-JEPA：单流 / 双流 / 三流(+光流) 对比。

| 页面 | 特征流 / 监督 | 检查点 | 数据集 |
|---|---|---|---|
| [localDiT_4env_v3_dual epoch 40](https://hongzefu.github.io/motionjepa-viz/localDiT_4env_v3_dual_epoch40/interactive.html) | 双流 SigLIP⊕DINOv3 / siglip+dino | `checkpoint_epoch_40.pt` (EMA) | v3 |
| [localDiT_4env_v3_single epoch 40](https://hongzefu.github.io/motionjepa-viz/localDiT_4env_v3_single_epoch40/interactive.html) | 单流 纯 SigLIP / siglip | `checkpoint_epoch_40.pt` (EMA) | v3 |
| [localDiT_4env_v3_nosiglip epoch 40](https://hongzefu.github.io/motionjepa-viz/localDiT_4env_v3_nosiglip_epoch40/interactive.html) | 纯 DINOv3 监督（siglip_weight=0） | `checkpoint_epoch_40.pt` (EMA) | v3 |
| [localDiT_4env_v4_flowSliding epoch 40](https://hongzefu.github.io/motionjepa-viz/localDiT_4env_v4_flowSliding_epoch40/interactive.html) | 三流 +光流(sliding, w=1.0) | `checkpoint_epoch_40.pt` (EMA) | v4 |
| [localDiT_4env_v4_flowSum epoch 40](https://hongzefu.github.io/motionjepa-viz/localDiT_4env_v4_flowSum_epoch40/interactive.html) | 三流 +光流(sum, w=0.4 降权) | `checkpoint_epoch_40.pt` (EMA) | v4 |
| [localDiT_4env_v4_flowSumDense epoch 40](https://hongzefu.github.io/motionjepa-viz/localDiT_4env_v4_flowSumDense_epoch40/interactive.html) | 三流 +光流(sum **dense**, w=0.4) · 解码器 ConvexUpSample 重建 512 维稠密光流 | `checkpoint_epoch_40.pt` (EMA) | v4 |
| [localDiT_4env_dual epoch 16](https://hongzefu.github.io/motionjepa-viz/localDiT_4env_dual_epoch16/interactive.html) | 双流 SigLIP⊕DINOv3（既有 v2） | `checkpoint_epoch_16.pt` (EMA) | v2 |

各 run 模型骨干相同（chunk-based local DiT，motion dim 384、K=16、EMA），差异在特征流 / 监督目标 / 数据集版本。6 个新 run（v3/v4）散点样本一致：N=323（episodes 90–99）。v4 三个光流 run（flowSliding / flowSum / flowSumDense）已训练完成（epoch 40）。6 个 v3/v4 run 全部 epoch 40，仅既有 v2 dual 为 epoch 16。入口页 [index.html](https://hongzefu.github.io/motionjepa-viz/) 提供对比导航与差异表。

## 仓库约束

**本仓库仅托管可视化本体，不含任何源代码、训练脚本、配置、检查点或原始数据。** 每个页面运行时只依赖：

- `interactive.html` 自身（t-SNE/UMAP 坐标与 labels 已内联进 HTML）
- 相对路径下的 `clips/*.mp4`（每个 chunk 一个短视频，用于悬停播放）
- 从 cdn.plot.ly 加载的 Plotly（唯一外部依赖）

模型代码、训练与抽取流程见私有主仓库 Motion-JEPA。

## 新增可视化

在仓库内新建子目录，放入该 run/epoch 的 `interactive.html` 与 `clips/`，并在入口页 `index.html` 追加导航，push 后 GitHub Pages 自动重建。
