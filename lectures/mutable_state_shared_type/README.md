## Prerequisites 前提条件

- Read [this](https://smartcontracts.org/docs/language-guide/mutable-state.html)
- 読む [これ](https://smartcontracts.org/docs/language-guide/mutable-state.html)
- [this](https://smartcontracts.org/docs/language-guide/sharing.html)
- [これ](https://smartcontracts.org/docs/language-guide/sharing.html)

## Things we'll cover 取材内容

- `let` vs `var`
- let` と `var` の比較
- immutable vs mutable arrays
- immutable 配列 vs mutable配列
- `Array` module from the base library - https://smartcontracts.org/docs/base-libraries/Array.html
- 基本ライブラリの `Array` モジュール - https://smartcontracts.org/docs/base-libraries/Array.html
  - freeze
  - フリーズ
  - thaw
  - 解凍
  - tabulate
  - 集計
- Example of a Pub Sub implementation
- Pub Sub の実装例

## Takeaways 持ち味

- As a rule of thumb, start with an immutable variable and change it when the situation demands.
- 経験則から言うと、まずイミュータブルな変数で始めて、状況に応じて変更するのがよいでしょう。
- Sharing state requires that state to be sharable.
- 状態を共有するには、その状態が共有可能であることが必要です。

## Resources リソース

- [pubsub example](https://github.com/dfinity/examples/tree/master/motoko/pub-sub)
- [pubsub 例](https://github.com/dfinity/examples/tree/master/motoko/pub-sub)
