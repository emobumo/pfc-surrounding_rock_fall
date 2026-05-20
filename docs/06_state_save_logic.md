# 06 State Save Logic

## 1. 状态保存逻辑的作用

状态保存用于记录矿房开挖后围岩崩落和塌陷的时间演化过程。

对于崩落模拟，最终状态并不能完整反映破坏过程。因此，需要在计算过程中按一定时间间隔保存多个中间状态，以便后续观察：

- 颗粒崩落过程；
- 采空区周围破坏扩展；
- 上覆岩体移动；
- 耦合边界响应；
- 远场 zone 应力变化；
- 不同时刻的模型稳定性。

## 2. 原始版本中的保存价值

原始版本已经包含自动保存逻辑，并且该部分是后续需要保留的重要内容之一。

其核心思想是：

```text
通过 FISH 函数读取当前力学时间；
判断当前时间与上一次保存时间的差值；
如果超过设定保存间隔，则自动执行 model save；
保存文件名按编号递增；
通过 fish callback 在计算过程中自动调用保存函数。
```

## 3. 当前阶段处理原则

当前阶段的首要目标是打通整体流程，因此结果输出和状态保存暂时不是第一优先级。

当前处理原则为：

1. 保留原始版本中自动保存的基本思想；
2. 暂时不急于重构所有输出格式；
3. 待 PFC 原岩应力恢复、耦合尺寸对接、开挖计算流程稳定后，再统一整理状态保存和结果输出。

## 4. 后续建议保存内容

### 4.1 模型状态文件

建议保存阶段包括：

- 颗粒生成完成；
- 伺服加载完成；
- 接触模型设置完成；
- PFC-zone 耦合完成；
- 初始平衡完成；
- 开挖完成后若干时间节点；
- 最终计算状态。

### 4.2 history 曲线

建议记录：

- 水平应力；
- 竖向应力；
- 墙体伺服速度；
- 平衡指标；
- 颗粒最大位移；
- 颗粒最大速度；
- 接触破坏数量；
- 采空区上方位移；
- zone 区域关键点应力或位移。

### 4.3 图像与截图

建议保存：

- 初始颗粒模型；
- 耦合区域示意；
- 开挖前状态；
- 开挖后典型阶段；
- 最终崩落形态；
- 远区应力云图；
- PFC 与 zone 边界局部放大图。

## 5. 建议保存命名规则

后续可采用更清晰的保存命名规则，例如：

```text
state_00_particles_generated
state_01_servo_equilibrated
state_02_contact_model_assigned
state_03_coupled_equilibrated
state_04_excavated
state_05_post_excavation_t001
state_06_post_excavation_t002
state_final
```

对于自动保存的中间状态，可采用：

```text
results/saved_states/post_excavation_%03d
```

## 6. 建议 FISH 变量命名

| 原始含义 | 建议变量名 | 说明 |
|---|---|---|
| 保存间隔 | `save_interval` | 每隔多少力学时间保存一次 |
| 上次保存时间 | `last_save_time` | 记录上一次保存的力学时间 |
| 当前保存编号 | `save_count` | 用于生成递增文件名 |
| 自动保存函数 | `auto_save_state` | 用于在 callback 中自动保存 |

## 7. 后续建议伪代码

后续可将自动保存逻辑整理为类似形式：

```text
[save_interval = 1.0]
[last_save_time = 0.0]
[save_count = 0]

def auto_save_state
    current_time = mech.time.total

    if current_time - last_save_time >= save_interval then
        filename = string.build("results/saved_states/post_excavation_%1", save_count)
        command
            model save @filename
        endcommand

        last_save_time = current_time
        save_count += 1
    endif
end

fish callback add @auto_save_state -0.5
```

具体语法需要根据 PFC2D 6.0 实际语法进一步确认。

## 8. 后续结果整理顺序

建议在流程打通后，按以下顺序完善结果输出：

1. 先保证关键阶段 `model save`；
2. 再添加 history 监测；
3. 再整理自动保存命名；
4. 再保存截图或云图；
5. 最后整理用于论文或汇报的结果图。
