---
type: concept
tags: [常微分方程, ODE, 速通]
sources: []
created: 2026-07-05
updated: 2026-07-05
---

# ⚡ ODE 速通 — 4 个核心题型

> **用户情况**：完全没学过常微分方程，30 分钟速通 4 类必考题型

---

## 🎯 题型 ① 可分离变量

**形式**：$\dfrac{dy}{dx} = f(x) \cdot g(y)$

**步骤**：
1. 分离变量：$\dfrac{dy}{g(y)} = f(x)\, dx$
2. 两边积分：$\int \dfrac{dy}{g(y)} = \int f(x)\, dx$
3. 整理成 $F(y) = G(x) + C$

**例**：$\dfrac{dy}{dx} = xy$
- 分离：$\dfrac{dy}{y} = x\, dx$
- 积分：$\ln|y| = \dfrac{x^2}{2} + C$
- 解：$y = C e^{x^2/2}$

---

## 🎯 题型 ② 一阶线性

**形式**：$\dfrac{dy}{dx} + p(x) \cdot y = q(x)$

### 🔑 套公式（必背！）

$$\boxed{y = e^{-\int p(x)\, dx}\left[\int q(x) e^{\int p(x)\, dx}\, dx + C\right]}$$

**例**：$y' + 2xy = x$
- $p = 2x$，$\int p\, dx = x^2$
- $e^{-\int p\, dx} = e^{-x^2}$
- $e^{\int p\, dx} = e^{x^2}$
- $y = e^{-x^2}\left[\int x e^{x^2}\, dx + C\right] = e^{-x^2}\left[\frac{1}{2}e^{x^2} + C\right] = \frac{1}{2} + C e^{-x^2}$

### 变体：齐次形式 $\dfrac{dy}{dx} = f(y/x)$

> 用代换 $u = y/x$ → $\dfrac{dy}{dx} = u + x\dfrac{du}{dx}$ → 化为可分离

---

## 🎯 题型 ③ 二阶常系数**齐次**线性

**形式**：$y'' + py' + qy = 0$

### 🔑 特征方程法（必背！）

**步骤**：
1. 写特征方程：$r^2 + pr + q = 0$
2. 求根 $r_1, r_2$
3. 按根的情况写通解

| 特征根 | 通解形式 |
|--------|---------|
| 两不等实根 $r_1 \neq r_2$ | $y = C_1 e^{r_1 x} + C_2 e^{r_2 x}$ |
| 两相等实根 $r_1 = r_2 = r$ | $y = (C_1 + C_2 x) e^{rx}$ |
| 共轭复根 $r = \alpha \pm \beta i$ | $y = e^{\alpha x}(C_1 \cos\beta x + C_2 \sin\beta x)$ |

**例**：$y'' - 3y' + 2y = 0$
- 特征方程：$r^2 - 3r + 2 = 0 \implies (r-1)(r-2) = 0$
- $r_1 = 1, r_2 = 2$（不等实根）
- 通解：$y = C_1 e^x + C_2 e^{2x}$

**例**：$y'' - 2y' + y = 0$
- $r^2 - 2r + 1 = 0 \implies (r-1)^2 = 0$
- $r_1 = r_2 = 1$（相等实根）
- 通解：$y = (C_1 + C_2 x) e^x$

**例**：$y'' + y = 0$
- $r^2 + 1 = 0 \implies r = \pm i$
- 共轭复根：$\alpha = 0, \beta = 1$
- 通解：$y = C_1 \cos x + C_2 \sin x$

---

## 🎯 题型 ④ 二阶常系数**非齐次**线性

**形式**：$y'' + py' + qy = f(x)$

### 🔑 通解 = 齐次通解 + 非齐次特解

**步骤**：
1. 解齐次方程 → 齐次通解 $\bar{y}$
2. 用**待定系数法**求特解 $y^*$
3. 总通解 $y = \bar{y} + y^*$

### 特解的设定（按 $f(x)$ 形式）

| $f(x)$ 形式 | 特解形式 | 说明 |
|-------------|----------|------|
| $P_n(x) e^{\lambda x}$ | $y^* = x^k \cdot Q_n(x) e^{\lambda x}$ | $\lambda$ 是特征根 → $k = $ 重数 |
| $P_n(x) e^{\alpha x}\cos\beta x$ | $y^* = x^k \cdot e^{\alpha x}[R_n^{(1)}(x)\cos\beta x + R_n^{(2)}(x)\sin\beta x]$ | $\alpha + \beta i$ 是特征根 → $k = $ 重数 |
| $P_n(x) e^{\alpha x}\sin\beta x$ | 同上 | 同上 |

**例**：$y'' - 3y' + 2y = 2e^x$
- 齐次通解（上一节例）：$\bar{y} = C_1 e^x + C_2 e^{2x}$
- $\lambda = 1$ 是特征根（重数 $k = 1$）
- 设特解 $y^* = Ax \cdot e^x$
- 代入求 $A$：
  - $y^{*\prime} = A e^x + Ax e^x = A(1+x) e^x$
  - $y^{*\prime\prime} = A e^x + A(1+x) e^x = A(2+x) e^x$
  - 代入：$A(2+x) e^x - 3A(1+x) e^x + 2Ax e^x = A[(2+x) - 3(1+x) + 2x] e^x = A[-1] e^x = -Ae^x$
  - 令 $-Ae^x = 2e^x \implies A = -2$
- 特解 $y^* = -2x e^x$
- 通解：$y = C_1 e^x + C_2 e^{2x} - 2x e^x$

---

## ⚠️ 易错点

1. **可分离**前必须**先判断是否能分离**（不是所有一阶都分得开）
2. **一阶线性公式**中的 $e^{\int p\, dx}$ 千万别忘
3. **特征根相等**时容易漏 $C_2 x$ 项
4. **非齐次特解**：$\lambda$ 是特征根时，必须**乘以 $x^k$**（否则消不掉齐次项）

## 💡 做题套路（30 秒判断题型）

> 看到 $y'' + py' + qy = f(x)$ → **特征根法**
> 看到 $y' + p(x)y = q(x)$ → **套一阶线性公式**
> 看到 $\dfrac{dy}{dx} = f(x) \cdot g(y)$ → **分离变量**
> 看到 $\dfrac{dy}{dx} = f(y/x)$ → **齐次代换** $u = y/x$

---

*Last updated: 2026-07-05*