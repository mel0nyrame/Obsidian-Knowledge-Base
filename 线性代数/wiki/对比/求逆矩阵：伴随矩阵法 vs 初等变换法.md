---
type: comparison
tags: [逆矩阵, 伴随矩阵, 初等变换, 代数余子式]
sources: [raw/素材/第二章矩阵.md, raw/素材/第三章矩阵的初等变换与线性方程组.md]
created: 2026-05-19
updated: 2026-05-20
---

## 对比主题

对于 $n$ 阶可逆方阵 $A$（满足 $|A| \neq 0$），存在两种求逆矩阵的方法：第二章的**伴随矩阵法**和第三章的**初等变换法**。两者理论基础不同，适用场景各异。

## 核心对比

| 维度 | 伴随矩阵法 | 初等变换法 |
|------|-----------|-----------|
| **章节** | 第二章 2.4 | 第三章 3.2 |
| **公式** | $A^{-1} = \frac{1}{\vert A \vert} A^*$ | $(A \mid E) \xrightarrow{\text{行变换}} (E \mid A^{-1})$ |
| **理论基础** | 代数余子式 + 行列式 | 初等矩阵 + 矩阵等价 |
| **操作方式** | 计算 $n^2$ 个代数余子式，拼成 $A^*$，再除以 $|A|$ | 对增广矩阵只做行变换，直到左边变成 $E$ |
| **核心计算量** | $n^2$ 个 $(n-1)$ 阶行列式 | 约 $n^3$ 次乘加运算 |
| **低阶（$n \leq 2$）** | ⚡ 极快（$A^{-1} = \frac{1}{ad-bc}\begin{pmatrix} d & -b \\ -c & a \end{pmatrix}$） | 也能用 |
| **高阶（$n \geq 3$）** | 🐢 极其繁琐 | ⚡ 标准方法 |
| **理论价值** | 给出逆矩阵的**显式表达式**，用于理论证明 | 给出**算法**，用于实际计算 |

## 与相关概念的联系

- [[代数余子式]] — 伴随矩阵法的核心计算单元
- [[初等变换]] — 初等变换法的操作基础
- 两种方法都依赖 $|A| \neq 0$（可逆的充要条件）

## 具体示例

### 方法一：伴随矩阵法 — $A^{-1} = \dfrac{A^*}{\vert A\vert}$

**例 1：二阶（秒出）**

求 $A = \begin{pmatrix} 3 & 5 \\ -2 & 4 \end{pmatrix}$ 的逆矩阵。

① 算行列式：$|A| = 3 \times 4 - 5 \times (-2) = 22$

② 二阶伴随口诀（主对角线互换、副对角线变号）：

$A^* = \begin{pmatrix} 4 & -5 \\ 2 & 3 \end{pmatrix}$

③ 套公式：$A^{-1} = \dfrac{1}{22}\begin{pmatrix} 4 & -5 \\ 2 & 3 \end{pmatrix}$

验证：$AA^{-1} = \frac{1}{22}\begin{pmatrix} 3 & 5 \\ -2 & 4 \end{pmatrix}\begin{pmatrix} 4 & -5 \\ 2 & 3 \end{pmatrix} = \frac{1}{22}\begin{pmatrix} 22 & 0 \\ 0 & 22 \end{pmatrix} = E$ ✅

---

**例 2：三阶（伴随法开始吃力）**

求 $A = \begin{pmatrix} 1 & 2 & 3 \\ 0 & 1 & 4 \\ 0 & 0 & 1 \end{pmatrix}$ 的逆矩阵。

① $|A| = 1$（上三角，对角线乘积）

② 算 9 个代数余子式：

第一行：$A_{11}=1, A_{12}=0, A_{13}=0$
第二行：$A_{21}=-2, A_{22}=1, A_{23}=0$
第三行：$A_{31}=5, A_{32}=-4, A_{33}=1$

③ 转置得 $A^* = \begin{pmatrix} 1 & -2 & 5 \\ 0 & 1 & -4 \\ 0 & 0 & 1 \end{pmatrix}$

④ $A^{-1} = A^*$（因为 $|A|=1$）✅

> 三阶伴随法需要算 9 个二阶行列式。三阶及以上推荐用初等变换法。

---

### 方法二：初等变换法 — $(A \mid E) \xrightarrow{\text{行变换}} (E \mid A^{-1})$

**例 3：二阶（感受流程）**

求 $A = \begin{pmatrix} 1 & 2 \\ 3 & 4 \end{pmatrix}$ 的逆矩阵。

$$
(A \mid E) = \left(\begin{array}{cc|cc} 1 & 2 & 1 & 0 \\ 3 & 4 & 0 & 1 \end{array}\right)
\xrightarrow{r_2 - 3r_1}
\left(\begin{array}{cc|cc} 1 & 2 & 1 & 0 \\ 0 & -2 & -3 & 1 \end{array}\right)
$$

