# 情報数学 チートシート

情報数学は、情報工学・計算機科学で必要となる数学の基礎や、数学的に物事を扱う考え方を学ぶことを目的としています。連続的でなく離散的なもの、無限でなく有限なものを対象とする「離散数学」と密接に関連しています。

---

## 1. 論理 (Logic)

### 重要公式:

* **真理値表 (Truth Table):** 命題の真偽を示す表
    * 否定: `$\neg p$`
    * 論理積 (連言): `$p \land q$`
    * 論理和 (選言): `$p \lor q$`
    * 排他的論理和: `$p \oplus q$`
    * 含意: `$p \to q$`
    * 同値: `$p \leftrightarrow q$`
* **論理結合子の優先順位:** `[高] $\neg, \land, \lor, (\oplus, \to, \leftrightarrow)$ [低]`
* **命題の等価性（重要な恒真式）**:
    * 交換則: `$p \land q \equiv q \land p$`, `$p \lor q \equiv q \lor p$`
    * 結合則: `$p \land (q \land r) \equiv (p \land q) \land r$`, `$p \lor (q \lor r) \equiv (p \lor q) \land (p \lor r)$`
    * 分配則: `$p \land (q \lor r) \equiv (p \land q) \lor (p \land r)$`, `$p \lor (q \land r) \equiv (p \lor q) \land (p \lor r)$`
    * べき等則: `$p \lor p \equiv p$`, `$p \land p \equiv p$`
    * 吸収則: `$p \land (p \lor q) \equiv p$`, `$p \lor (p \land q) \equiv p$`
    * 単位則: `$\top \land p \equiv p$`, `$\bot \lor p \equiv p$`
    * 支配則: `$\bot \land p \equiv \bot$`, `$\top \lor p \equiv \top$`
    * 二重否定則: `$\neg (\neg p) \equiv p$`
    * 矛盾則: `$p \land \neg p \equiv \bot$`
    * 排中則: `$p \lor \neg p \equiv \top$`
    * ド・モルガンの法則: `$\neg (p \lor q) \equiv \neg p \land \neg q$`, `$\neg (p \land q) \equiv \neg p \lor \neg q$`
    * 含意の規則: `$p \to q \equiv \neg p \lor q$`
    * 同値の規則: `$(p \leftrightarrow q) \equiv (p \to q) \land (q \to p)$`
    * 対偶則: `$(p \to q) \equiv (\neg q \to \neg p)$`
* **限定子を含む否定**:
    * `$\neg \forall x P(x) \leftrightarrow \exists x \neg P(x)$`
    * `$\neg \exists x P(x) \leftrightarrow \forall x \neg P(x)$`
    * 全称限定子・存在限定子の交換則: `$\forall x \forall y P(x, y) \leftrightarrow \forall y \forall x P(x, y)$`, `$\exists x \exists y P(x, y) \leftrightarrow \exists y \exists x P(x, y)$`

### 主要アルゴリズム: なし

### 基本用語:

* **命題 (Proposition):** 「**真(true)**」または「**偽(false)**」のいずれか一方に定まる文。
* **真理値 (Truth Value):** 命題の値 (**T**: 真, **F**: 偽)。
* **論理結合子 (Logical Connective):** 命題をつないで新しい命題を作る記号（否定、論理積、論理和、排他的論理和、含意、同値）。
* **論理式 (Logical Formula):** 命題記号と論理結合子を再帰的に組み合わせたもの。
* **恒真式 (Tautology):** 常に真となる論理式。
* **充足可能 (Satisfiable):** 真となる場合がある論理式。
* **恒偽式 (Contradiction):** 常に偽となる論理式。
* **等価 (Equivalent) / 論理同値 (Logically Equivalent):** 論理式 A↔B が恒真であるとき、AとBは等価であるといい `$A \equiv B$` と表す。
* **命題関数 (Propositional Function) / 述語 (Predicate):** 変数を含む文で、変数を代入すると命題になるもの。
* **限定子 (Quantifier):** 命題関数がどの範囲で真となるかを表す表現 (全称限定子 `$\forall$`、存在限定子 `$\exists$`)。

