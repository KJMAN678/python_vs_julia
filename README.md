# python_vs_julia
01 python.ipynb python のコード  
02 julia.ipynb julia のコード  

ざっくりとしたコードの流れ

- データの読込  
- 統計量の表示  
- 欠損値の処理  
- 相関係数
- 特徴量の選定
- データの分割
- 学習モデルの作成
‐ 誤差
‐ 予測データの作成
- csvの出力

## python と julia の違いをピックアップ

#### ライブラリのインポート
##### python
```python
import pandas as pd
```

##### julia
```julia
using DataFrames
```

#### csv の読込
##### python
```python
train = pd.read_csv(カレントディレクトリのパス + "train.csv")
```

##### julia
```julia
train = DataFrame(load("train.csv"))
```

#### 欠損値のカウント

##### python
```python
train.isnull().sum()
```

#### julia
```julia
Dict(zip(names(train), sum.(eachcol(ismissing.(train)))))
```

#### 欠損値を平均値に置き換える

##### python
```python
test["Age"] = test["Age"].fillna(test["Age"].mean())
```

##### julia
```julia
test[:, :Age] = coalesce.(test[:, :Age], mean(test[ismissing.(test)[:, :Age] .== 0, :][:, :Age]))
```
