# ch2 命题逻辑的等值和推理演算

## 1. 等值定理

给定两个命题公式 $A$ 和 $B$，设 $P_1$，$P_2$，$\dots$，$P_n$ 为出现于 $A$ 和 $B$ 中的所有命题变项，则公式 $A$ 和 $B$ 共有 $2^n$ 个解释。若在任一解释下，公式 $A$ 和 $B$ 的真值都想同，则称 $A$ 和 $B$ 是等值的、或称等价，记作 $A = B$ 或 $A \Leftrightarrow B$。

【**等值定理**】设 $A$，$B$ 为两个命题公式，$A = B$ 的**充要条件**是 $A \leftrightarrow B$ 为一个重言式。

等值定理的实用性之一：若证明两个公式等值，只要证明由这两个公式构成的双条件式是重言式。

等值关系满足等价关系的三个性质：

- 自反性：$A = A$
- 对称性：若 $A = B$，则 $B = A$
- 传递性：若 $A = B$，$B = C$，则 $A = C$

两个重要结论：

1. 一个命题（原命题）与它的逆否命题等值：$P\to Q = \lnot Q \to \lnot P$
2. 一个命题的逆命题与它的否命题等值：$Q\to P = \lnot P \to \lnot Q$

## 2. 等值公式

若 $X$ 是合式公式 $A$ 的一部分，且 $X$ 本身也是一个合式公式，则称 $X$ 为公式 $A$ 的子公式。

【**置换规则**】设 $X$ 为公式 $A$ 的子公式，用与 $X$ 等值的公式 $Y$ 将 $A$ 中的 $X$ 施以代换，称为置换。

置换后公式 $A$ 化为公式 $B$，置换规则的性质保证公式 $A$ 与公式 $B$ 等值，即 $A = B$。且当 $A$ 是重言式时，置换后的公式 $B$ 也是重言式。此为**等值定律**。

【**定理**】设 $\phi(A)$ 是含命题公式 $A$ 的命题公式，$\phi(B)$ 是用命题公式 $B$ 置换了 $\phi(A)$ 中的 $A$ 之后得到的命题公式。如果 $A = B$，则 $\phi(A) = \phi(B)$。

1. 双重否定律：$\lnot \lnot P = P$

2. 结合律：

    - $(P \lor Q) \lor R = P \lor (Q \lor R)$

    - $(P \land Q) \land R = P \land (Q \land R)$

    - $(P \leftrightarrow Q) \leftrightarrow R = P \leftrightarrow (Q \leftrightarrow R)$

    - <p style="color: red;">$(P \to Q) \to R \ne P \to (Q \to R)$</p>

3. 交换律：

    - $P \lor Q = Q \lor P$

    - $P \land Q = Q \land R$

    - $P \leftrightarrow Q = Q \leftrightarrow P$

    - <p style="color: red;">$P \to Q \ne Q \to P$</p>

4. 分配律：

    - $P \lor (Q \land R) = (P \lor Q)\land (P \lor R)$

    - $P\land (Q \lor R) = (P \land Q)\lor (P \land R)$

    - $P \to (Q \to R) = (P \to Q) \to (P \to R)$

    - <p style="color: red;">$P \leftrightarrow (Q \leftrightarrow R) \ne (P \leftrightarrow Q) \leftrightarrow (P \leftrightarrow R)$</p>

5. 幂等律（恒等律）

    - $P \lor P = P$
    - $P \land P = P$
    - $P \to P = 1$
    - $P \leftrightarrow P = 1$

6. 吸收律

    - $P \lor (P \land Q) = P$
    - $P \land (P \lor Q) = P$

7. 德摩根律

    - $\lnot (P \lor Q) = \lnot P \land \lnot Q$
    - $\lnot (P \land Q) = \lnot P \lor \lnot Q$

    对蕴涵词、双条件词作否定有：

    - $\lnot (P \to Q) = P \land \lnot Q$
    - $\lnot (P \leftrightarrow Q) = \lnot P \leftrightarrow Q = P \leftrightarrow \lnot Q = (\lnot P \land Q)\lor (P \land \lnot Q)$

8. 同一律

    - $P \lor 0 = P$
    - $P \land 1 = P$
    - $1 \to P = P$
    - $1 \leftrightarrow P = P$
    - $P \to 0 = \lnot P$
    - $0 \leftrightarrow P = \lnot P$

9. 零律

    - $P \lor 1 = 1$
    - $P \land 0 = 0$
    - $P \to 1 = 1$
    - $0 \to P = 1$

10. 补余律

    - $P \lor \lnot P = 1$
    - $P \land \lnot P = 0$
    - $P \to \lnot P = \lnot P$
    - $\lnot P \to P = P$
    - $P \leftrightarrow \lnot P = 0$

**常用等值公式**：

- 蕴涵等值式：$P \to Q = \lnot P \lor Q$
- 前提合取合并：$P \to (Q \to R) = (P \land Q) \to R$
- 等价等值式：$P \leftrightarrow Q = (P \to Q) \land (Q \to P)$
- 假言易位：$P \to Q = \lnot Q \to \lnot P$
- 等价否定等值式：$P \leftrightarrow Q = \lnot P \leftrightarrow \lnot Q$
- 归谬论：$(P \to Q) \land (P \to \lnot Q) = \lnot P$
- 前提析取合并：$(P \to R) \land (Q \to R) = (P \lor Q) \to R$
- 前提交换：$P \to (Q \to R) = Q \to (P \to R)$
- $P \leftrightarrow Q = (P \land Q) \lor (\lnot P \land \lnot Q)$
- $P \leftrightarrow Q = (P \lor \lnot Q) \land (\lnot P \lor Q)$

## 3. 命题关系与真值表的关系



## 4. 联结词的完备集

## 5. 对偶式

## 6. 范式

## 7. 推理形式与基本推理公式

## 8. 推理演算

## 9. 归纳推理