---

## 2. 集合 (Sets)

### 重要公式:

* **集合が等しい条件:** `$A = B \text{ if and only if } A \subseteq B \land B \subseteq A$`
* **部分集合の定義:** `$A \subseteq B \text{ if and only if } \forall x (x \in A \to x \in B)$`
* **真部分集合の定義:** `$A \subset B \text{ if and only if } A \subseteq B \land \neg (B \subseteq A)$`
* **和集合の濃度:** `$|A \cup B| = |A| + |B| - |A \cap B|$` (有限集合の場合)
* **集合に関する恒等式**: (例として一部抜粋)
    * 単位則: `$A \cup \emptyset = A$`, `$A \cap U = A$`
    * ド・モルガンの法則: `$\overline{A \cup B} = \bar{A} \cap \bar{B}$`, `$\overline{A \cap B} = \bar{A} \cup \bar{B}$`

### 主要アルゴリズム: なし

### 基本用語:

* **集合 (Set):** 対象物の集まり。
* **空集合 (Empty Set):** 要素を持たない集合 (記号: `$\emptyset$` または `{}`)。
* **全体集合 (Universal Set):** 議論の対象となるすべての要素を含む集合 (記号: **U**)。
* **部分集合 (Subset):** 集合Aの任意の要素が集合Bの要素であるとき、AはBの部分集合である (`$A \subseteq B$`)。
* **濃度 (Cardinality):** 有限集合Sの異なる要素の個数 (記号: `$|S|$`)。
* **べき集合 (Power Set):** 集合Sの全ての部分集合の集合 (記号: `$\mathcal{P}(S)$` または `$2^S$`)。
* **直積 (Cartesian Product):** 集合AとBの全ての順序対`(a,b)`の集合 (記号: `$A \times B = \{(a,b) | a \in A \land b \in B\}$`)。
* **和集合 (Union):** AまたはBの要素を含む集合 (記号: `$A \cup B = \{x | x \in A \lor x \in B\}$`)。
* **共通部分 (Intersection):** AとBいずれにも含まれる要素からなる集合 (記号: `$A \cap B = \{x | x \in A \land x \in B\}$`)。
* **差集合 (Difference):** Aには含まれるがBには含まれない要素からなる集合 (記号: `$A - B = \{x | x \in A \land x \notin B\}$`)。
* **補集合 (Complement):** 全体集合Uに対する集合Aの補集合 (記号: `$\bar{A}$` または `$A^c$`, `$A^c = U - A$`)。

---

## 3. 関数 (Functions)

### 重要公式:

* **単射 (Injection) の定義:** `$\forall x, y \in A (x \neq y \to f(x) \neq f(y))$`。
* **全射 (Surjection) の定義:** `$\forall b \in B \exists a \in A (f(a) = b)$`。
* **関数の合成:** 関数 `$g: A \to B$` と `$f: B \to C$` に対して、合成関数 `$(f \circ g)(a) = f(g(a))$`。
* **逆関数:** `$f: A \to B$` が全単射ならば逆関数 `$f^{-1}: B \to A$` が存在する (`$f(a) = b \implies f^{-1}(b) = a$`)。

### 主要アルゴリズム: なし

### 基本用語:

* **関数 (Function) / 写像 (Mapping):** 定義域の各要素に終集合の要素をちょうど1つ割り当てるもの。
* **定義域 (Domain):** 関数fの入力となる集合A。
* **終集合 (Codomain):** 関数fの出力が含まれる集合B。
* **値域 (Range):** fによる定義域の全ての要素の像の集合。
* **単射 (Injection) / 1対1関数 (One-to-one function):** 定義域の異なる要素が終集合の異なる要素に写像される関数。
* **全射 (Surjection) / 上への関数 (Onto function):** 終集合の全ての要素が定義域のいずれかの要素の像である関数。
* **全単射 (Bijection) / 1対1対応 (One-to-one correspondence):** 単射かつ全射である関数。
* **単調増加 (Monotonically Increasing):** `$x < y \implies f(x) < f(y)$` を満たす関数。
* **単調減少 (Monotonically Decreasing):** `$x < y \implies f(x) > f(y)$` を満たす関数。
* **切捨て関数 (Flooring):** 実数xを超えない最大の整数を対応させる関数 (記号: `$\lfloor x \rfloor$`)。
* **切り上げ関数 (Ceiling):** 実数x以上の最小の整数を対応させる関数 (記号: `$\lceil x \rceil$`)。

