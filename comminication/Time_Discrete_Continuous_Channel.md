# Time Discrete Continuous Channel

[TOC]

## Define

A Time-Discrete Continuous Channel is a communication channel. This type of channel is often used in digital communication where signals are sampled at discrete times but can take continuous amplitude values.

- Time is discrete, signals are transmitted at distinct time steps.
- Signal values are continuous, the transmitted and received symbols can take any real value within a range.

## Property

### Additive Noise Channel

$$
Y_i = X_i + N_i
$$

- $\mathbb P(y|x) = p_Z(y - x)$
- $h(Y|X) = h(Z)$

$$
C = \max_{p(x)} h(Y) - h(Z)
$$

### Additive white Gaussian noise channel

$$
Y_i = X_i + N_i\\ N_i \sim N(0, σ^2)
$$

Additive white Gaussian noise is a basic noise model used to mimic the effect of many random processes that occur in nature, which satisfy specific characteristics:

  - **Additive**: The noise is added to the signal, rather than multiplying or distorting it in other ways.
  - **White**: The noise has a constant power spectral density across all frequencies, meaning it affects all frequencies equally.
  - **Gaussian**: The noise follows a Gaussian (normal) distribution with mean 0 and variance $\sigma^2$.


$$
C = B \log\left(1 + \frac{P}{N}\right)
$$

Channel capacity of AWGN channel, defining the upper limit on data transmission rate for a given bandwidth and SNR.

- $X_i$ is the transmitted signal at discrete-time event index $i$.
- $N_i \sim \mathcal{N}(0, \sigma^2)$ is the additive white Gaussian noise
- $C$: is the channel capacity (bits per second, bps)
- $B$: is the channel bandwidth (Hertz, Hz)
- $P$ is the average power of the transmitted signal (Watts, W).
- $N = \sigma^2$ is the noise power (Watts, W).
- $\frac{P}{\sigma^2}$ is the signal-to-noise ratio (SNR).

### Parallel Additive Gauss Noise Channel

$$
C = \frac{1}{2} \sum_{i=1}^N \log \left(1+\frac{P_i}{σ_i^2}\right)
$$

The total channel capacity for parallel additive Gauss noise channel is the sum of individual channel capacities.

$$
\begin{align*}
P_i &= \max\left\{ 0, \frac{1}{ν^*} - σ_i^2 \right\}  \\
\sum P_i &= P
\end{align*} \tag{optimal power allocation}
$$

Optimal power allocation strategy to achieve channel capacity. Channels with too high noise ($σ_i^2$ large) may get zero power allocation.

- $P_i$ is the power allocated to sub-channel $i$
- $σ_i^2$ is the noise variance.
- $\frac{1}{ν^*}$: water level, determined by the total available power $P$.

## Appendix

### Proof of Additive Noise Channel

$$
\begin{align*}
y &= x + z  \\
C &= \max I(X;Y)  \tag{定义}  \\
&= \max ( h(Y) - h(Y|X) )  \\
&= \max ( h(Y) - h(X+Z|X) )  \tag{代入}  \\
&= \max ( h(Y) - h(Z|X) )  \\
&= \max ( h(Y) - h(Z) )  \tag{$X,Z$统计独立}
\end{align*}
$$

### Proof of Additive white Gaussian noise
$$
\begin{align*}
y &= x + z  \quad z \sim N(0, σ^2)  \tag{信道}\\
C &= \max ( H(Y) - H(Z) )  \tag{性质}\\
  &= \max ( H(Y) - \frac{1}{2} \log(2 π e σ^2) )  \tag{Gauss分布微分熵}
\end{align*}
$$

$\because$ 限功率最大熵: 平均功率受限的随机变量, 当$Y$为Gauss分布时, $H(Y)$ 取得最大值.
$$
\begin{align*}
C &= \frac{1}{2} \log(2 π e (P + σ^2)) - \frac{1}{2} \log(2 π e σ^2)  \tag{限功率最大熵}\\
  &= \frac{1}{2} \log\left(1 + \frac{P}{N}\right)  \tag{$σ^2 = N$ 噪声功率}\\
  &= B \log\left(1 + \frac{P}{N}\right)  \tag{2B速率采样}
\end{align*}
$$

### Proof of Parallel Additive Gauss Noise Channel

原问题形式   (解凸优化) 
$$
\begin{align*}
\max \quad& C = \sum C_i = \frac{1}{2} \sum \log\left(1 + \frac{P_i}{σ_i^2}\right)  \\
s.t. \quad& P_i ≥ 0  \\
  & \sum P_i^* = P
\end{align*}
$$

  将问题简化, 令$\frac{P_i}{P}$归一化写作$x_i$, $σ_i^2$写作$α_i$, 

$$
\begin{align*}
\min \quad& - \sum \log(α_i + x_i)  \\
s.t. \quad& x ⪰ 0  \\
  & 1^T x = 1
\end{align*}
$$

Lagrange 函数,
$$
L(x, λ, ν) = - \sum \log (α_i + x_i) + \sum λ_i (- x_i) + ν (1^T x - 1)
$$

KKT 条件,
$$
\begin{align*}
x^* &⪰ 0  \\
1^T x^* &= 1  \\
λ &⪰ 0  \\
λ_i x_i &= 0  \\
\frac{∂ L}{∂ x_i} |_{x_i = x_i^*} &= - \frac{1}{α_i + x_i^*} - λ_i^* + ν^* = 0
\end{align*}
$$

第5式得$λ_i = ν^* - \frac{1}{α_i + x_i^*}$, 回代消去$λ$, 
$$
\begin{align*}
x^* &⪰ 0  \\
1^T x^* &= 1  \\
ν^* &≥ \frac{1}{α_i + x_i^*}  \\
\left(ν^* - \frac{1}{α_i + x_i^*}\right) x_i^* &= 0
\end{align*}
$$

(1) 当$x_i^* ≠ 0$时, 即$x_i^* > 0$
$$
\begin{align*}
  \Rightarrow \quad& ν^* = \frac{1}{α_i + x_i^*}  \\
  \Rightarrow \quad& x_i^* = \frac{1}{ν^*} - α_i > 0  \\
  \Rightarrow \quad& ν^* < \frac{1}{α_i}
\end{align*}
$$

(2) 当$x_i^* = 0$时, 
$$
\Rightarrow \quad ν^* ≥ \frac{1}{α_i}
$$

(综上)
$$
\begin{align*}
  x_i &= \max\left\{ 0, \frac{1}{ν^*} - α_i \right\}\\
  1^T x^* &= 1
\end{align*}
$$

结果称为注水方法, $α_i$ 为第i区域的池底高度, 向整个区域注水, 注水总量为$\sum x_i^* = 1$, 则水面高度为$\frac{1}{ν} = α_i + x_i^*$, 每个区域的水深$x_i^*$即是其最优解.