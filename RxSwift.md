
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

---

- Single

**性質**

1度だけ onSuccsess または onError が流れる。 onComplete 、 onNext は流れない点に注意

**使い所**

レスポンスのあるAPIリクエスト

プロミス的な使い方

FirebaseのsingleEvent


```
public enum SingleEvent<Element> {
    /// One and only sequence element is produced. (underlying observable sequence emits: `.next(Element)`, `.completed`)
    case success(Element)

    /// Sequence terminated with an error. (underlying observable sequence emits: `.error(Error)`)
    case error(Swift.Error)
}
```

- Completable

**性質**

1度だけ 、onComplete または onError が流れる。

**使い所**

レスポンスボディの無いAPIリクエスト


```
public enum CompletableEvent {
    /// Sequence terminated with an error. (underlying observable sequence emits: `.error(Error)`)
    case error(Swift.Error)

    /// Sequence completed successfully.
    case completed
}
```

- Maybe

**性質**

SingleとCompleteが合わさったような性質。
1度だけ、アイテムかerrorが流れるか、または全くイベントが流れない。
(実装の際にはイベントが流れてこないことがある点も考慮が必要)

**使い所**

1回だけ表示したいイベントの条件とか？


## RxSwiftの機能カタログ

- zip

複数の Observable を順番に組み合わせます。ReavtiveX の説明はこちらです。

CollectionType の拡張メソッドとして提供されています。

```
let observable1 = Observable.of(1, 2, 3, 4, 5)
let observable2 = Observalbe.of("A", "B", "C", "D")
let newObservable = [observable1, observable2].zip { "\($0[0])\($0[1])" }
// "1A", "2B", "3C", "4D" を通知する
```