---

## 4. 数列と可算集合 (Sequences and Countable Sets)

### 重要公式:

* **等差数列の一般項:** `$a_n = a_0 + nb$` (初項 `$a_0$`, 公差 `$b$`, `$n \ge 0$`)。
* **等比数列の一般項:** `$a_n = a_0 r^n$` (初項 `$a_0$`, 公比 `$r$`, `$n \ge 0$`)。
* **等比数列の和:** `$\sum_{k=0}^{n} ar^k = \frac{a r^{n+1} - a}{r-1}$` (ただし `$r \neq 1$`)。
* **等差数列の和:** `$\sum_{k=0}^{n} (a_0 + kb) = (n+1) \frac{2a_0 + nb}{2}$`。
* **和の公式:**
    * `$\sum_{k=1}^{n} k = \frac{n(n+1)}{2}$`
    * `$\sum_{k=1}^{n} k^2 = \frac{n(n+1)(2n+1)}{6}$`
    * `$\sum_{k=1}^{n} k^3 = \left(\frac{n(n+1)}{2}\right)^2$`

### 主要アルゴリズム: なし

### 基本用語:

* **数列 (Sequence):** 正の整数の集合からある集合Sへの関数。
* **一般項 (General Term):** 数列のn番目の要素 `$a_n$`。
* **等差数列 (Arithmetic Progression):** 隣り合う項の差が一定の数列。
* **等比数列 (Geometric Progression):** 隣り合う項の比が一定の数列。
* **可算集合 (Countable Set):** 有限集合であるか、または自然数の集合と1対1対応となる集合。

---

## 5. 数学的証明法と再帰 (Mathematical Proof Methods and Recursion)

### 重要公式:

* **推論規則 (Rules of Inference)**: (例として一部抜粋)
    * 構成的三段論法 (Modus Ponens): `$p, p \to q \implies q$`
    * 破壊的三段論法 (Modus Tollens): `$\neg q, p \to q \implies \neg p$`
    * 仮言三段論法 (Hypothetical Syllogism): `$p \to q, q \to r \implies p \to r$`

### 主要アルゴリズム:

* **再帰的定義 (Recursive Definition):** 対象を定義するために、それ自身を用いて定義すること。
    * **関数の再帰的定義:** 初期ステップと再帰ステップで関数値を定義。
    * **集合の再帰的定義:** 初期ステップで基本要素を指定し、再帰ステップで既知の要素から新しい要素を定義。

### 基本用語:

* **定理 (Theorem):** 真であることを証明できる命題。
* **証明 (Proof):** 命題の系列を用いて定理が真であることを示すこと。
* **推論規則 (Rules of Inference):** 結論が仮定の集合から論理的に導かれることを正当化するもの。
* **直接法 (Direct Proof):** `$p$` を真と仮定し、`$q$` が真であることを証明する `$p \to q$` の証明方法。
* **対偶法 (Proof by Contraposition):** `$\neg q$` を偽と仮定し、`$\neg p$` が偽であることを証明する `$p \to q$` の証明方法。
* **背理法 (Proof by Contradiction):** `$p$` を真かつ `$\neg q$` を偽と仮定し、矛盾する結論を導くことで元の命題が正しいことを証明する `$p \to q$` の証明方法。
* **数学的帰納法 (Mathematical Induction):** ある命題関数 `$P(n)$` がすべての正の整数 `$n$` で真であることを証明する方法 (基底段階と帰納段階)。
* **強数学的帰納法 (Strong Mathematical Induction):** P(k)だけでなく `P(1) \land \dots \land P(k)` が真であることを利用する帰納法。

