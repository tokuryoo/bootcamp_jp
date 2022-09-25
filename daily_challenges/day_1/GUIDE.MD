# Daily guide : day 1 🥚

Welcome into the first day of the Motoko Bootcamp ! <br/>
This guide is meant to cover some basics on : **Actor**, **function**, **types**,**variables**, **loops** and **modules**.

Motoko Bootcampの初日を迎えました！<br/>
このガイドでは、以下の基本的な事柄について説明します。: **Actor**, **function**, **types**,**variables**, **loops** and **modules**.

# Prerequisites ✅

- Check you have dfx installed on your machine.
- dfxがインストールされていることを確認してください。

  ```
  dfx --version
  ```

- Start a new project called **day_1** and turn on your local replica.
- 新しいプロジェクト **day_1** を開始し、ローカルレプリカをオンにします。

  ```
  dfx new day_1
  cd day_1
  dfx start
  ```

# Motoko 👻

Motoko is a language that has been developed by the **Dfinity** foundation specifically for the Internet Computer. </br>

A motoko file is a file with the indication .mo at the end.

Let's create a new project with dfx using the command :

Motokoは、**Dfinity**財団がインターネット・コンピュータのために特別に開発した言語です。 </br>

motokoファイルは、末尾に.moの表示があるファイルです。

dfxで新しいプロジェクトを.moコマンドで作ってみましょう。


```
dfx create hello
```

You can open the new project with your IDE (Visual Studio Code or other) and you will notice inside src/hello a file called main.mo : this is a motoko file.

IDE (Visual Studio Code など) で新しいプロジェクトを開くと、src/hello の中に main.mo というファイルがあることに気づくでしょう。

<p align="center"> <img src="img/file.png" width="300"/> </p>

# Actor 🤖

If you open the main.mo file you will notice that the first word is **actor**.

main.moファイルを開くと、最初の単語が **actor** であることに気づくだろう。


```
actor {

};
```

An **actor** is simply the representation of a canister for the Motoko language.

On the Internet Computer each canister is separated from all other canisters and can only communicate with other canister through **asynchronous** messages. 📭

**アクター** とは、簡単に言えば、モトクロス言語のキャニスターを表現したものです。

インターネット・コンピュータでは、各キャニスターは他のすべてのキャニスターから分離されており、他のキャニスターとは **非同期** メッセージを通じてのみ通信することができます。📭


# Function ⚙️

This actor has only one function called **greet**. <br/>

このアクターは、**greet** という1つの機能しか持っていません。<br/>


```
actor {

    public func greet(name : Text) : async Text {
        return "Hello, " # name # "!";
    };
};

```

## Public / Private

Notice that this function is **public** : it means it can be called by other actors and by users on the Internet Computer. ✅ <br/>

You will see later that function can sometimes be **private** (in that case it can only be called by the actor himself and not by external entities). ⛔️

この関数は **public** であることに注意してください : これは、他のアクターやインターネット上のユーザーから呼び出すことができることを意味します Computer。✅ <br/>

関数が **private** である場合もあることは後で説明します（その場合、アクター自身によってのみ呼び出すことができ、外部からは呼び出すことができません）。⛔️

## Argument & Return value

The next thing you should notice is the **argument** of the function greet : the argument here is called name and is of type **Text**.

次に注目すべきは、関数greetの**引数**で、ここではnameと呼ばれ、**Text** という型になっています。

The return value of this function is of type **async Text**. <br/> This means that the person or canister calling will have to **await** to get the result. ⏱

この関数の戻り値は、**async Text** 型です。<br/> これは、呼び出した人またはキャニスターが結果を取得するために **待機** する必要があることを意味します。⏱

To understand this concept you need to imagine what it means to be a canister on the Internet Computer : at any moment an user or an other canister can call you through any of your **public** function.

このコンセプトを理解するためには、インターネット・コンピュータのキャニスターであることの意味を想像する必要があります。

What if you were already answering a previous request ? You are a simple program you can only do one thing at a time : you need to finish what you are currently doing and **then** you will be able to process the incoming request. ⚡️

