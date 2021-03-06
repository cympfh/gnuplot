# インラインデータ

スクリプトの中で直接データを書いて使う方法

## 複数行文字列リテラルとして与える方法

変数にデータを代入してこれを plot させる.
以下の例では `$data` にデータを入れて使っている.

```bash
$data << EOD
0 0
1 1
2 4
3 8
4 16
5 24
6 32
EOD

plot $data w lp
```

## 標準入力から与える方法

ファイル名を `'-'` とすると標準入力から読む.
標準入力といってもバッチ実行モードでは, plot コマンドに続くデータがそのまま標準入力として渡されるので, スクリプトにデータを記述できる.

`e` コマンドでデータの入力を終わる.

```bash
plot '-' w lp
0 0
1 1
2 4
3 8
4 16
5 24
6 32
e
```

複数 `'-'` をプロットすれば複数回データの入力を読む.

```bash
plot '-' w lp, '-' w lp
1
2
3
e
1
4
9
e
```