---

## 6. 整数と整除 (Integers and Divisibility)

### 重要公式:

* **整除の定義:** `$a | b$` とは、`$b = ac$` となる整数 `$c$` が存在すること (`$a \neq 0$`)。
* **除法の定理:** 整数 `$a$`, 正整数 `$d$` に対して、`$a = dq + r$` となる `$q$` と `$r$` ($0 \le r < d$) が一意に決まる。
* **ユークリッドの互除法 (Euclidean Algorithm) の性質:** `$a = bq + r$` のとき、`$\text{gcd}(a, b) = \text{gcd}(b, r)$`。

### 主要アルゴリズム:

* **ユークリッドの互除法:** 2つの整数 `$a, b$` の最大公約数を求めるアルゴリズム。`$a \text{ mod } b = r$` とし、`$b$` を新たな `$a$`, `$r$` を新たな `$b$` として、$r=0$ になるまで繰り返す。$r=0$ となった時の $b$ がGCDである。

### 基本用語:

* **約数 (Divisor):** `$a | b$` のとき、$a$ を $b$ の約数という。
* **倍数 (Multiple):** `$a | b$` のとき、$b$ を $a$ の倍数という。
* **素数 (Prime):** 1より大きい正整数で、約数が1とそれ自身のみであるもの。
* **最大公約数 (Greatest Common Divisor, GCD):** `$d | a \land d | b$` となる最大の `$d$` (記号: `$\text{gcd}(a, b)$`)。
* **互いに素 (Relatively Prime) / 互いに素 (Coprime):** `$\text{gcd}(a, b) = 1$` となる整数 `$a, b$`。
* **最小公倍数 (Least Common Multiple, LCM):** `$a$` と `$b$` の両方が割り切る最小の正整数 (記号: `$\text{lcm}(a, b)$`)。

---

## 7. 関係 (Relations)

### 重要公式:

* **関係の定義:** 集合AとBの間の2項関係Rは `$A \times B$` の部分集合である (`$R \subseteq A \times B$`)。
* **2項関係の性質の定義:**
    * 反射的 (Reflexive): `$\forall x \in A (xRx)$`
    * 対称的 (Symmetric): `$\forall x, y \in A (xRy \to yRx)$`
    * 反対称的 (Anti-symmetric): `$\forall x, y \in A (xRy \land yRx \to x = y)$`
    * 推移的 (Transitive): `$\forall x, y, z \in A (xRy \land yRz \to xRz)$`
* **関係の演算:**
    * 逆関係 (Inverse Relation): `$R^{-1} = \{(y, x) | (x, y) \in R\}$`。
    * 合成関係 (Composition of Relations): `$R \circ S = \{(x, z) | \exists y ((x, y) \in R \land (y, z) \in S)\}$` (R: A→B, S: B→C)。

### 主要アルゴリズム: なし

### 基本用語:

