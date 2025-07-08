# コンピュータアーキテクチャ チートシート

---

## 1. 基本性能評価

### 重要公式

* **ICのコスト (IC Cost)**
  * [cite_start]ダイ1個あたりのコスト: $Cost\ per\ die = \frac{Cost\ per\ wafer}{Dies\ per\ wafer \times Yield}$ [cite: 400]
  * [cite_start]ウェーハあたりのダイ数: $Dies\ per\ wafer \approx \frac{Wafer\ area}{Die\ area}$ [cite: 401]
  * [cite_start]歩留まり: $Yield = \frac{1}{(1 + (Defects\ per\ area \times Die\ area / 2))^2}$ [cite: 403]

* **性能と実行時間 (Performance and Execution Time)**
  * [cite_start]相対性能: $性能 = \frac{1}{実行時間}$ [cite: 454]
  * [cite_start]CPU実行時間 (CPU Time): $CPU時間 = CPUクロックサイクル数 \times クロックサイクル時間 = \frac{CPUクロックサイクル数}{クロック周波数}$ [cite: 483, 484]
  * [cite_start]CPUクロックサイクル数: $CPUクロックサイクル数 = プログラム中の実行命令数 \times CPI$ [cite: 494-497]
  * [cite_start]総合的なCPU時間: $CPU実行時間 = \frac{プログラム中の実行命令数 \times CPI}{クロック周波数}$ [cite: 496, 497]

* **消費電力 (Power)**
  * [cite_start]CMOS ICの消費電力: $Power = Capacitive\ load \times Voltage^2 \times Frequency$ [cite: 628]

### 基本用語