もし、あなたがすでに前のリクエストに答えていたとしたらどうでしょう？あなたは一度に一つのことしかできない単純なプログラムです。現在行っていることを終えて、**それから**、入ってきた要求を処理することができます。⚡️


By specifying that the return value is of type **async Text** you indicate to anyone that if they call your **greet** function they will get back a **Text** value but they will have to wait a bit. 🏎

戻り値が **async Text** 型であることを指定することで、誰でもあなたの **greet** 関数を呼べば **Text** 値が戻ってくるが、少し待たなければならないことを示すことができるのです。🏎

**Remember** : every **public** function of an actor has a return value that is **async**.

アクターのすべての **public** 関数は **async** の戻り値を持っていることを **思い出してください**。


## Calling a function

We can call the greet function using <a href="https://smartcontracts.org/docs/developers-guide/cli-reference/dfx-parent.html" target="\_blank"> dfx </a> by running the following commands in your terminal.

ターミナルで以下のコマンドを実行することで、<a href="https://smartcontracts.org/docs/developers-guide/cli-reference/dfx-parent.html" target="\_blank"> dfx </a>を使用してgreet関数を呼び出すことができます。


```
dfx deploy day_1
```

Once the canister has been deployed.

キャニスターがデプロイされたら

```
dfx canister call day_1 greet '("world")'
("Hello, world!")
```

**day_1** is the name of the canister.

**day_1** はキャニスターの名前です。

**greet** is the function we are calling.

**greet** は、今回呼び出す関数です。

<br/>
**"world"** is the argument we are sending.
Note : when using dfx you should put your argument(s) into **'( )'**.

**"world"** は、送信する引数です。
注意 : dfx を使うときは、引数を **'( )'** に入れる必要があります。
<br/>

**"Hello, world"** is the value returned by the function.

**"Hello, world"** は、この関数が返す値です。

More generally you can call any canister method with any argument, using this generic command.

より一般的には、この汎用コマンドを使用して、任意の引数で任意のキャニスター・メソッドを呼び出すことができます。

```

dfx canister call <CANISTER_NAME> <METHOD_NAME> '(ARGUMENT)'

```

# Variables 変数 💾

You can declare variables using the **let** keyword and the assignement operator : **=** .

変数の宣言には、**let** キーワードと代入演算子を使用します。 : **=** .

<br/> You can think of a variable has a box where you can store anything and access it later using the name of this variable. 📦

変数とは、何かを保存しておき、後でこの変数名を使ってアクセスするための箱であると考えることができます。📦

```
let a = 5;
let b = a + 3; // 8
```

By default variables are **immutables** in Motoko, this means that once a variable has been assigned a value you cannot change it. <br/>

Motokoでは、デフォルトで変数は**不変**です。これは、一度値が割り当てられた変数は、変更できないことを意味します。

You can declare **mutable** variables using the **var** keyword.

**var** キーワードを使用すると、**mutable** 変数を宣言することができます。

```
var a = 5;
var b = a + 3; // 8
```

You can reassign a new value inside **mutable** variable with the reassignement operator : **:=**.

mutable** 変数の内部に新しい値を代入するには、再代入演算子 :  **:=**


```
var a = 5;  //  First declaration.
var a := 6; //  Reassignement to a new value.
```

Take a look at the following actor declaration 👀.

次のアクター宣言👀を見てみましょう。 👀.


```
actor {
    let a = 4;
    a := 5;
};
```

 <details>
        <summary style="color:green"> 🤔  What do you think would happen if we tried to deploy this actor ? 🤔 このアクターをデプロイしようとしたら、どうなると思いますか？</summary>
        <br/>
        This would result in an error, we are trying to reassign a <strong> mutable </strong> variable. The exact error is : <strong> <i> type error [M0073], expected mutable assignment target. </strong> </i>
        これは、<strong> mutable </strong> 変数を再代入しようとしている、というエラーになります。正確なエラーは : <strong> <i> type error [M0073], expected mutable assignment target. </strong> </i> です。
</details>
<br/>

# Types 型 🍎

In Motoko, every variable has a type, to indicate the type we use the symbol <strong> : </strong> <br/> Here's a few examples of variable with their type and their value.

