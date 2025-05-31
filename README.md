<a name="top"></a>

# 高考数列题与线性代数解法（2019–2024）

本项目整理了中国大陆（全国卷与部分地方卷）和法国高考（Baccalauréat）中关于数列的典型问题（2019–2024），并结合线性代数的视角，如向量、矩阵递推、特征值等方法进行统一求解与分析。适合竞赛学生、大学先修课程、以及高考扩展研究使用。

> **点击跳转到英文版本：** [English Version](#english-version)

---

## 目录

- [一、题目汇总（中法高考 2019–2024）](#overview_ch)  
- [二、典型题解析](#examples_ch)  
  - [例题 1（中国全国卷 II 理科，2019）](#example1_ch)  
  - [例题 2（中国新高考 I 卷，2021）](#example2_ch)  
  - [例题 3（法国 Baccalauréat S，2023）](#example3_ch)  
- [三、线性代数方法简述](#methods_ch)  
- [四、致谢与参考资料](#refs_ch)  

---

<a name="overview_ch"></a>
## 一、题目汇总（中法高考 2019–2024）

以下为各年度中国大陆和法国高考中部分典型与“数列”相关的题目示例。表格中仅列出核心信息，完整题目详见项目中的 LaTeX 文档。

| 年份 | 国家/地区   | 卷别             | 类型        | 概要内容                                                                 |
|------|--------------|------------------|-------------|--------------------------------------------------------------------------|
| 2019 | 中国大陆     | 全国卷 II（理科） | 二元递推    | 数列 \(\{a_n\},\{b_n\}\) 满足 \(a_{n+1}=a_n+b_n,\;b_{n+1}=a_n+b_n\)       |
| 2019 | 法国         | Bac S（海外）    | 仿射递推    | \(p_{n+1}=0.8\,p_n+0.3\,(1-p_n)\)，概率背景                               |
| 2020 | 中国大陆     | 全国卷 II（理科） | 等比递推    | 等比数列 \(a_n\)，已知 \(a_1+a_2=12,\;a_1a_2=32\)                          |
| 2020 | 法国         | Bac S（海外）    | 非恒定系数  | \(u_{n+1}=(n+1)\,u_n-1\)，数列发散或收敛                                  |
| 2021 | 中国大陆     | 全国卷 I（理科）  | 求和递推    | \(2\,S_n=n\,a_n\)，求数列通项及和                                          |
| 2021 | 法国         | Bac S（Métropole）| 非线性递推  | \(u_{n+1}=\tfrac{1+u_n}{3+u_n}\)，辅助变量转等比                           |
| 2022 | 中国大陆     | 新高考 I 卷      | 非线性迭代  | \(u_{n+1}=\tfrac{1+u_n}{1+2u_n}\)，收敛极限                               |
| 2022 | 法国         | Bac 全国卷       | 可变系数    | \(u_{n+1}=\tfrac{n^2+1}{\,n+1\,}u_n\)，对数累加解                           |
| 2023 | 中国大陆     | 新高考 I 卷      | 等差构造    | “可分数列”问题，删除两项后将剩余元素分组成等差                              |
| 2023 | 法国         | Bac 全国乙卷     | 分段定义    | 等差数列与分段数列 \(b_n\) 的前 \(n\) 项和比较                               |
| 2024 | 中国大陆     | 全国卷 I（理科）  | 等差分组    | 划分 \(1,2,\dots,4m+2\)，删除两项后将剩余 \(4m\) 个数分组成等差               |
| 2024 | 法国         | Bac 全国卷       | 仿射递推    | 与 2019 类似的概率递推 \(p_{n+1}=0.4\,p_n+0.4\)                               |

---

<a name="examples_ch"></a>
## 二、典型题解析

<a name="example1_ch"></a>
### 例题 1（中国全国卷 II 理科，2019）

**题目**：已知数列 \(\{a_n\}\) 与 \(\{b_n\}\) 满足  
\[
\begin{cases}
a_1 = 1,\quad b_1 = 0,\\[4pt]
a_{n+1} = a_n + b_n,\\[4pt]
b_{n+1} = a_n + b_n,\quad n \ge 1.
\end{cases}
\]  
1. 证明：\(\{\,a_n + b_n\,\}\) 为等比数列，\(\{\,a_n - b_n\,\}\) 为等差数列；  
2. 求 \(\{a_n\}\) 与 \(\{b_n\}\) 的通项公式。  

#### 解法概览

1. **向量化、矩阵表示**  
   令 \(\displaystyle \mathbf{v}_n = \begin{pmatrix}a_n\\[4pt] b_n\end{pmatrix}.\)  
   由题意可写成  
   \[
   \mathbf{v}_{n+1} 
   = \begin{pmatrix}1 & 1\\[4pt] 1 & 1\end{pmatrix}\,\mathbf{v}_n, 
   \quad 
   \mathbf{v}_1 = \begin{pmatrix}1\\[4pt]0\end{pmatrix}.
   \]
   记 \(M = \begin{pmatrix}1 & 1\\[4pt] 1 & 1\end{pmatrix}\)，则 \(\mathbf{v}_n = M^{\,n-1}\,\mathbf{v}_1\)。

2. **求特征值与特征向量**  
   求解  
   \[
   \det\bigl(M - \lambda I\bigr) 
   = (1-\lambda)^2 - 1 = 0 
   \;\Longrightarrow\; \lambda_1 = 2,\;\lambda_2 = 0.
   \]  
   - 对应 \(\lambda_1 = 2\) 的特征向量满足 \((M - 2I)\mathbf{u} = 0\)，得 \(\mathbf{u}_1 = \begin{pmatrix}1\\[4pt]1\end{pmatrix}.\)  
   - 对应 \(\lambda_2 = 0\) 的特征向量满足 \(M\mathbf{u} = \mathbf{0}\)，得 \(\mathbf{u}_2 = \begin{pmatrix}1\\[4pt]-1\end{pmatrix}.\)

3. **将初始向量展开到特征向量基底**  
   \[
   \mathbf{v}_1 
   = \begin{pmatrix}1\\[4pt]0\end{pmatrix} 
   = \alpha\,\mathbf{u}_1 + \beta\,\mathbf{u}_2 
   = \alpha \begin{pmatrix}1\\[4pt]1\end{pmatrix} + \beta \begin{pmatrix}1\\[4pt]-1\end{pmatrix} 
   = \begin{pmatrix}\alpha + \beta\\[4pt] \alpha - \beta\end{pmatrix}.
   \]
   由 \(\alpha + \beta = 1\) 且 \(\alpha - \beta = 0\)，解得 \(\alpha = \beta = \tfrac12\)。

4. **计算 \(\mathbf{v}_n = M^{\,n-1}\,\mathbf{v}_1\)**  
   由于 \(M\,\mathbf{u}_1 = 2\,\mathbf{u}_1\) 且 \(M\,\mathbf{u}_2 = 0\)，可得当 \(n \ge 2\) 时：  
   \[
   \mathbf{v}_n 
   = M^{\,n-1}\,\mathbf{v}_1 
   = \tfrac12\,2^{\,n-1}\,\mathbf{u}_1 \;+\; \tfrac12\,0^{\,n-1}\,\mathbf{u}_2 
   = 2^{\,n-2}\begin{pmatrix}1\\[4pt]1\end{pmatrix}.
   \]
   故对 \(n \ge 2\)：  
   \[
   a_n = 2^{\,n-2}, 
   \quad 
   b_n = 2^{\,n-2}.
   \]
   结合 \(n=1\) 时 \(a_1=1,\;b_1=0\)，即可完整描述。

5. **验证等比与等差**  
   - 当 \(n\ge2\) 时：  
     \[
     a_n + b_n = 2^{\,n-2} + 2^{\,n-2} = 2^{\,n-1},
     \]  
     这是首项 \(2\)、公比 \(2\) 的等比数列。  
   - 当 \(n\ge2\) 时：  
     \[
     a_n - b_n = 2^{\,n-2} - 2^{\,n-2} = 0,
     \]  
     这是恒为 \(0\) 的等差数列（公差 \(0\)），结合 \(n=1\) 时 \(a_1 - b_1 = 1\)，也可认为是从 \(n=2\) 开始常数项的等差数列。

---

<a name="example2_ch"></a>
### 例题 2（中国新高考 I 卷，2021）

**题目**：数列 \(\{a_n\}\) 满足：  
\[
a_2 = 1,\quad 2\,S_n = n\,a_n,\quad n\in\mathbb{N}^+,\quad S_n = \sum_{k=1}^n a_k.
\]  
(1) 求 \(\{a_n\}\) 的通项公式；  
(2) 若存在 \(k>1\) 使得 \(S_k=100\)，求最小正整数 \(k\)。

#### 解法概览

1. **化简递推**  
   由 \(2\,S_n = n\,a_n\) 与 \(2\,S_{n-1} = (n-1)\,a_{n-1}\)，相减得：  
   \[
   2\,(S_n - S_{n-1}) = n\,a_n - (n-1)\,a_{n-1} 
   \;\Longrightarrow\; 
   2\,a_n = n\,a_n - (n-1)\,a_{n-1}.
   \]  
   因此：
   \[
   (n-2)\,a_n = (n-1)\,a_{n-1},\quad n\ge2.
   \]
   已知 \(a_2 = 1\)，且 \(2\,S_1 = a_1 \Rightarrow a_1 = 0\)。

2. **迭代展开**  
   对 \(n \ge 3\)：  
   \[
   a_n = \frac{\,n-1\,}{\,n-2\,}\,a_{n-1}, 
   \quad a_2 = 1,\;a_1 = 0.
   \]
   由归纳可知：
   \[
   a_n = \frac{\,n-1\,}{2},\quad n \ge 2, 
   \quad a_1 = 0.
   \]

3. **求 \(S_n\) 及 \(k\)**  
   当 \(n \ge 2\)：  
   \[
   S_n 
   = a_1 + \sum_{k=2}^n \frac{k-1}{2} 
   = 0 + \frac12 \sum_{j=1}^{\,n-1} j 
   = \frac{\,n(n-1)\,}{4}.
   \]
   若 \(S_k = 100\)，则解  
   \[
   \frac{k(k-1)}{4} = 100 
   \;\Longrightarrow\; k^2 - k - 400 = 0.
   \]
   正根 \(k = \frac{1 + \sqrt{1601}}{2} \approx 20.506\)。  
   故最小正整数 \(k = 21\)。

---

<a name="example3_ch"></a>
### 例题 3（法国 Baccalauréat S，2023）

**题目**：某城市每天感染人数 \(u_n\) 和潜伏期人数 \(v_n\) 满足：  
\[
\begin{cases}
u_{n+1} = 0.8\,u_n + 0.2\,v_n, \\[4pt]
v_{n+1} = 0.1\,u_n + 0.9\,v_n,
\end{cases}
\quad n \ge 0,\quad (u_0,v_0)\;\text{已知}.
\]  
1. 写出 \(\mathbf{x}_{n+1} = A\,\mathbf{x}_n\) 的矩阵 \(A\)；  
2. 求 \(\{u_n\},\{v_n\}\) 的通项以及长期极限。

#### 解法概览

1. **向量矩阵表示**  
   令  
   \[
   \mathbf{x}_n = \begin{pmatrix}u_n\\[4pt]v_n\end{pmatrix}, 
   \quad 
   A = \begin{pmatrix}0.8 & 0.2\\[4pt]0.1 & 0.9\end{pmatrix}.
   \]
   则  
   \(\mathbf{x}_{n+1} = A\,\mathbf{x}_n\)。

2. **特征值与特征向量**  
   计算特征方程：  
   \[
   \det(A - \lambda I) 
   = (0.8 - \lambda)(0.9 - \lambda) - 0.02 = 0 
   \;\Longrightarrow\; \lambda_1 = 1,\;\lambda_2 = 0.7.
   \]
   分别求解对应特征向量 \(\mathbf{u}_1\)、\(\mathbf{u}_2\)。

3. **初始向量分解**  
   设 \(\mathbf{x}_0 = \alpha\,\mathbf{u}_1 + \beta\,\mathbf{u}_2\)。  
   则  
   \[
   \mathbf{x}_n = A^n\,\mathbf{x}_0 
   = \alpha\,1^n\,\mathbf{u}_1 + \beta\,(0.7)^n\,\mathbf{u}_2 
   = \alpha\,\mathbf{u}_1 + \beta\,(0.7)^n\,\mathbf{u}_2.
   \]
   当 \(n \to \infty\)，\((0.7)^n \to 0\)，故 \(\mathbf{x}_n \to \alpha\,\mathbf{u}_1\)。  
   因此长期极限由 \(\lambda=1\) 对应的特征向量 \(\mathbf{u}_1\) 决定。

---

<a name="methods_ch"></a>
## 三、线性代数方法简述

| 方法                            | 适用情形                             | 简要说明                                                                                                        |
|---------------------------------|--------------------------------------|------------------------------------------------------------------------------------------------------------------|
| 向量迭代法（矩阵形式）          | 多变量线性递推系统                    | 将递推系统表示为 \(\mathbf{x}_{n+1} = A\,\mathbf{x}_n\)，通过对 \(A\) 的特征值/特征向量分析获得通项与极限。     |
| 矩阵幂建模                        | 一变量常量或仿射递推                    | 将标量递推 \(a_{n+1} = p\,a_n + q\) 扩展为 \(\begin{pmatrix}a_{n+1}\\1\end{pmatrix} = \begin{pmatrix}p & q\\0 & 1\end{pmatrix} \begin{pmatrix}a_n\\1\end{pmatrix}\)。 |
| 特征值分解                       | 研究长期行为（平稳状态）                | 对 \(A\) 进行对角化或分解，写作 \(\mathbf{x}_n = P\,D^n\,P^{-1}\,\mathbf{x}_0\)，当 \(\lvert \lambda \rvert < 1\) 时 \(\lambda^n \to 0\)。    |
| 辅助变量法（非线性 → 线性）      | 非线性或仿射递推，可化为等比递推          | 定义 \(v_n = f(u_n)\) 使 \(v_{n+1} = \lambda\,v_n\) （等比数列），再反推 \(u_n\)。                                     |
| 对数累加法                        | 变量系数乘积递推（如 \(u_{n+1} = c_n\,u_n\)） | 令 \(w_n = \ln(u_n)\)，则 \(w_{n+1} - w_n = \ln(c_n)\)，对 1 至 \(n-1\) 求和得到 \(w_n\)，再取指数还原 \(u_n\)。   |

---

<a name="refs_ch"></a>
## 四、致谢与参考资料

- 中国教育部考试中心（全国高考试题）  
- 法国教育部 Baccalauréat 官方资源  
- 各年度真题解析及教学扩展资料  
- 高中阶段线性代数与数列教材  

📂 本项目同时提供 LaTeX 源文件 `sequence_problems.tex`，详见项目仓库根目录。

---

<hr/>

<a name="english-version"></a>

# II. Advanced Analysis of Examination Sequences via Linear Algebra (2019–2024)

This project compiles representative sequence-related problems from Mainland China’s Gaokao (national and select provincial papers) and the French Baccalauréat (2019–2024). We adopt a linear algebra perspective—employing vectors, matrix recurrences, eigenvalues, and so forth—to present unified solutions and analyses. This material is suitable for competition preparation, university extension courses, or in-depth pre-university study.

> **Click to return to Chinese version:** [中文版本](#top)

---

## Table of Contents

- [1. Problem Overview (China & France 2019–2024)](#overview_en)  
- [2. Detailed Worked Examples](#examples_en)  
  - [Example 1 (China Gaokao, National Paper II, 2019)](#example1_en)  
  - [Example 2 (China New Gaokao I Paper, 2021)](#example2_en)  
  - [Example 3 (France Baccalauréat S, 2023)](#example3_en)  
- [3. Summary of Linear Algebra Techniques](#methods_en)  
- [4. Acknowledgements and References](#refs_en)

---

<a name="overview_en"></a>
## 1. Problem Overview (China & France 2019–2024)

Below is a selection of typical “sequence” problems from Gaokao (China) and the French Baccalauréat. Only core information is shown; for full problem statements, please refer to the TeX source provided in this repository.

| Year | Country/Region | Paper/Series                    | Type                    | Brief Description                                                           |
|------|----------------|---------------------------------|-------------------------|-----------------------------------------------------------------------------|
| 2019 | China          | National Paper II (Science)     | Two-variable recurrence | Sequences \(\{a_n\},\{b_n\}\) satisfying \(a_{n+1} = a_n + b_n,\; b_{n+1} = a_n + b_n\) |
| 2019 | France         | Baccalauréat S (Overseas)       | Affine recurrence       | \(p_{n+1} = 0.8\,p_n + 0.3\,(1-p_n)\); probability context                    |
| 2020 | China          | National Paper II (Science)     | Geometric progression   | Geometric sequence \(a_n\); given \(a_1 + a_2 = 12,\; a_1 a_2 = 32\)         |
| 2020 | France         | Baccalauréat S (Overseas)       | Non-constant coefficient | \(u_{n+1} = (n+1)\,u_n - 1\); divergence/convergence analysis                 |
| 2021 | China          | National Paper I (Science)      | Summation recurrence    | \(2\,S_n = n\,a_n\); find general term and sums                              |
| 2021 | France         | Baccalauréat S (Métropole)      | Nonlinear recurrence    | \(u_{n+1} = \frac{1 + u_n}{3 + u_n}\); use an auxiliary variable to reduce to GP |
| 2022 | China          | New Gaokao I Paper              | Nonlinear iteration     | \(u_{n+1} = \frac{1 + u_n}{1 + 2\,u_n}\); convergence and limit              |
| 2022 | France         | National Baccalauréat           | Variable coefficient    | \(u_{n+1} = \frac{n^2 + 1}{\,n + 1\,} u_n\); log-sum technique               |
| 2023 | China          | New Gaokao I Paper              | Arithmetic grouping     | “Divisible sequence” problem: remove two terms and group the rest into APs   |
| 2023 | France         | National Baccalauréat (Series S)| Piecewise-defined sequence | Compare sums of an AP and a piecewise-defined sequence                        |
| 2024 | China          | National Paper I (Science)      | AP partitioning         | Partition \(1,2,\dots,4m+2\) after removing two terms into AP quartets         |
| 2024 | France         | National Baccalauréat           | Affine recurrence       | Similar to 2019: \(p_{n+1} = 0.4\,p_n + 0.4\) in a probabilistic setting         |

---

<a name="examples_en"></a>
## 2. Detailed Worked Examples

<a name="example1_en"></a>
### Example 1 (China Gaokao, National Paper II, 2019)

**Problem Statement**  
Define two sequences \(\{a_n\}\) and \(\{b_n\}\) by:
\[
\begin{cases}
a_1 = 1, \quad b_1 = 0, \\[4pt]
a_{n+1} = a_n + b_n, \\[4pt]
b_{n+1} = a_n + b_n, \quad n \ge 1.
\end{cases}
\]
1. Prove that \(\{\,a_n + b_n\,\}\) is a geometric progression and \(\{\,a_n - b_n\,\}\) is an arithmetic progression.  
2. Find the general term of \(\{a_n\}\) and \(\{b_n\}\).

#### Solution Outline

1. **Vectorisation and Matrix Representation**  
   Let 
   \[
   \mathbf{v}_n = \begin{pmatrix}a_n \\[4pt] b_n\end{pmatrix}.
   \]
   The recurrence can be written as
   \[
   \mathbf{v}_{n+1} 
   = \begin{pmatrix}1 & 1 \\[4pt] 1 & 1\end{pmatrix}\mathbf{v}_n, 
   \quad \mathbf{v}_1 = \begin{pmatrix}1\\[4pt]0\end{pmatrix}.
   \]
   Denote 
   \[
   M = \begin{pmatrix}1 & 1 \\[4pt] 1 & 1\end{pmatrix}, \quad 
   \mathbf{v}_n = M^{\,n-1}\,\mathbf{v}_1.
   \]

2. **Eigenvalues and Eigenvectors**  
   Compute the characteristic polynomial:
   \[
   \det(M - \lambda I) 
   = (1-\lambda)^2 - 1 = 0 
   \;\Longrightarrow\; \lambda_1 = 2, \;\lambda_2 = 0.
   \]
   - For \(\lambda_1 = 2\), solve \((M - 2I)\mathbf{u} = 0\), yielding \(\mathbf{u}_1 = \begin{pmatrix}1 \\[4pt] 1\end{pmatrix}.\)  
   - For \(\lambda_2 = 0\), solve \(M\mathbf{u} = \mathbf{0}\), yielding \(\mathbf{u}_2 = \begin{pmatrix}1 \\[4pt] -1\end{pmatrix}.\)

3. **Express the Initial Vector in the Eigenbasis**  
   \[
   \mathbf{v}_1 
   = \begin{pmatrix}1 \\[4pt] 0\end{pmatrix} 
   = \alpha\,\mathbf{u}_1 + \beta\,\mathbf{u}_2 
   = \alpha \begin{pmatrix}1 \\[4pt] 1\end{pmatrix} 
   + \beta \begin{pmatrix}1 \\[4pt] -1\end{pmatrix} 
   = \begin{pmatrix}\alpha + \beta \\[4pt] \alpha - \beta\end{pmatrix}.
   \]
   From \(\alpha + \beta = 1\) and \(\alpha - \beta = 0\), solve \(\alpha = \beta = \tfrac12\).

4. **Compute \(\mathbf{v}_n = M^{\,n-1}\,\mathbf{v}_1\)**  
   Since \(M\,\mathbf{u}_1 = 2\,\mathbf{u}_1\) and \(M\,\mathbf{u}_2 = 0\), for \(n \ge 2\):
   \[
   \mathbf{v}_n 
   = M^{\,n-1}\,\mathbf{v}_1 
   = \tfrac12\,2^{\,n-1}\,\mathbf{u}_1 + \tfrac12\,0^{\,n-1}\,\mathbf{u}_2 
   = 2^{\,n-2}\,\begin{pmatrix}1 \\[4pt] 1\end{pmatrix}.
   \]
   Hence,
   \[
   a_n = 2^{\,n-2}, \quad b_n = 2^{\,n-2}, \quad n \ge 2,
   \]
   together with \((a_1,b_1)=(1,0)\).

5. **Verify “Arithmetic” and “Geometric” Properties**  
   - For \(n \ge 2\):
     \[
     a_n + b_n = 2^{\,n-2} + 2^{\,n-2} = 2^{\,n-1},
     \]
     which is a geometric progression with ratio \(2\).  
   - For \(n \ge 2\):
     \[
     a_n - b_n = 2^{\,n-2} - 2^{\,n-2} = 0,
     \]
     a constant sequence (arithmetic progression with common difference \(0\)).

---

<a name="example2_en"></a>
### Example 2 (China New Gaokao I Paper, 2021)

**Problem Statement**  
Let \(\{a_n\}\) be a sequence whose partial sums are \(S_n = a_1 + a_2 + \cdots + a_n\). It is given that
\[
a_2 = 1, \quad 2\,S_n = n\,a_n, \quad n \in \mathbb{N}^+.
\]
1. Determine the general term \(a_n\).  
2. If there exists \(k > 1\) such that \(S_k = 100\), find the smallest such positive integer \(k\).

#### Solution Outline

1. **Convert to a Single-Variable Recurrence**  
   From \(2\,S_n = n\,a_n\) and \(2\,S_{n-1} = (n-1)\,a_{n-1}\), subtract:
   \[
   2\,(S_n - S_{n-1}) = n\,a_n - (n-1)\,a_{n-1} 
   \;\Longrightarrow\; 
   2\,a_n = n\,a_n - (n-1)\,a_{n-1}.
   \]
   Hence,
   \[
   (n-2)\,a_n = (n-1)\,a_{n-1}, \quad n \ge 2.
   \]
   Given \(a_2 = 1\) and \(2\,S_1 = a_1 \Rightarrow a_1 = 0\).

2. **Iterate to Find the Closed Form**  
   For \(n \ge 3\):
   \[
   a_n = \frac{\,n-1\,}{\,n-2\,}\,a_{n-1}, 
   \quad a_2 = 1, \; a_1 = 0.
   \]
   By induction:
   \[
   a_n = \frac{\,n-1\,}{2}, \quad n \ge 2, \quad a_1 = 0.
   \]

3. **Compute \(S_n\) and Solve for \(k\)**  
   For \(n \ge 2\):
   \[
   S_n = \sum_{i=1}^n a_i 
       = 0 + \sum_{k=2}^n \frac{k-1}{2} 
       = \frac12 \sum_{j=1}^{\,n-1} j 
       = \frac{\,n(n-1)\,}{4}.
   \]
   To have \(S_k = 100\), solve
   \[
   \frac{k(k-1)}{4} = 100 
   \;\Longrightarrow\; k^2 - k - 400 = 0.
   \]
   The positive root is \(k = \frac{1 + \sqrt{1601}}{2} \approx 20.506\).  
   Hence the smallest integer is \(k = 21\).

---

<a name="example3_en"></a>
### Example 3 (France Baccalauréat S, 2023)

**Problem Statement**  
A city’s daily infection numbers \(u_n\) and latent infection numbers \(v_n\) satisfy:
\[
\begin{cases}
u_{n+1} = 0.8\,u_n + 0.2\,v_n, \\[4pt]
v_{n+1} = 0.1\,u_n + 0.9\,v_n,
\end{cases}
\quad n \ge 0, \quad (u_0, v_0)\ \text{given.}
\]
1. Write the system as \(\mathbf{x}_{n+1} = A\,\mathbf{x}_n\).  
2. Find the general terms of \(\{u_n\}\) and \(\{v_n\}\), and determine the long-term limit.

#### Solution Outline

1. **Form the Vector–Matrix Equation**  
   Let
   \[
   \mathbf{x}_n = \begin{pmatrix}u_n \\[4pt] v_n\end{pmatrix}, 
   \quad 
   A = \begin{pmatrix}0.8 & 0.2\\[4pt]0.1 & 0.9\end{pmatrix}.
   \]
   Then \(\mathbf{x}_{n+1} = A\,\mathbf{x}_n\).

2. **Eigenvalues and Eigenvectors**  
   Compute
   \[
   \det(A - \lambda I) = (0.8 - \lambda)(0.9 - \lambda) - 0.02 = 0 
   \;\Longrightarrow\; \lambda_1 = 1,\;\lambda_2 = 0.7.
   \]
   Find eigenvectors \(\mathbf{u}_1\) for \(\lambda_1 = 1\) and \(\mathbf{u}_2\) for \(\lambda_2 = 0.7\).

3. **Express the Initial Vector in the Eigenbasis**  
   Let \(\mathbf{x}_0 = \alpha\,\mathbf{u}_1 + \beta\,\mathbf{u}_2\).  
   Then
   \[
   \mathbf{x}_n = A^n\,\mathbf{x}_0 
                = \alpha\,1^n\,\mathbf{u}_1 + \beta\,(0.7)^n\,\mathbf{u}_2 
                = \alpha\,\mathbf{u}_1 + \beta\,(0.7)^n\,\mathbf{u}_2.
   \]
   As \(n \to \infty\), \((0.7)^n \to 0\), so \(\mathbf{x}_n \to \alpha\,\mathbf{u}_1\).  
   Therefore, the long-term equilibrium is given by the eigenvector corresponding to eigenvalue 1.

---

<a name="methods_en"></a>
## 3. Summary of Linear Algebra Techniques

| Technique                              | Applicable Situation                                    | Brief Description                                                                                                                                    |
|----------------------------------------|---------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| Vector Recurrence (Matrix Form)        | Multi-variable linear recurrence systems                | Represent \(\mathbf{x}_{n+1} = A\,\mathbf{x}_n\). Analyse eigenvalues/eigenvectors of \(A\) to find explicit solutions and long-term behaviour.         |
| Matrix Power Modelling                 | Single-variable constant or affine recurrence           | Convert a scalar recurrence \(a_{n+1} = p\,a_n + q\) into \(\begin{pmatrix}a_{n+1}\\1\end{pmatrix} = \begin{pmatrix}p & q\\0 & 1\end{pmatrix} \begin{pmatrix}a_n\\1\end{pmatrix}\).  |
| Eigenvalue Decomposition               | Study of long-term behaviour (steady states)            | Diagonalise or triangularise \(A\) to write \(\mathbf{x}_n = P\,D^n\,P^{-1}\,\mathbf{x}_0\). When \(\lvert \lambda \rvert < 1\), \(\lambda^n \to 0\).         |
| Auxiliary Sequence (Nonlinear → Linear)  | Nonlinear or affine recurrences reducible to GP          | Define \(v_n = f(u_n)\) so that \(v_{n+1} = \lambda\,v_n\) (a geometric progression), then invert \(f\) to recover \(u_n\).                              |
| Logarithmic Summation Method           | Variable-coefficient multiplicative recurrence (e.g. \(u_{n+1} = c_n\,u_n\)) | Let \(w_n = \ln(u_n)\), so \(w_{n+1} - w_n = \ln(c_n)\). Summing telescopically yields \(w_n\), and exponentiating recovers \(u_n\).                          |

---

<a name="refs_en"></a>
## 4. Acknowledgements and References

- National Examinations Authority of China, Gaokao Papers  
- French Ministry of Education, Baccalauréat Official Resources  
- Various official solution guides and supplementary materials  
- High school textbooks on linear algebra and sequence analysis  

📂 The complete LaTeX source file `sequence_problems.tex` is provided for detailed statements and solutions.

---