* [cite_start]**CPI (Cycles Per Instruction)**: 命令あたりの平均クロックサイクル数 [cite: 498]。
* [cite_start]**IPC (Instructions Per Cycle)**: 1サイクルあたりの実行命令数。CPIの逆数 [cite: 507]。
* [cite_start]**応答時間 (Response Time)**: タスクを完了させるまでに必要な合計時間 [cite: 447]。
* [cite_start]**スループット (Throughput)**: 単位時間あたりに終了した作業量 [cite: 451]。
* [cite_start]**Amdahlの法則 (Amdahl's Law)**: システムのある部分を改善しても、その改善が全体の性能向上に寄与する割合には限界があるという法則 [cite: 734, 738]。
* [cite_start]**電力の壁 (Power Wall)**: 消費電力と冷却の問題により、クロック周波数の向上が限界に達している状況 [cite: 593, 639-641]。

---

## 2. MIPS命令セットアーキテクチャ (ISA)

### 命令フォーマット

* [cite_start]**R形式 (R-type)**: 主にレジスタ間の算術・論理演算に使用 [cite: 1011]。
  * [cite_start]フィールド: `op | rs | rt | rd | shamt | funct` [cite: 1019-1032]
* [cite_start]**I形式 (I-type)**: 即値を含む演算、ロード/ストア、条件分岐に使用 [cite: 1037]。
  * [cite_start]フィールド: `op | rs | rt | address/immediate` [cite: 1038]
* [cite_start]**J形式 (J-type)**: 無条件ジャンプに使用 [cite: 1448, 1732]。
  * [cite_start]フィールド: `op | target address` [cite: 1732]

### アドレッシングモード

* [cite_start]**即値アドレッシング (Immediate Addressing)**: オペランドが命令内に含まれる定数 [cite: 1442, 1459]。
* [cite_start]**レジスタアドレッシング (Register Addressing)**: オペランドがレジスタ [cite: 1457]。
* [cite_start]**ベース相対アドレッシング (Base-relative Addressing)**: レジスタの値と命令内の定数（オフセット）の和でメモリアドレスを指定 [cite: 1457]。
* [cite_start]**PC相対アドレッシング (PC-relative Addressing)**: プログラムカウンタ(PC)からの相対アドレスで分岐先を指定 [cite: 1449, 1450]。
* [cite_start]**疑似直接アドレッシング (Pseudo-direct Addressing)**: ジャンプ命令で、PCの上位4ビットと命令内の26ビットアドレスを結合してジャンプ先を指定 [cite: 1459, 1455]。

### 主要命令とレジスタ規約

* **主要命令**:
  * [cite_start]算術演算: `add`, `sub`, `addi` [cite: 860, 1348]
  * [cite_start]データ転送: `lw` (ロード), `sw` (ストア) [cite: 992]
  * [cite_start]条件分岐: `beq` (等しいなら分岐), `bne` (等しくないなら分岐) [cite: 1349]
  * [cite_start]比較: `slt` (より小さいならセット), `slti` (即値で比較) [cite: 1359]
  * [cite_start]無条件分岐: `j` (ジャンプ), `jal` (ジャンプしてリンク), `jr` (レジスタへジャンプ) [cite: 1354, 1360, 1395]
* **レジスタ規約**:
  * [cite_start]`$a0`–`$a3`: 引数用 [cite: 1394]
  * [cite_start]`$v0`–`$v1`: 戻り値用 [cite: 1394]
  * [cite_start]`$t0`–`$t9`: 一時変数用（呼び出し側で待避責任） [cite: 1402]
  * [cite_start]`$s0`–`$s7`: 保存用変数（被呼び出し側で待避責任） [cite: 1402]
  * [cite_start]`$sp`: スタックポインタ [cite: 1396]
  * [cite_start]`$ra`: 戻りアドレス [cite: 1394]
  * [cite_start]`$fp`: フレームポインタ [cite: 1407]
  * [cite_start]`$gp`: グローバルポインタ [cite: 1408]

---

## 3. 算術演算

### 重要公式

* **IEEE 754 浮動小数点数表現**:
  * [cite_start]単精度: $(-1)^S \times (1 + Fraction) \times 2^{(Exponent - 127)}$ [cite: 1562]
  * [cite_start]倍精度: $(-1)^S \times (1 + Fraction) \times 2^{(Exponent - 1023)}$ [cite: 1567]

### 主要アルゴリズム

* [cite_start]**乗算アルゴリズム (最終版)** [cite: 214-217]:
  1. 64ビットの積レジスタの下位32ビットに乗数をセット。被乗数レジスタを用意。
  2. 積レジスタの最下位ビット(LSB)をチェックする。
  3. もしLSBが1なら、被乗数を積レジスタの上位半分に加算する。
  4. 積レジスタ全体を1ビット右にシフトする。
  5. この処理を32回繰り返す。最終的な積が64ビットレジスタに得られる。

* [cite_start]**除算アルゴリズム (改良版)** [cite: 1544-1546]:
  1. 64ビットの剰余レジスタの右半分に被除数をセット。除数レジスタを用意。
  2. 剰余レジスタを1ビット左にシフトする。
  3. 剰余レジスタの上位半分から除数を引く。
  4. 結果が0以上なら、剰余レジスタを1ビット左にシフトし、LSBに1をセットする。
  5. 結果が負なら、除数を足して値を戻し、剰余レジスタを1ビット左にシフトしてLSBに0をセットする。
  6. この処理を32回繰り返す。商は剰余レジスタの下位半分に、剰余は上位半分に残る。

### 基本用語

* [cite_start]**2の補数 (2's Complement)**: 負数を表現する方法。ビットを反転して1を加えることで得られる [cite: 1150, 1240]。
* [cite_start]**符号拡張 (Sign Extension)**: 短いビット長の符号付き数を長いビット長に変換する際、符号ビットを上位ビットにコピーすること (`lb` と `lbu` の違い) [cite: 1179, 1188, 1189]。
* [cite_start]**IEEE 754**: 浮動小数点数の標準規格 [cite: 1562]。
* [cite_start]**仮数部 (Fraction/Mantissa)**: 浮動小数点数の有効数字部分 [cite: 1562]。
* [cite_start]**指数部 (Exponent)**: 浮動小数点数の桁を表す部分。大小比較を容易にするため、実際の値にバイアス（ゲタ）を加えたゲタばき表現が用いられる [cite: 1562, 241, 1564]。
* [cite_start]**非数 (NaN - Not a Number)**: 0÷0など、不正な演算結果を示す特別な値 [cite: 1573]。

---

## 4. プロセッサのデータパスと制御

### データパスと制御信号

単一サイクルプロセッサのデータパスは、命令の種類に応じて必要な機能ユニットを制御信号で切り替えながら動作する。

![A simplified diagram of a single-cycle MIPS datapath.](https://i.imgur.com/u1nSkgp.png)

* **データパスの構成要素**:
  * [cite_start]**命令メモリ**: PCが示すアドレスから命令を読み出す [cite: 1678]。
  * [cite_start]**PC (プログラムカウンタ)**: 次に実行する命令のアドレスを保持する [cite: 1678]。
  * [cite_start]**レジスタファイル**: レジスタの読み書きを行う [cite: 1681]。
  * [cite_start]**ALU (算術論理ユニット)**: 算術演算や論理演算を実行する [cite: 1681]。
  * [cite_start]**データメモリ**: `lw` や `sw` 命令でデータの読み書きを行う [cite: 1689]。
* **主要な制御信号の機能**:
  * [cite_start]**RegDst**: 書き込み先レジスタを`rt` (0) と `rd` (1) のどちらにするか選択 [cite: 1696]。
  * [cite_start]**ALUSrc**: ALUの第2入力をレジスタ(`rt`) (0) と即値 (1) のどちらにするか選択 [cite: 1696]。
  * [cite_start]**MemtoReg**: レジスタへの書き込みデータをALUの実行結果 (0) とメモリからの読み出しデータ (1) のどちらにするか選択 [cite: 1696]。
  * [cite_start]**RegWrite**: レジスタファイルへの書き込みを有効化 (1) するか [cite: 1682]。
  * [cite_start]**MemRead**: データメモリの読み出しを有効化 (1) するか [cite: 1690]。
  * [cite_start]**MemWrite**: データメモリの書き込みを有効化 (1) するか [cite: 1690]。
  * [cite_start]**Branch**: 分岐命令 (`beq`) であり、かつALUのゼロ判定が真の場合にPCを分岐先アドレスに更新する [cite: 1698, 1699]。
  * [cite_start]**Jump**: PCをジャンプ先アドレスに更新する [cite: 1735]。
  * [cite_start]**ALUOp**: 命令のopコードに基づき、ALU制御ユニットに送られる信号。ALU制御ユニットはこれとfunctフィールドから最終的なALU操作を決定する [cite: 1713]。

### ALU制御

| 命令のopコード | ALUOp | 命令操作 | functフィールド | ALUの演算 | ALU制御コード |
| :--- | :--- | :--- | :--- | :--- | :--- |
| lw/sw | 00 | load/store | xxxxxx | 加算 | 0010 |
| beq | 01 | branch equal | xxxxxx | 減算 | 0110 |
| R形式 | 10 | add | 100000 | 加算 | 0010 |
| R形式 | 10 | sub | 100010 | 減算 | 0110 |
| R形式 | 10 | and | 100100 | AND | 0000 |
| R形式 | 10 | or | 100101 | OR | 0001 |
| R形式 | 10 | slt | 101010 | set on less than | 0111 |
[cite_start][cite: 1714]