* **2項関係 (Binary Relation):** 2つの集合の要素を結びつけるもの。
* **同値関係 (Equivalence Relation):** 反射的、対称的、推移的である関係。
* **同値類 (Equivalence Class):** 同値関係Rにおいて、aと同値関係にある要素の集合 `$[a] = \{b \in A | aRb\}$`。
* **商集合 (Quotient Set):** 集合Aと同値関係Rに対し、Rに関する同値類の集合 `$A/R = \{[a] | a \in A\}$`。
* **半順序関係 (Partial Order Relation):** 反射的、反対称的、推移的である関係。
* **半順序集合 (Partially Ordered Set):** 半順序関係Rが定義された集合S (記号: `$(S, R)$`)。
* **全順序集合 (Total Order Set):** 半順序集合Sの任意の2要素が比較可能であるとき。
* **ハッセ図 (Hasse Diagram):** 有限半順序集合を図示する方法。反射的関係や推移的関係の矢印は省略する。
* **最大元 (Maximum Element):** 任意のyに対し `$y \sqsubseteq x_0$` を満たす `$x_0$`が集合内に存在し、その$x_0$が最大元。
* **極大元 (Maximal Element):** `$x$`よりも大きい要素が存在しない `$x$`。
* **最小元 (Minimum Element):** 任意のyに対し `$x_0 \sqsubseteq y$` を満たす `$x_0$`が集合内に存在し、その$x_0$が最小元。
* **極小元 (Minimal Element):** `$x$`よりも小さい要素が存在しない `$x$`。
* **上界 (Upper Bound):** 部分集合Aの任意の元aに対し、`$a \sqsubseteq x_0$` となる `$x_0$`。
* **上限 (Supremum, Least Upper Bound):** 上界集合の最小元 (記号: `$\text{sup} A$`)。
* **下界 (Lower Bound):** 部分集合Aの任意の元aに対し、`$y_0 \sqsubseteq a$` となる `$y_0$`。
* **下限 (Infimum, Greatest Lower Bound):** 下界集合の最大元 (記号: `$\text{inf} A$`)。
* **束 (Lattice):** 半順序集合 `$A$` の任意の2元が上限と下限をともに持つとき。
* **P閉包 (P-closure):** 関係Rに対して、Rを含む最小の性質Pを満たす関係R'。

---

## 8. 代数 (Algebra)

### 重要公式:

* **演算の性質:**
    * 結合則 (Associative Law): `$\forall x, y, z \in A (x \circ (y \circ z) = (x \circ y) \circ z)$`
    * 交換則 (Commutative Law): `$\forall x, y \in A (x \circ y = y \circ x)$`
* **束の性質 (代数として):** (上記結合則、交換則に加えて)
    * べき等則: `$a \lor a = a$`, `$a \land a = a$`
    * 吸収則: `$(a \lor b) \land b = b$`, `$(a \land b) \lor b = b$`
* **分配律 (Distributive Law):**
    * `$a \lor (b \land c) = (a \lor b) \land (a \lor c)$`
    * `$a \land (b \lor c) = (a \land b) \lor (a \lor c)$`
* **ブール束の性質 (ブール代数):**
    * 単位元: `$a \lor 0 = a$`, `$a \land 1 = a$`
    * 補元: `$a \lor \bar{a} = 1$`, `$a \land \bar{a} = 0$`
    * ド・モルガンの法則: `$\overline{a \lor b} = \bar{a} \land \bar{b}$`, `$\overline{a \land b} = \bar{a} \lor \bar{b}$`
* **準同型写像の定義:** `$f: A \to B$` が `$f(x \circ y) = f(x) * f(y)$` を満たす。

### 主要アルゴリズム: なし

### 基本用語:

* **2項演算 (Binary Operation):** 集合Aの2つの元に対し、Aの1つの元を与えるもの。
* **閉じている (Closed):** 集合Aの2つの要素に対する演算の結果が、必ずその集合Aにあること。
* **代数 (Algebra):** 集合とその上に定義された演算を組にしたもの。
* **可換 (Commutative):** 交換則を満たす代数。
* **単位元 (Identity Element):** `$e \in A$` で、`$\forall x \in A (e \circ x = x \circ e = x)$` を満たすもの。
* **逆元 (Inverse Element):** 単位元 `$e$` がある代数において、`$x \circ y = y \circ x = e$` を満たす `$y$` を `$x$` の逆元という。
* **半群 (Semigroup):** 結合法則を満たす代数。
* **モノイド (Monoid):** 結合法則を満たし、単位元をもつ代数。
* **群 (Group):** 結合法則を満たし、単位元を持ち、すべての元が逆元をもつ代数。
* **可換群 (Abelian Group):** 交換則も満たす群。
* **分配束 (Distributive Lattice):** 束の性質に加えて分配則を満たす束。
* **ブール束 (Boolean Lattice) / ブール代数 (Boolean Algebra):** 相補的な分配束。
* **準同型写像 (Homomorphism):** 2つの代数間で演算を保存する関数。
* **同型写像 (Isomorphism):** 全単射な準同型写像。