Motoko では、すべての変数に型があり、型を示すために <strong> : </strong> という記号を使用します。<br/>
 以下は、変数の型と値の例です。

```
let name : Text = "Motoko";

let age : Nat = "2";

let ghost : Bool = true;
```

In most cases, you can omit the type of a variable and Motoko will deduce it for you. For instance, if you declare a variable with this expression :
ほとんどの場合、変数の型を省略することができ、Motokoはそれを推論してくれます。例えば、このような式で変数を宣言した場合、:

```

let name = "Motoko";

```

Motoko will automatically know that this variable is of type **Text**. <br/>
However for the sake of clarity : I **strongly advise** you to use the the type of variables you are using and that's what we will do in the following lessons.

Motokoは自動的にこの変数が**Text**型であることを認識します。<br/>
しかし、わかりやすくするために、私は、あなたが使っている変数の型を使用することを強くお勧めします。

# Error エラー 😵

Motoko has strict rules around types, during this week you'll probably encounter a lot of **type errors**. 👩‍⚖️ <br/>

Motoko 型に厳しいので、この一週間は **型エラー**が 多発しそうです。 👩‍⚖️ <br/>


One example of such an error would be to try to add two variables of different types. Let's try to add a **Text** with a **Nat**.

このようなエラーの一例として、異なる型の2つの変数を追加しようとする場合があります。例えば、**Text**と**Nat**を追加しようとします。


```

public func add_five(number : Text) : async Text {
    return (number + 5);
};

```

Trying to compile this code will result in an type error.

このコードをコンパイルしようとすると、型エラーになります。

```

type error [M0050], literal of type
Nat
does not have expected type
Text

```

We will cover many types in details but for the moment try to remember that you should always keep an eye on what are the types of the variables you are using.

詳細はこれから説明しますが、とりあえず、自分が使っている変数がどのようなタイプなのか、常に注意しておくことを心がけてください。

# Nat and operations Nat と 演算子 🧮

Let's start with the **Nat** type. This type is meant to represent any natural number. <br/>

まず、**Nat** 型から始めましょう。この型は任意の自然数を表現するためのものです。

Natural numbers are : 0,1,2,3 ... ∞

自然数とは．0,1,2,3 ... ∞

## Addition 加算 ➕

You can add two numbers using the addition operator **+**

加算演算子 **+** を使って、2つの数値を足すことができます。


```

let a : Nat = 1 + 1;

```

## Multiplication 乗算 ✖️

You can multiply two numbers using the multiplication operator : **\***

2つの数字を掛け合わせるには、Multiplication演算子を使用します。: **\***


```

let a : Nat = 10 * 10;

```

## Substraction 減算 ➖

You can substract two numbers using the substraction operator : **-**

2つの数値を引き算するには、減算演算子 : **-**

```

let a : Nat = 10 - 5;

```

☢️ Be careful when using substraction operator with the type Nat. ☢️ <br/> <br/> The type **Nat** is composed of positive numbers only. <br/> If the result of the substraction is below 0, your value won't be of type Nat anymore and if your program if expecting a value of type **Nat** it might **trap**.

☢️ Nat型にサブトラクション演算子を使用する場合は注意が必要です。☢️ <br/> <br/> Nat** 型は正の数のみから構成されます。もし、減算の結果が0以下であれば、その値はもうNat型ではなく、もしプログラムが**Nat**型の値を期待しているならば、**trap**するかもしれません。


```
actor {
    let a : Nat = 1 - 2;
};
```

Trying to deploy this actor would result in a **subtraction underflow** causing a **trap**..

このアクターを配置しようとすると、**subtraction underflow** が発生し、**trap** を引き起こします。

```
Error: The Replica returned an error: code 5, message: "Canister rrkah-fqaaa-aaaaa-aaaaq-cai trapped explicitly: Natural subtraction underflow"

エラーです。レプリカはエラーコード5、メッセージを返しました。"キャニスター rrkah-fqaaa-aaaaq-cai が明示的にトラップされました。自然減算のアンダーフロー"

```