$$
\xrightarrow{-\frac{1}{2}r_2}
\left(\begin{array}{cc|cc} 1 & 2 & 1 & 0 \\ 0 & 1 & \frac{3}{2} & -\frac{1}{2} \end{array}\right)
\xrightarrow{r_1 - 2r_2}
\left(\begin{array}{cc|cc} 1 & 0 & -2 & 1 \\ 0 & 1 & \frac{3}{2} & -\frac{1}{2} \end{array}\right)
$$

$A^{-1} = \begin{pmatrix} -2 & 1 \\ \frac{3}{2} & -\frac{1}{2} \end{pmatrix}$

---

**例 4：三阶上三角（与例 2 同一矩阵，不同方法）**

求 $A = \begin{pmatrix} 1 & 2 & 3 \\ 0 & 1 & 4 \\ 0 & 0 & 1 \end{pmatrix}$ 的逆矩阵。

$$
(A \mid E) = \left(\begin{array}{ccc|ccc}
1 & 2 & 3 & 1 & 0 & 0 \\
0 & 1 & 4 & 0 & 1 & 0 \\
0 & 0 & 1 & 0 & 0 & 1
\end{array}\right)
$$

自下而上消元：

$$
\xrightarrow{\substack{r_1-3r_3 \\ r_2-4r_3}}
\left(\begin{array}{ccc|ccc}
1 & 2 & 0 & 1 & 0 & -3 \\
0 & 1 & 0 & 0 & 1 & -4 \\
0 & 0 & 1 & 0 & 0 & 1
\end{array}\right)
\xrightarrow{r_1-2r_2}
\left(\begin{array}{ccc|ccc}
1 & 0 & 0 & 1 & -2 & 5 \\
0 & 1 & 0 & 0 & 1 & -4 \\
0 & 0 & 1 & 0 & 0 & 1
\end{array}\right)
$$

$A^{-1} = \begin{pmatrix} 1 & -2 & 5 \\ 0 & 1 & -4 \\ 0 & 0 & 1 \end{pmatrix}$，与例 2 结果一致 ✅

---

**例 5：三阶一般矩阵（初等变换法的主场）**

求 $A = \begin{pmatrix} 1 & 0 & 2 \\ 2 & -1 & 3 \\ 4 & 1 & 8 \end{pmatrix}$ 的逆矩阵。

$$
(A \mid E) = \left(\begin{array}{ccc|ccc}
1 & 0 & 2 & 1 & 0 & 0 \\
2 & -1 & 3 & 0 & 1 & 0 \\
4 & 1 & 8 & 0 & 0 & 1
\end{array}\right)
\xrightarrow{\substack{r_2-2r_1 \\ r_3-4r_1}}
\left(\begin{array}{ccc|ccc}
1 & 0 & 2 & 1 & 0 & 0 \\
0 & -1 & -1 & -2 & 1 & 0 \\
0 & 1 & 0 & -4 & 0 & 1
\end{array}\right)
$$

$$
\xrightarrow{-r_2}
\left(\begin{array}{ccc|ccc}
1 & 0 & 2 & 1 & 0 & 0 \\
0 & 1 & 1 & 2 & -1 & 0 \\
0 & 1 & 0 & -4 & 0 & 1
\end{array}\right)
\xrightarrow{r_3-r_2}
\left(\begin{array}{ccc|ccc}
1 & 0 & 2 & 1 & 0 & 0 \\
0 & 1 & 1 & 2 & -1 & 0 \\
0 & 0 & -1 & -6 & 1 & 1
\end{array}\right)
$$

$$
\xrightarrow{-r_3}
\left(\begin{array}{ccc|ccc}
1 & 0 & 2 & 1 & 0 & 0 \\
0 & 1 & 1 & 2 & -1 & 0 \\
0 & 0 & 1 & 6 & -1 & -1
\end{array}\right)
\xrightarrow{\substack{r_1-2r_3 \\ r_2-r_3}}
\left(\begin{array}{ccc|ccc}
1 & 0 & 0 & -11 & 2 & 2 \\
0 & 1 & 0 & -4 & 0 & 1 \\
0 & 0 & 1 & 6 & -1 & -1
\end{array}\right)
$$

$A^{-1} = \begin{pmatrix} -11 & 2 & 2 \\ -4 & 0 & 1 \\ 6 & -1 & -1 \end{pmatrix}$

## 结论

| 场景 | 推荐方法 |
|------|---------|
| **手算 $n=2$** | 伴随矩阵法（套公式秒出） |
| **手算 $n \geq 3$** | 初等变换法（步骤最清晰） |
| **理论证明** | 伴随矩阵法（有显式表达式 $A^{-1}|A| = A^*$） |
| **数值计算 / 编程** | 初等变换法（高斯-约当消元 $O(n^3)$） |

> 两种方法**互补而非对立**：伴随矩阵法让你**理解**逆矩阵的结构，初等变换法让你**高效地算出**逆矩阵。

## 参见

- [[代数余子式]] — 伴随矩阵的核心组成
- [[初等变换]] — 初等变换法的操作基础
- [[wiki/来源/2026-05-19 第二章 矩阵]] — 伴随矩阵法原始内容
- [[wiki/来源/2026-05-19 第三章 矩阵的初等变换与线性方程组]] — 初等变换法原始内容
