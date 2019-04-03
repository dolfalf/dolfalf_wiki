
## Swift基本

- swift clouser

https://qiita.com/taketomato/items/5731cff19c40cde94528

- map

配列のmapは配列の要素1つ1つに操作をした結果の配列を返します。

```
[1, 2, 3].map { $0 * 2 } // → [2, 4, 6]
["3", "2", "1"].map { Int($0) } // → [Optional(3), Optional(2), Optional(1)]
```

- flatmap

flatMapはmapのような動きをして、更に2重の配列を1重に直してくれます。

```
[[1, 2], [3]].flatMap { $0 } // → [1, 2, 3]
[[1, 2], [3]].flatMap { $0 + [1] } // → [1, 2, 1, 3, 1]
```

- flatMap(中がオプショナルな配列用)

中身がOptionalの配列を中身をアンラップした配列にしてくれます。

```
["1", "2", "3"].map { Int($0) } // → [Optiona(1), Optiona(2), Optiona(3)]
["1", "2", "3"].flatMap { Int($0) } // → [1, 2, 3]
```

- filter

filterは条件に合う要素を絞り込む時に使う！

filterは、条件にマッチする要素のみを取り出したい場合に使用します。

以下のコードでは配列内の3未満の数値を取り出しています。

```
let array = [1,2,3,4,5]
let newArray = array.filter { $0 < 3 }
newArray // [1,2]
```

## RxSwift What??

- just

ある特定の値をを元にObservableを生成します。
1回のonNext(value)の直後にonCompletedを発行します。

もっと詳しく。。。
[RxSwift Observable生成関数まとめ](https://qiita.com/moaible/items/de94c574b25ea4f0ef17)