💡 A **trap** is an error that happen during the **execution** of a program, when a **trap** happen the execution of the programm is stopped and a, error message is returned.

💡 トラップとは、プログラムの実行中に発生するエラーのことで、トラップが発生すると、プログラムの実行が停止し、エラーメッセージが返されます。


## Division & modulo 除算と余り ➗

You can divide two numbers using the **division** operator : **/** .
<br>
You can get the remainder of a divided by b using the **modulo** operator : **%** .

2 つの数値を割り算するには、**division** 演算子を使用します。**/** .
<br>
a を b で割った余りは、**modulo** 演算子を用いて求めることができます。**%** .

```
let a : Nat = 10 / 2;
let b : Nat = 3 % 2;
```

In this case **a** equals **5** and **b** equals **1**.

この場合、**a**は**5**に、**b**は**1**に相当します。

# Challenge 🎮

Take a break and try completing challenge 1 to 4.
一息ついてから、チャレンジ1～4をクリアしてみてください。

# Boolean and conditions 🟢 🔴

Let's move on to a new type called **Bool**. <br/>
This type is relatively special because it his composed of only two values : **true** and **false**.

次に、**Bool**という新しい型に移りましょう。<br/>
この型は比較的特殊で、2つの値のみから構成される。**true**とfalse**の2つの値で構成される。

This type is often used with **if condition** to add conditions to your function.

この型は、しばしば**if条件**と一緒に使用され、関数に条件を追加するために使用されます。

```
if(true) {
    // Do this
} else {
    // Do that
};

```

Now let me introduce the **equality** operator **==**. <br/>This operator is used to test if two values are equals. It returns a boolean indicating **true** or **false**.
We can actually combine the **==** operator with the **if condition**.

ここで、**均等**演算子*==*を紹介します。<br/>この演算子は、2つの値が等しいかどうかをテストするために使用されます。これは、**true** または **false** を示すブーリアン値を返します。
実際には、**==**演算子と**if条件**を組み合わせることができます。

```
if(1 == 1) {
    return ("Hello");
} else {
    return ("Ola");
};
```

❓ What do you think this expression will return ? この式は何を返すと思いますか？

It will return **Hello** indeed. <br/>
The condition 1 == 1 is always **true** so this expression is not extremly interesting. <br/> <br/> Let's move to something else and introduce variables into our condition.

確かに **Hello** が返ってきます。<br/>
1 == 1 という条件は常に **true** なので、この式はあまり面白くありません。<br/> <br/> では、他の条件に移って、変数を導入してみましょう。


```
actor {
    public func equal_to_one (n : Nat) : async Text {
        if(n == 1) {
            return("n is equal to 1 !");
        } else {
            return ("n is not equal to 1 !");
        };
    };
};

```

We can actually test our function by deploying our actor and calling this function with different parameters.

実際にアクターをデプロイして、この関数を異なるパラメータで呼び出すことで、関数をテストすることができます。

```
dfx canister call hello equal_to_one '(1)'
("n is equal to 1 !")
```

```
dfx canister call hello equal_to_one '(2)'
("n is not equal to 1 !")
```

Let me introduce other **relational operators** :
その他の**関係演算子**を紹介しよう。

- The **<** (less than) operator.
- **<** (less than) 演算子.
  ```
  3 < 5     //true
  6 < 2     //false
  1 < 1     //false
  ```
- The **>** (more than) operator.
- **>** (more than) 演算子.
  ```
  3 > 5     //false
  6 > 2     //true
  1 > 1     //false
  ```
- The **<=** (less than or equal to) operator.
- The **<=** (less than or equal to) 演算子.
  ```
  3 <= 5    //true
  6 <= 2    //false
  1 <= 1    //true
  ```

- The **>=** (more than or equal to) operator.
- **>=** (more than or equal to) 演算子.
  ```
  3 >= 5    //falser
  6 >= 2    //true
  1 >= 1    //true
  ```
- The **!=** (not equal) operator.
- **!=** (not equal) 演算子.
  ```
  1 != 1    //false
  1 != 0    //true
  ```

We can use some of those new operators to rewrite our actor.

