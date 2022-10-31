# Daily guide : day 4 🐓

Welcome into the **day 4** of the Motoko Bootcamp ! <br/>
Today we will cover the following topics : **Custom type** and **Linked list**.
Motoko Bootcamp の **day 4** へようこそ !<br/>
本日は、以下のトピックを取り上げます。**Custom 型** と **連結リスト** について説明します。

# Prerequisites 前提条件 ✅

- Make sure you have dfx installed on your machine.
- お使いのマシンに dfx がインストールされていることを確認してください。

  ```
  dfx --version
  ```

- Start a new project called **day_4** and turn on your local replica.
- 新しいプロジェクト **day_4** を開始し、ローカルレプリカをオンにします。

  ```
  dfx new day_4
  cd day_4
  dfx start
  ```

# Custom type // Custom型🔧

During the previous days we have manipulated different types (Nat, Text, Bool, Array); today we are creating to create our **own** type !
Create a new file called person.mo in the day_4 folder (next to main.mo) and copy and paste the following declaration.

これまでの数日間で、さまざまな型（Nat、Text、Bool、Array）を操作してきました。 今日は、自分自身の型を作成します。
day_4フォルダ（main.mo があるフォルダ）（訳注 src フォルダ直下で良い）にperson.moというファイルを新規に作成し、以下の宣言をコピー＆ペーストしてください。


```
module {

}
```

