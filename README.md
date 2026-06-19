# Motion-JEPA · Motion Embedding 交互式可视化

**在线访问（GitHub Pages）：https://hongzefu.github.io/motionjepa-viz/**

Motion-JEPA 学到的**潜在运动向量（motion token）**的交互式散点图：t-SNE / UMAP 投影，可按 task / episode / variant 着色，悬停任一点即播放对应的视频 clip，用来直观检查 motion token 是否按动作语义聚类。公网永久托管，无需在本地起服务即可查看。

## 当前可用的可视化

| 页面 | 检查点 | 说明 |
|---|---|---|
| [localDiT_4env_v3_dual epoch 8](https://hongzefu.github.io/motionjepa-viz/localDiT_4env_v3_dual_epoch8/interactive.html) | `checkpoint_epoch_8.pt` (EMA) | epoch 8 / 40，训练中最新快照 |
| [localDiT_4env_dual epoch 16](https://hongzefu.github.io/motionjepa-viz/localDiT_4env_dual_epoch16/interactive.html) | `checkpoint_epoch_16.pt` (EMA) | epoch 16，离线评估时段的快照 |

两次运行训练配置相同：双流 SigLIP + DINOv3，AdamW lr 3e-4、wd 1e-4、fp32、batch 8/卡、max_epochs 40。入口页 [index.html](https://hongzefu.github.io/motionjepa-viz/) 提供两页对比导航。

## 仓库约束

**本仓库仅托管可视化本体，不含任何源代码、训练脚本、配置、检查点或原始数据。** 每个页面运行时只依赖：

- `interactive.html` 自身（t-SNE/UMAP 坐标与 labels 已内联进 HTML）
- 相对路径下的 `clips/*.mp4`（每个 chunk 一个短视频，用于悬停播放）
- 从 cdn.plot.ly 加载的 Plotly（唯一外部依赖）

模型代码、训练与抽取流程见私有主仓库 Motion-JEPA。

## 新增可视化

在仓库内新建子目录，放入该 run/epoch 的 `interactive.html` 与 `clips/`，并在入口页 `index.html` 追加导航，push 后 GitHub Pages 自动重建。