それらの新しい演算子のいくつかを使って、アクターを書き換えることができる。

```
actor {
    public func inf_to_one (n : Nat) : async Text {
        if(n < 1){
            return("n is below 1 !");
        };
        if( n > 1){
            return("n is above 1 !");
        } else {
            return("n is equal to 1!");
        };
    };
};

```

You now have the mission to deploy this actor and test this function for different values. 😉

このアクターを配備し、異なる値でこの機能をテストする使命があります。

# Challenge 🎮

Take a break and try completing challenge 5 and 6.

一息ついて、チャレンジ5と6のクリアに挑戦してください。

# Array 配列 🗃

In Motoko, an **array** is a collection of **similar** data elements.

Motokoでは、**配列**は**類似の**データ要素の集まりです。

```
let array_1 : [Text] = ["Motoko", "is", "a", "great", "language", "."];

let array_2 : [Nat] = ["05", "07", "2021"];

let array_3 = ["This is not correct", 12345];   ⛔️ Not valid
```

As you can see array_3 is not valid; we are trying to mix a value of type Text with a value of type Nat. <br/> Again, an array can only contains elements of the similar type.

Text 型の値と Nat 型の値を混在させようとしているのです。<br/>繰り返しになりますが、配列には同じ型の要素しか入れられません。

🕵️‍♂️ To access an element in an array we use an **index**. <br/> Array are indexed starting at zero. This means the first element in the array can be accessed using **array[0]**, the second element using **array[1]** and so on.
<br/> <br/> You can access the size of an array using **array.size()**.

🕵️‍♂️  配列の要素にアクセスするには、**インデックス**を使用します。<br/>配列は0から始まるインデックスを持ちます。つまり、配列の最初の要素には **array[0]** を、2番目の要素には **array[1]** を使ってアクセスすることができ、以下同様です。
<br/> <br/>配列のサイズにアクセスするには、 **array.size()** を使用します。

Let's rewrite our actor and play with what we've learned.

学んだことを活かして、役者を書き換えて遊ぼう。


```
actor {

    let array : [Text] = ["Motoko", "is", "a", "great", "language", "."];

    public func check_index(n : Nat) : async Text {
        return(array[n]);
    };

    public func check_size() : async Nat {
        returrn(array.size());
    };
};
```

💡 Note that the function check_size has no argument.
💡 関数 check_size には引数がないことに注意してください。

<br/>

❓ What do you think this command will return ?

❓ このコマンドは何を返すのでしょうか？


```
dfx canister call hello check_size '()'
```

❓ What about this one ?

❓ これはどうですか？

```
dfx canister call hello check_index '(6)'
```

✅ The first command will return **6** the second one should report a **trap** error indicating than the index is out of the bounds of the Array.

✅ 最初のコマンドは **6** を返し、2番目のコマンドはインデックスが配列の範囲外であることを示す **trap** エラーを報告するはずです。
を報告する。

# Loop ループ ⏭

We can loop over an array using a **for** loop and the following syntax.
Copy and paste the following code and deploy the actor.

for**ループと次の構文を使って、配列の上をループすることができます。
以下のコードをコピー＆ペーストして、アクターをデプロイしてください。

```
import Debug "mo:base/Debug";

actor {
    let array : [Nat] = [1, 2, 3, 4, 5];

    public func test() : async () {
        for (value in array.vals()){
            Debug.print(debug_show(value))
        };
    };
};

```

This syntax means that we will go trough all values in the array and print them.
Once you've deployed the actor, run the following command.

この構文は、配列内のすべての値を調べて表示することを意味します。
アクターをデプロイしたら、以下のコマンドを実行します。

```
dfx canister call hello test '()'
```

In your terminal (in the window that is running the replica) you should see this output.

ターミナル（レプリカを実行しているウィンドウ）で、次のような出力が表示されるはずです。

<p align="center"> <img src="img/terminal.png" width="800"/> </p>

# Challenge 🎮

Take a break and try completing challenge 7 and 8.

一息ついて、チャレンジ7、8のクリアに挑戦してください。

# Module 🧩