This is a **module** declaration, contrary to all previous .mo files that were **actor** declarations. <br/>
A module is (just the like the base library modules we've been using) a piece of code that we can import and reuse.

これは **モジュール** 宣言であり、これまでの .mo ファイルが **アクター** 宣言であったのとは対照的です。<br/>
モジュールとは、（これまで使ってきた base ライブラリモジュールと同じように）インポートして再利用できるコード片のことです。

This is how we can create a custom type. If you want your type to be accessible from the outside of the module you need to make it **public**.

このようにして、カスタムタイプを作成できます。もし、モジュールの外からあなたのタイプにアクセスできるようにしたい場合は、それを **public** にする必要があります。

```
public type Person = {
  name : Text;
  age : Nat;
};
```

The type Person is also called an **object** with different **fields** (name, age).

Person 型は、異なる**フィールド** (名前、年齢)を持つ**オブジェクト**とも呼ばれます。

Now that we have declared our type we can create our first variable of type Person.

型を宣言したので、Person型の最初の変数を作成できます。

```
let tom : Person = {
  name = "Tom Cruise";
  age = 59;
};
```

You can access any **field** using the **dot** notation.

**ドット** 記法を用いて、任意の **フィールド** にアクセスできます。

```
let tom_name = tom.name;
let tom_age = tom.age;
```

In your main.mo file you can **import** the type Person and use it as if it was part of Motoko native types.

main.moファイルの中で、型 Person を **import** して、Motokoのネイティブ型の一部であるかのように使用できます。


```
import Person "person";
actor {
  public type Person = Person.Person;
  let penelope : Person = {
    name = "Penelope Cruz";
    age = 47;
  };

};

```

💡 **Person.Person** simply means : grab the type Person from the Person module.

💡 **Person.Person** は、Person モジュールから Person タイプを取得することを意味します。

# Challenge 課題 🎮

Take a break and try completing challenge 1 to 3.

一息ついてから、チャレンジ1～3をクリアしてみてください。

# Linked list //連結リスト 🔗

A linked list is a datastructure, that contrary to array has a **dynamic** size.
It consists of many **nodes** each node contains :

連結リストはデータ構造の一つであり、配列とは異なり、**動的** なサイズを持つ。
多くの **ノード** から構成され、各ノードは下記 :

- A value of type T.
- T型の値。
- A pointer to the next node or to **_null_**.
- 次のノードへのポインタ、または **_null_** へのポインタ。

<p align="center"> <img src="img/linked-list.svg" width="400"/> </p>
<p align="center"> <i> <strong> A linked list of Nat</i> </strong> </p>

The first element of this linked list is a node where :

この連結リストの最初の要素は、下記ノード :

- Value of type **Nat** equals to 12.
- 型 **Nat** の値は12に相当する。
- A pointer to next node.
- 次のノードへのポインタ。

💡 A pointer is just a memory location indicating where a data is stored. You can think of it as an **arrow** indicating where to find the next node.

💡 ポインターは、データが格納されている場所を示すメモリの場所に過ぎません。次のノードがどこにあるかを示す**矢印**のようなものだと考えることができます。

Here's how one would define a **linked list** in Motoko.

Motokoで**連結リスト**を定義すると、次のようになります。

```
public type List<T> = ?(T, List<T>);
```

This means that a List of type T is either :

これは、型TのListは、以下のいずれかであることを意味します。

- **_null_**
- A **couple** of two elements.
  - 1st element is a value of type T.
  - 2nd element is a List of type T.
- 2つの要素からなる **couple** である。
  - 1番目の要素はT型の値である。
  - 2番目の要素はT型のListである。

💡 To acces an element in a **linked list** you need to start from the first node and follow all the nodes until you came accross the value you are looking for. </n> <br/>
This is more complex than with **arrays** where we could just use array[i], but linked lists have other advantages that we will see.

**連結リスト**の要素にアクセスするには、最初のノードから始めて、探している値に出会うまですべてのノードをたどる必要があります。</n> <br/>
これは、単にarray[i]を使うことができる**配列**よりも複雑ですが、連結リストには他の利点もあるので、これから見ていきます。


# Challenge 課題🎮

Take a break and try completing challenge 4 to 6. <br/>

一息ついて、チャレンジ4～6をクリアしてみてはいかがでしょうか。

# Switch / Case

We have already seen the switch/case expression in previous lessons, but let's make a quick review.
We can use the switch/case on **optional expression**.
An element of type **List** can be of value **_null_**. We can check it that way.

switch/case 式は以前のレッスンですでに見ていますが、簡単に復習しておきましょう。
**switch/caseは**オプション式**で使うことができます。
List** 型の要素は、値 **_null_** である可能性があります。そのようにチェックすることができます。

```
public type List<T> = ?(T, List<T>);
public func is_list_null(list : List<Nat>) : async Text {
        switch(list){
            case(null) {
                return "The list is null... 😢"
            };
            case(?list){
                return "This list is not null 🥳"
            };
        }
    };
```

The switch/case can also be used for testing different **values**.

switch/caseは、異なる**値**をテストするためにも使用することができます。

```
public func month_to_season (month : Text) : async Text {
  switch(month){
    case("January") return "Winter";
    case("February") return "Winter";
    case("March") return "Spring";
    case("April") return "Spring";
    case("May") return "Spring";
    case("June") return "Summer";
    case("July") return "Summer";
    case("August") return "Summer";
    case("September") return "Autumn";
    case("October") return "Autumn";
    case("November") return "Autumn";
    case("December") return "Winter";
    case(_) return "This is not a month";
  }
};
```

The last case statement is used to indicate a default value, in case the value in the switch (in our case the **month**) do not find in any of the previous cases. It will default to the case with the **\_** indicator :

最後のcase文は、スイッチの値(この例では**month**)が前のどのケースにも当てはまらない場合に、デフォルト値を示すために使用されます。デフォルトでは、 **\_** インジケータの付いたケースになります。

```
case(_) return "This is not a month";
```

You can actually try this function by deploying it in the Motoko Playground and check what value you get back with "April" and then with "Hello".

実際にこの機能をMotoko Playgroundにデプロイして、「April」、「Hello」でどんな値が返ってくるか試してみてください。

# Challenge 🎮

Take a break and try completing challenge 7 to 10. <br/>

一息ついて、チャレンジ7～10をクリアしてみてください。
