# 04 Parameter Table

本文件用于集中记录项目中的关键参数、含义、单位和当前状态。当前阶段部分参数尚未最终确定，可先用 `TBD` 标记。

## 1. 几何参数

| 参数名 | 含义 | 当前状态 | 单位 | 备注 |
|---|---|---:|---|---|
| `width` | PFC 颗粒区域宽度 | TBD | m | 应与耦合墙和 zone 空区尺寸对应 |
| `height` | PFC 颗粒区域高度 | TBD | m | 应与耦合墙和 zone 空区尺寸对应 |
| `maishen` | 埋深或模型顶部深度控制参数 | TBD | m | 用于确定初始应力或模型位置 |
| `domain_x_min` | 模型 domain 左边界 | TBD | m | 需覆盖 PFC 与 zone 计算范围 |
| `domain_x_max` | 模型 domain 右边界 | TBD | m | 需覆盖 PFC 与 zone 计算范围 |
| `domain_y_min` | 模型 domain 下边界 | TBD | m | 需覆盖 PFC 与 zone 计算范围 |
| `domain_y_max` | 模型 domain 上边界 | TBD | m | 需覆盖 PFC 与 zone 计算范围 |
| `stope_width` | 矿房宽度 | TBD | m | 当前可先使用矩形矿房 |
| `stope_height` | 矿房高度 | TBD | m | 当前可先使用矩形矿房 |
| `stope_center_x` | 矿房中心 x 坐标 | TBD | m | 用于选中待删除颗粒 |
| `stope_center_y` | 矿房中心 y 坐标 | TBD | m | 用于选中待删除颗粒 |

## 2. 颗粒生成参数

| 参数名 | 含义 | 当前状态 | 单位 | 备注 |
|---|---|---:|---|---|
| `rdmin` | 最小颗粒半径 | TBD | m | 控制颗粒级配 |
| `rdmax` | 最大颗粒半径 | TBD | m | 控制颗粒级配 |
| `porosity` | 初始孔隙率 | TBD | - | 用于颗粒生成 |
| `density` | 颗粒密度 | TBD | kg/m³ | 后续应与岩石类型对应 |
| `damp` | 颗粒局部阻尼 | TBD | - | 用于加速平衡 |

## 3. 原岩应力与伺服参数

| 参数名 | 含义 | 当前状态 | 单位 | 备注 |
|---|---|---:|---|---|
| `sigma_v` | 目标竖向应力 | TBD | Pa | 可由埋深和容重估算 |
| `sigma_h` | 目标水平应力 | TBD | Pa | 可由侧压系数或给定值确定 |
| `k0` | 侧压系数 | TBD | - | 若使用 `sigma_h = k0 * sigma_v` |
| `servo_gain` | 伺服增益 | TBD | - | 控制墙体速度调整强度 |
| `servo_tol` | 应力误差容许值 | TBD | - | 用于判断伺服是否达到目标 |
| `servo_max_velocity` | 墙体最大速度 | TBD | m/s | 防止伺服加载过快 |
| `equilibrium_ratio` | 平衡判据 | TBD | - | 用于判断模型是否稳定 |

## 4. PFC 接触模型参数

当前阶段，PFC 区域接触模型计划先套用本地参考案例“含裂隙岩体原岩应力平衡与开挖扰动模拟”中的接触模型。由于该案例为 PFC5.0 版本，以下参数需要在转换并确认后填充。

| 参数名 | 含义 | 当前状态 | 单位 | 备注 |
|---|---|---:|---|---|
| `emod` | 接触有效模量 | TBD | Pa | 需根据参考案例确认 |
| `kratio` | 法向/切向刚度比 | TBD | - | 需根据参考案例确认 |
| `fric` | 摩擦系数 | TBD | - | 需根据参考案例确认 |
| `pb_emod` | 平行键有效模量 | TBD | Pa | 若使用平行键模型 |
| `pb_kratio` | 平行键刚度比 | TBD | - | 若使用平行键模型 |
| `pb_ten` | 平行键抗拉强度 | TBD | Pa | 控制拉伸破坏 |
| `pb_coh` | 平行键黏聚力 | TBD | Pa | 控制剪切破坏 |
| `pb_fa` | 平行键摩擦角 | TBD | degree | 若参考案例中使用 |
| `contact_model` | 接触模型类型 | TBD | - | 需确认 linear、linearpbond 或其他模型 |

## 5. FLAC zone 参数

当前阶段，FLAC 的本构模型和参数先保持原始版本不变。后续如有修改，再在此表补充。

| 参数名 | 含义 | 当前状态 | 单位 | 备注 |
|---|---|---:|---|---|
| `zone_density` | zone 密度 | 原始版本 | kg/m³ | 暂不修改 |
| `zone_model` | FLAC 本构模型 | 原始版本 | - | 暂不修改 |
| `zone_bulk` | 体积模量 | 原始版本 | Pa | 暂不修改 |
| `zone_shear` | 剪切模量 | 原始版本 | Pa | 暂不修改 |
| `zone_young` | 弹性模量 | 原始版本 | Pa | 若原始版本使用 |
| `zone_poisson` | 泊松比 | 原始版本 | - | 若原始版本使用 |

## 6. 耦合参数

| 参数名 | 含义 | 当前状态 | 单位 | 备注 |
|---|---|---:|---|---|
| `coupling_x_min` | 耦合边界左侧范围 | TBD | m | 应与 PFC 区域边界一致 |
| `coupling_x_max` | 耦合边界右侧范围 | TBD | m | 应与 PFC 区域边界一致 |
| `coupling_y_min` | 耦合边界下侧范围 | TBD | m | 应与 PFC 区域边界一致 |
| `coupling_y_max` | 耦合边界上侧范围 | TBD | m | 应与 PFC 区域边界一致 |
| `zone_margin` | zone 区域外扩距离 | TBD | m | 决定远场范围 |
| `coupling_wall_id` | 耦合墙编号 | TBD | - | 需避免与伺服墙体冲突 |

## 7. 开挖与保存参数

| 参数名 | 含义 | 当前状态 | 单位 | 备注 |
|---|---|---:|---|---|
| `excavation_method` | 开挖方式 | 删除 PFC 颗粒 | - | 当前采用颗粒删除形成采空区 |
| `excavation_steps` | 开挖步数 | TBD | - | 当前可先一次性删除 |
| `save_interval` | 自动保存间隔 | 后续整理 | s 或力学时间 | 流程打通后再优化 |
| `save_count` | 保存文件编号 | 后续整理 | - | 用于递增保存文件名 |
| `total_calculation_time` | 开挖后计算时间 | TBD | s 或力学时间 | 待确定 |

## 8. 后续多岩性参数

流程打通后，计划通过多个 DXF 区域完成不同岩性区的颗粒分组和赋参。

| 参数名 | 含义 | 当前状态 | 单位 | 备注 |
|---|---|---:|---|---|
| `rock_group_name` | 岩性分组名称 | 后续扩展 | - | 例如 ore、hanging_wall、footwall |
| `dxf_region_file` | DXF 区域文件 | 后续扩展 | - | 用于导入复杂区域 |
| `group_density` | 分组颗粒密度 | 后续扩展 | kg/m³ | 多岩性赋参 |
| `group_contact_model` | 分组接触模型 | 后续扩展 | - | 不同岩性可采用不同参数 |