As you've probably noticed in the previous actor declaration, we have imported a **module** (called **Debug**). <br/>

先ほどのアクター宣言でお気づきかと思いますが、**モジュール**（*Debug**という名前）をインポートしています。

A module is composed of code written by someone else that you can use in your own program. <br/>
We will see different ways to import modules and even how to create your own modules.
However, for today we only need to know how to import modules from the **base library**.

モジュールとは、他の人が書いたコードを自分のプログラムで使用できるようにしたものです。<br/>
モジュールをインポートするさまざまな方法と、独自のモジュールを作成する方法について見ていきます。
しかし、今日のところは **ベースライブラリ** からモジュールをインポートする方法だけ知っていればよいのです。

💡 The **base library** is a set of modules to handle common operations on the most used types (Array, Bool, Nat, Int, Text...).

💡 **基本ライブラリ**は、最もよく使われる型（Array, Bool, Nat, Int, Text...）に対する共通の操作を扱うためのモジュール群です。


- The **source code** for this library is accessible <a href="https://github.com/dfinity/motoko-base" target="_blank"> here </a> and is maintained by engineers from the Dfinity foundation and community members.
- このライブラリの**ソースコード**は、<a href="https://github.com/dfinity/motoko-base" target="_blank">こちら</a> からアクセスでき、Dfinity財団のエンジニアとコミュニティメンバーによって維持されています。
  <br/>

- Each module has a **documentation** page where you can read about the available functions. Here is the documentation page for the <a href="https://smartcontracts.org/docs/base-libraries/Text.html" target="_blank"> Text </a> module.
- 各モジュールには **ドキュメント** ページがあり、利用可能な関数について読むことができます。ここでは、<a href="https://smartcontracts.org/docs/base-libraries/Text.html" target="_blank">Text</a> モジュールのドキュメント・ページを紹介します。


The **source code** is meant to understand how a specific module was written whereas the **documentation** is meant to understand how you can use a module. <br/> You need to know how to use the **documentation** but you don't need to understand how the **source code** for these modules was written (expect if you are curious 👀).

**ソースコード** は特定のモジュールがどのように書かれたかを理解するためのものであり、**ドキュメンテーション** はそのモジュールをどのように使うことができるかを理解するためのものです。<br/>ドキュメント**の使い方を知る必要はありますが、これらのモジュールの**ソースコード**がどのように書かれたかを理解する必要はありません（興味がある人は別ですが👀）。

Here's an example that show how to import the <a href="https://smartcontracts.org/docs/base-libraries/Nat.html" target="_blank"> **Nat** </a> module and use the **toText** function.

以下は、<a href="https://smartcontracts.org/docs/base-libraries/Nat.html" target="_blank"> **Nat** </a>> モジュールをインポートして、**toText**関数を使用する例です。


```
import Nat "mo:base/Nat";

actor {
    public func nat_to_text(n : Nat) : async Text {
        return(Nat.toText(n));
    };
};
```

Here's the part of the documentation covering the function used.

以下は、使用した関数に関するドキュメントの部分です。

<p align="center"> <img src="img/text.png" width="800"/> </p>

💡 At this point you might be wondering how we were using the type **Nat** in previous examples without importing the corresponding module. <br/> <br/>This is an important subtility to understand : the **_type_** Nat is by default available in Motoko but if you need to use one function from the **_module_** Nat you need to import the module before.

💡 ここで，これまでの例で，どのようにして対応するモジュールをインポートせずに **Nat** という型を使用していたのか，不思議に思うかもしれません．<br/><br/>これは理解すべき重要な点です： **_type_** Nat は Motoko でデフォルトで利用可能ですが、 **_module_** Nat の関数を使用する必要がある場合、事前にモジュールをインポートする必要があります。

```
actor {
    let a : Nat = 5; ✅ Valid.
    public func nat_to_text(n : Nat) : async Text {
        return(Nat.toText(n)); ⛔️ Incorrect without importing the module.
    };
};

```

# Challenge 🎮

Take a break and try completing challenge 9 and 10.

一息ついて、チャレンジ9、10をクリアしてみてはいかがでしょうか。
