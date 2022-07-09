# PID算法

> PID原理：https://www.cnblogs.com/foxclever/p/8902029.html
>
> PID控制算法C语言实现：https://blog.csdn.net/mcueno/article/details/83317851

## PID原理

P:Proportion 比例

I:Integral 积分

D:Derivative 导数

![](https://img-blog.csdnimg.cn/20190705215313291.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyOTkyMDg0,size_16,color_FFFFFF,t_70)

PID公式：

误差 = 给定值-测量值
$$
e(t) = in(t) - out(t)
$$
则pid控制器的输出信号
$$
u(t)=K_p(e(t)+\frac{1}{T_t}\int_{0}^{t}e(t)dt+T_D\frac{de(t)}{dt})
$$

- Kp比例系数
- Tt积分时间常数
- TD微分时间常数
- u(t)PID控制器输出信号
- e(t)误差

### 各项作用：

比例项：若只有比例项，则系统存在稳态误差（steady-state error）

积分项：消除静态误差

微分项：根据偏差的变化趋势实现超前调节，提高响应速度

### 离散化：

**位置型PID算法：**

假设系统采样周期为$$T$$，检查第$$k$$个采样周期，
$$
U(k)=K_p(e(k)+\frac{T}{T_I}\sum e(k)+\frac{T_D}{T}(e(k)-e(k-1)))
$$
也可以记为
$$
U(k) = K_pe(k)+K_i\sum e(k)+K_d(e(k)-e(k-1))
$$
**增量型PID算法：**

根据
$$
\Delta U(k) = U(k) - U(k-1)
$$
有
$$
\Delta U(k)=K_p(e(k)-e(k-1))+K_ie(k)+K_d(e(k)-2e(k-1)+e(k-2))
$$
则
$$
U(k) = U(k-1) + \Delta U(k)
$$

## C语言实现

