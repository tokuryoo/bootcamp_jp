# Daily guide : day 3 🐥

Welcome into the **day 3** of the Motoko Bootcamp ! <br/>
Today we will cover the following topics : **Array**, **Optional and Generic type**, and **Higher order functions**.

Motoko Bootcamp の **day 3** へようこそ!<br/>
本日は、以下のトピックを取り上げます。: **配列*、*Optional と Generic 型**、**高階関数**

# Prerequisites 前提条件✅

- Make sure you have dfx installed on your machine.
- お使いのマシンに dfx がインストールされていることを確認してください。

  ```
  dfx --version
  ```

- Start a new project called **day_3** and turn on your local replica.
- 新しいプロジェクト **day_3** を開始し、ローカルのレプリカをオンにします。

  ```
  dfx new day_3
  cd day_3
  dfx start
  ```

# Array 配列 🚚

Datastructures in any programming language are essential, on almost every program you need to store and access data into datastructures. 💿<br/>
どのようなプログラミング言語でもデータ構造は不可欠であり、ほとんどすべてのプログラムにおいて、データをデータ構造に格納し、アクセスする必要があります。💿

Data structures come in a lot of differents forms, each one has its own advantages and drawbacks, there is no perfect datastructures (even though some are more used than others), the optimal datastructure for a given task depends on the situtation and on your priorities.<br/>
データ構造には様々な形態があり、それぞれに利点と欠点があります。あるタスクに最適なデータ構造は、状況や優先順位に依存します。

We have already played with **Array**, but today we'll see exactly how they are created and many useful functions to use with them.<br/>
すでに**配列**で遊んできましたが、今日はそれらがどのように作られるのか、またそれらを使った多くの便利な関数について見ていきましょう。


<p align="center"> <img src="img/array.png" width="400"/> </p>

An array is a fixed-length data structure, once an array of a specified size is created you cannot increase the capacity expect by creating a completely new array.
This means that at the time the code will run, it will always **know** what is the size of the array. (This is not the case for all datastructures) <br/>
Accessing an element in an array is extremely simple, you only need to request the value at a specific index.

