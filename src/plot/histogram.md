# ヒストグラム（度数表）

## 概要

ある値の列からなるデータがあるとき, コレに関するヒストグラムを作成する.
直接的にその機能は gnuplot にはなく,
度数を計算する必要があるが, 次の方法を使うとうまくこれが gnuplot の機能で実現する.

## 手法

`x:(1.0)` からなる折れ線グラフを
`with frequency`
で描くと重複した点の個数だけ `y` を加算する.
これに `with boxes` 等の装飾を施すことでよくあるヒストグラムを描ける.

## Example

データはソートしておいた方が無難.
`x` の上に置く box は `x` を中心とする幅を持った箱として描画されるので,
必要に応じて `0.5` だけずらすなどすると見やすくなる.

![](https://i.imgur.com/jlBaaED.png)

### Source Code

```bash
width = 1.0
hist(x) = width * (floor(x / width) + 0.5)
set boxwidth width * 1.0
set xtics width

$data <<EOM
0
1
1
1
1
2
2
3
6
8
EOM

set xrange [0:10]
set yrange [0:]
set ytics 1
set grid
set style fill solid 0.5 border lc rgb '#55aaff'
plot $data u (hist($1)):(1) smooth frequency with boxes fillcolor '#55aaff' not
```
