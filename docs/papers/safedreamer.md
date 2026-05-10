# SafeDreamer 阅读笔记

## 基本信息

- **论文标题**: SafeDreamer: Safe Reinforcement Learning with World Models
- **发表**: ICLR 2024
- **关键词**: Safe RL, World Models, DreamerV3, Lagrangian, CMDP

---

## 核心思路

在 DreamerV3 的 world model 框架里引入 Lagrangian 方法，让 agent 在 latent imagination 中同时优化 reward 和满足安全约束（cost 趋近于零）。

**动机**：现有 model-free Safe RL（PPO-Lag 等）在 cost threshold 接近零时 critic 估计不准，表现很差；而已有的 model-based 方法（LAMBDA、Safe SLAC）没有充分利用 online + background planning 的组合。

**四个变体**：

- **OSRP**：在线用 CCEM 在 world model 里 rollout 轨迹，筛选满足 cost 约束的，再选 reward 最高的执行
- **OSRP-Lag**：加 PID Lagrangian，用 TD(λ) 估计 cost value，排序用 J_R - λ_p * J_C
- **BSRP-Lag**：后台规划，用 Augmented Lagrangian 训练 safe actor，不做在线 planning，适合实时性要求高的场景
- **SafeDreamer**：以上组合的统一框架

**关键设计**：

- World model loss 里显式加了 cost decoder loss（β_c ln C_φ），让 latent state 编码安全信息
- TD(λ) 同时估计 reward value 和 cost value
- Lagrangian multiplier 根据实际 episode cost return 动态更新

---

## 实验结果

- Safety-Gymnasium 5 个 vision task 上几乎达到零 cost，reward 与 DreamerV3 持平
- 比 LAMBDA 降低 94.3% cost
- 同时支持 vision 和 low-dimensional input
- OSRP 在动态环境更好，BSRP-Lag 在静态精细操作更好

---

## 与 CILD 的关联

SafeDreamer 验证了在 latent space 里做 cost-aware 规划是可行的，但它的路线是"重建世界 + 外挂 cost head"——world model 通过 observation reconstruction 学习表征，cost 信息只通过一个额外的 decoder loss 间接影响 latent space。

CILD 的路线不同：不重建像素，让 cost structure 直接塑造表征学习。理论上更 compact，latent space 里不会塞入对控制无关的视觉细节。

SafeDreamer 可以作为实验对比的 anchor——它代表"重建 + Lagrangian"路线的 SOTA。如果 CILD 能在相同 benchmark 上用更紧凑的表征达到类似的 cost/reward trade-off，就能说明 cost-informed representation 的价值。

---

## 疑问

- SafeDreamer 的 cost decoder loss 权重 β_c 对表征的影响有多大？如果把 β_c 调很高，是否能逼近 cost-informed representation 的效果？
- 它每个任务独立训练，没有跨任务迁移——如果 cost structure 变了，整个模型要重训，这是重建路线的固有问题还是可以解决的？