配列は固定長のデータ構造であり、一度指定したサイズの配列を作成すると、全く新しい配列を作成しても容量を増やすことはできません。
つまり，コードが実行されるときには，常に配列のサイズを**知っている**ことになります．(これはすべてのデータ構造に当てはまるわけではありません）。<br/>
配列の要素へのアクセスは非常に簡単で、特定のインデックスにある値を要求するだけです。

```
let array : [Nat] = [10, 3, 4, 5];
let a : Nat = array[3]; // 5
```

You can access tothe size of an array using **.size()**.

配列のサイズは、**.size()** を使ってアクセスすることができます。

```
let array : [Nat] = [1, 3 , 4];
let size : Nat = array.size() // 3
```

🕵️ Deeply understanding why accessing an element in an array is so efficient involves explaining how the computer manages memory, this is out of scope for this lesson but I'll try to explain it in simple terms : if we know the size of an array when the code is compiled, we can allocate the exact memory for it, remember the memoy location of the first value in the array and write all other values in the memory locations directly following the location of the first value.

🕵 配列の要素にアクセスするのがなぜ効率的なのかを深く理解するには、コンピュータがどのようにメモリを管理しているかを説明する必要があります。: コンパイル時に配列のサイズが分かっていれば、その配列のために正確なメモリを確保し、配列の最初の値のメモリ位置を記憶し、最初の値の位置の直後のメモリ位置に他のすべての値を書き込むことができます。

Then if we want to access any element in the array we just need to look at the location of the first element and eventually jump to the right memory location by taking into account the index of the element we are trying to access.

そして、配列内の任意の要素にアクセスしたい場合は、最初の要素の位置を確認し、最終的にはアクセスしようとする要素のインデックスを考慮して、正しいメモリ位置にジャンプすればよいのです。

In Motoko, by default arrays are **immutable** (like variables). This means once the array is created you can only **read** the values inside but cannot **write**.

Motoko では、デフォルトで配列は **immutable** (変数のようなもの) です。つまり、配列が作成されると、中の値を**読む**ことだけができ、**書く**ことはできません。


You can create **mutable** arrays but you need to use the keyword **var**.

**mutable** 配列を作成することができますが、キーワード **var** を使用する必要があります。

```
let array_1 : [Nat] = [1, 2, 3]; // immutable

let array_2: [var Nat] = [1, 2, 3]; // mutable
```

```
array_1[1] := 0; // ⛔️ impossible to reassign values of an immutable array. 不変配列の値を再代入することは不可能です。

array_2[1] := 0; // ✅ valid reassignment in a mutable array. ミュータブル配列で有効な再割り当て。
```

# Challenge 🎮

Take a break and try completing challenge 1 to 3.

一息ついてから、課題1～3をクリアしてみてください。

# Optional type // Optional 型❓

In Motoko there is a special value called **_null_**. <br/>
This value represents the absence of a result, this is useful if you want one of your function to indicate that it has no specific return value.
The type of **_null_** is **Null** (this type contains only one value).

Motokoでは、**_null_** という特殊な値があります。<br/>
この値は結果がないことを表し、関数の1つに特定の戻り値がないことを示したい場合に有用である。
**_null_** の型は **Null** である（この型は1つの値のみを含む）。

Let's say you want to create a function named **_index_of_one_** that takes an array of type **[Nat]** and returns the first index such that the value at that index is equal to 1. <br/> You also want this function to return **_null_** if no matching index was found.
例えば、 **[Nat]** 型の配列を受け取り、そのインデックスにある値が1に等しい最初のインデックスを返す **_index_of_one_** という名前の関数を作りたいとします。<br/>また、この関数は、一致するインデックスが見つからなかった場合、**_null_** を返すようにしたい。


```
actor {
    public func index_of_one(array : [Nat]) : async Nat {
        for((number,index) in array.vals()){
            if(number == 1) {
                return index;
            }
        };
        return null;
    };
};
```

This declaration is not valid because **_null_** is not a type Nat 😕 <br/>
Trying to deploy this code would result in the following error.

この宣言は、**_null_** が Nat 😕 型でないため、無効です。<br/>
このコードをデプロイしようとすると、次のようなエラーが発生します。

```
type error [M0050], literal of type
  Null
does not have expected type
  Nat
```

We need a way to explain to Motoko that the value returned can be either a **Nat** or **_null_**.

返される値が **Nat** か **_null_** のどちらかであることをMotokoに説明する方法が必要です。

Luckily there is a notation exactly for that, it's called the optional type : **?T**. <br/>
In our case we would use **?Nat** because we are returning **Nat** or **_null_**.

幸運なことに、まさにそのための記法があり、それはオプション型と呼ばれています。**?T**.<br/> 私たちの場合は、**Nat** または **_null_** を返すので、**?Nat** を使用します。

We can rewrite our actor using our new type.

新しい型を使って、アクターを書き換えることができます。

```
actor {
    public func index_of_one(array : [Nat]) : async ?Nat {
        for((number,index) in array.vals()){
            if(number == 1) {
                return index;
            }
        };
        return null;
    };
};
```

Sometimes in your code you will need to handle those optional values, you can do so with a **switch** expression.

コード内でこれらのオプション値を処理する必要がある場合、**switch** 式を使用して処理することができます。

```
import Nat "mo:base/Nat";
actor {
    public func null_or_nat(n : ?Nat) : async Text {
        switch(n){
            // Case where n is null
            case(null) {
                return ("The argument is null");
            };
            // Case where n is a nat
            case(?something){
                return ("The argument is : " # Nat.toText(something));
            };
        };
    };
};
```

You can deploy this actor and try those commands.

このアクターをデプロイして、これらのコマンドを試すことができます。

```
dfx canister call day_3 null_or_nat '(opt 4)'
("The argument is : 4")
```

🕵️ Notice again the difference between Candid and Motoko. <br/>
Here we have to use the Candid syntax **opt 4** whereas in Motoko we could just write **?4**.

🕵️ Candid と Motoko の違いにもう一度注目してください。<br/>
ここでは、Motokoでは単に**?4**と書くことができるのに対し、Candidでは**opt 4**という構文を使わなくてはなりません。

```
dfx canister call day_3 null_or_nat '(null)'
("The argument is null")
```

☢️ It's important to understand that the type **?Nat** and **Nat** are really different. <br/> If a function is expecting a value of type **Nat** as parameter and it receives a value of type **?Nat** it will not appreciate. 😠

☢️ **?Nat** 型と**Nat** 型は本当に違うものだと理解することが重要です。<br/>
もし関数がパラメータとして **Nat** 型の値を期待していて、それが **?Nat** 型の値を受け取った場合、それは評価されないでしょう。😠

Take a loot at something we shouldn't do, we'll use again the same code from the previous example but without the **switch** expression.

この例では、前の例と同じコードを使いますが、**switch** 式は使いません。

```
import Nat "mo:base/Nat";
actor {
    public func null_or_nat(n : ?Nat) : async Text {
        return ("The argument is : " # Nat.toText(something)); ⛔️ what is the type of something at this point?
    };
};
```

This code will not compile because the function toText is expecting a parameter of type Nat as we can see in the documentation.

このコードは、ドキュメントにあるように、関数 toText が Nat 型のパラメータを期待しているため、コンパイルされません。

<p align="center"> <img src="img/toText.png" width="600"/> </p>

Some functions accept optional types, but not this one. <br/>
I hope you now appreciate the importance of **switch** / **case**.

関数によっては、オプションの型を受け付けるものもありますが、この関数ではありません。<br/>
これで**switch** / **case**の重要性を理解していただけたと思います。

# Generic type // Generic 型 👤

I have briefly introduced the concept of generic type when we introduced the optional type with the notation **?T**. Let's dive into it.

オプショナル型を**?T**という表記で紹介したときに、ジェネリック型の概念について簡単に紹介しました。その中に飛び込んでみましょう。

The generic type **T** allow us to write more general code, that can work with different types and be reused.

汎用型 **T** は、より一般的なコードを書くことを可能にし、異なる型を扱うことができ、再利用することができます。

Let's say we want to write a function called **_is_array_size_even_** that returns a **Bool** indicating if the size of the array is even or not.</br>
We could write something like this

例えば、配列のサイズが偶数かどうかを示す **Bool** を返す **_is_array_size_even_** という関数を書きたい場合を考えてみましょう。<br/>
次のように書けばよいでしょう。

```
public func is_array_size_even(array : [Nat]) : async Bool {
    let size = array.size();
    if(size % 2 == 0){
        return true;
    } else {
        return false;
    };
};
```

This function is valid, but it only works if our array is filled with **Nat**. What about an array with **Text** values inside ?

この関数は有効ですが、配列が **Nat** で満たされている場合のみ機能します。配列の中に **Text** 値がある場合はどうでしょうか？

- An quick and dirty solution would be to create a lot of different functions for each type of array we want to use : **\_is_array_size_even_nat** **\_is_array_size_even_text** **\_is_array_size_even_char** ...
  I hope you agree that this solution sucks.
- 手っ取り早く解決するには、使用したい配列の種類ごとに多くの異なる関数を作成することです。**\_is_array_size_even_nat** **\_is_array_size_even_text** **\_is_array_size_even_char** ...
  このソリューションが最悪であることに同意していただけると幸いです。

- A better solution is to use the generic notation : **T**. This basically allow us to create **one** generic function that we can reuse for all the types available in Motoko.
- より良い解決策は，一般的な表記法を用いることである．**T**. これにより、Motokoで利用可能なすべての型に対して再利用可能な**1つの**汎用関数を作成することが基本的に可能になります。

```
public func is_array_size_even<T>(array : [T]) : async Bool {
    let size = array.size();
    if(size % 2 == 0){
        return true;
    } else {
        return false;
    };
};
```

T means "whatever type you want" and [T] means "whatever type you want as long as it's an array".
Tは「好きな型」、[T]は「配列である限り好きな型」を意味します。

🕵️ Notice the <T> following the name of the function. It means that this function now depends on the type of T. <br/> If you want to use the array_size function you'll need to specify for which type you are going to use it !

🕵️ 関数の名前の後にある<T>に注目してください。これは、この関数がTの型に依存することを意味しています。<br/>
もしarray_size関数を使いたいなら、どの型に対して使うかを指定する必要があります !


```
func is_array_size_even<T>(array : [T]) : Bool {
    let size = array.size();
    if(size % 2 == 0){
        return true;
    } else {
        return false;
    };
};

let array : [Nat] = [1,2,3,4];
let bool : Boolean = is_array_size_even<Nat>(array); // I indicate to the compiler which type I'm gonna use the function on.
```

We've used T to represent the generic type but you will also see A or B or C being used in the documentation, this doesn't change anything.

ここではTを使って一般的な型を表しましたが、ドキュメントではAやB、Cも使われています。

# Challenge 🎮

Take a break and try completing challenge 4 to 6.

一息ついて、チャレンジ4～6をクリアしてみてはいかがでしょうか。

# Higher order functions 高階関数🏋️‍♀️

So far, we've only seen functions taking simple arguments (**Nat**, **Text**, **Char**...) but functions can also take other functions as arguments, such functions are called **higher order function**.

これまで、単純な引数（**Nat**, **Text**, **Char**...）を取る関数しか見てきませんでしたが、関数は他の関数を引数に取ることもでき、そのような関数は **高階関数** と呼ばれます。

The **Array** module contains several higher order function, those are really powerful and useful methods so I'll present some of them.

**Array**モジュールにはいくつかの高階関数があり、それらは本当に強力で便利なメソッドなので、そのいくつかを紹介します。


- <a href="https://smartcontracts.org/docs/base-libraries/Array.html#find" target="_blank"> **Find** </a> : This function takes two parameters [A] an array and **f** a function that takes a value of type A and returns a **Bool**. (f is called a **predicate**).<br/>This function returns the first value for which the **predicate** is **true**.
- <a href="https://smartcontracts.org/docs/base-libraries/Array.html#find" target="_blank"> **Find** </a> : この関数は2つのパラメータ [A] 配列と **f** 型の値を受け取り **Bool** を返す関数を受け取ります。(fは**述語**と呼ばれる)。<br/>この関数は**述語**が**true**となる最初の値を返す。

```
import Array "mo:base/Array";
actor {
    let f = func (n : Nat) : Bool {
        if (n > 10) {
            return true
        } else {
            return false
        };
    };

    public func mystere(array : [Nat]) : async ?Nat {
        return(Array.find<Nat>(array, f));
    };

};
```

🕵️ Notice this code sample makes use of the 3 concepts we've been discussing about : Optional type, Generic type and Higher-order functions. 😎

🕵️ このコードサンプルでは、これまで議論してきた3つの概念を利用していることに注目してください。オプショナル型、汎用型、高階関数。😎

<details>
        <summary style="color:green"> 🤔 What do you think <strong> mystere([1,4,5,18,0,2,3]) </strong> will return ? // <strong> mystere([1,4,5,18,0,2,3]) </strong> は何を返すと思いますか？</summary>
        <br/>    
        The first value above 10 in the array so <strong> ?18 </strong> (do not forget that the value is of type <strong> ?Nat </strong> because this function might return <strong> <i> null </i> </strong>).
		<br/><br/>
        配列の10以上の最初の値なので <strong>?18</strong> (この関数は <strong><i>null</i></strong> を返すかもしれないので、この値が <strong>?Nat</strong> 型であることを忘れないでください).
    </details>
	<br/>

- <a href="https://smartcontracts.org/docs/base-libraries/Array.html#filter" target="_blank"> **Filter** </a> : This function also takes an array [A] and a **predicate** f and returns a new array [A] where only values that validate the predicate are kept.
- <a href="https://smartcontracts.org/docs/base-libraries/Array.html#filter" target="_blank"> **Filter** </a> : この関数も配列 [A] と **述語** f を受け取り、述語を検証する値のみが保持された新しい配列 [A] を返す。

We can even reuse the same predicate as in the previous example. ♻️

先ほどの例と同じ述語を再利用することも可能です。♻️


```
import Array "mo:base/Array";
actor {
    let f = func (n : Nat) : Bool {
        if (n > 10) {
            return true
        } else {
            return false
        };
    };

    public func surprise(array : [Nat]) : async ?Nat {
        return(Array.filter<Nat>(array, f));
    };
};
```

<details>
        <summary style="color:green"> 🤔 What do you think <strong> surprise([1, 23, 4, 25, 12]) </strong> will return ? // <strong> surprise([1, 23, 4, 25, 12]) </strong> は何を返すと思いますか？ </summary>
        <br/>    
        An array where only values above 10 are kept (the order is not modified) : <strong> [23, 25, 12]</strong>.
		<br/> <br/>
        10以上の値のみが保持される配列（順序は変更されない）: <strong> [23, 25, 12]</strong><br/> <br/>
    </details>
	<br/>

- <a href="https://smartcontracts.org/docs/base-libraries/Array.html#fmap" target="_blank"> **Map** </a> : This function (again) takes an array [A] but this time f is a function taking a value of type A and returning a value of type B. This function simply apply the function f to **all** elements in the array and returns the new array.

- <a href="https://smartcontracts.org/docs/base-libraries/Array.html#fmap" target="_blank"> **Map** </a> : この関数も配列 [A] を受け取りますが、今度は f が A 型の値を受け取り B 型の値を返す関数です。この関数は単に配列の **全** 要素に関数 f を適用して、新しい配列を返します。


```
import Array "mo:base/Array";
actor {
    let f = func (n : Nat) : Nat {
        return(n + 1);
    };

    public func riddle(array : [Nat]) : async [Nat] {
        return(Array.map<Nat, Nat>(array, f));
    };
};
```

<details>
        <summary style="color:green"> 🤔 What do you think <strong> riddle([0, 0, 0, 0]) </strong> will return ? // <strong> riddle([0, 0, 0, 0]) </strong> は何を返すと思いますか？</summary>
        <br/>    
        A new array where all values have been increased by one : <strong> [1, 1, 1, 1]</strong>.
		<br/> <br/>
        すべての値が 1 つずつ増加した新しい配列 : <strong> [1, 1, 1, 1]</strong>.<br/> <br/>
    </details>
	<br/>

# Challenge 🎮

Take a break and try completing challenge 7 to 10.

一息ついて、チャレンジ7～10をクリアしてみてください。

