# Daily guide : day 2 🐣

Welcome into the **day 2** of the Motoko Bootcamp ! <br/>
Today we will cover the following topics : **Binary**, **Nat 8**, **Char** and **Text**.

Motoko Bootcamp の **day 2** へようこそ! <br/>
本日は、以下のトピックを取り上げます : **Binary**, **Nat 8**, **Char** and **Text**. 

# Prerequisites 前提条件✅

- Before taking on this lesson I **strongly** recommend watching this introduction to Computer Science from Harvard : https://www.youtube.com/watch?v=1tnj3UCkuxU
  <br/> <br/> You should start the video from the beggining and watch until **35:40** (I recommend watching the whole video if you can but the most important topics related to this lesson are covered in the first part of the video).
- このレッスンに参加する前に、ハーバード大学のコンピューターサイエンスの紹介を見ることを **強く** お勧めします : https://www.youtube.com/watch?v=1tnj3UCkuxU
  <br/> <br/>ビデオは最初から始めて、**35:40**まで見てください（できれば全部見ることをお勧めしますが、このレッスンに関連する最も重要なトピックは、ビデオの最初の部分でカバーされています）。

- Make sure have dfx installed on your machine.
- お使いのマシンにdfxがインストールされていることを確認してください。

  ```
  dfx --version
  ```

- Start a new project called **day_2** and turn on your local replica.
- 新しいプロジェクト **day_2** を開始し、ローカルのレプリカをオンにします。

  ```
  dfx new day_2
  cd day_2
  dfx start
  ```

# Decimal 🔢

Decimal is a base-10 **number system**, which uses ten digits (0 to 9), this is the primarly systems used by humans (probably because we have 10 fingers to count).

10 進法は、10 桁（0〜9）の数字を使う基本 10 進法で、人間が主に使う数字です（人間には数えるための指が10本あるからでしょう）。

<p align="center"> <img src="img/decimal_system.jpeg" width="400"/> </p>

In the decimal system, once you've reached the last digit (which is 9), you add a new digits and restart counting from 0 at the right-most digit.

10進法では、最後の桁（9）に到達したら、新しい桁を追加して、一番右の桁の0から数え直します。

    0 1 2 3 4 5 6 7 8 9 ... wait I don't have any digits anymore ? 😧

    10 11 12 .... 99 wait I don't have any digits anymore ?  😧

    0 1 2 3 4 5 6 7 8 9 ...待てよ、もう桁がないんだけど？😧

    10 11 12 .... 99 待って......もう1桁もないんだけど？ 😧

Each digit represents a **power** of 10.
各桁は10の**乗**を表します。

1234 = 1 x 1000 + 2 x 100 + 3 x 10 + 4 x 1 = 1 x 10 <sup>3</sup> + 2 x 10 <sup>2</sup> + 3 x 10 <sup>1</sup>+ 4 x 10 <sup>0</sup>.

# Binary 🟢 🔴

Binary is a base-2 **number system**, it only uses two digits (0 and 1). <br/> This is the system used at the heart of all computers : every number, every character, every image, every video is encoded as binary for a computer.

2進法は、2桁の数字（0と1）だけを使用する基本2進法です。<br/>すべてのコンピュータの心臓部で使用されているシステムです。すべての数字、文字、画像、動画は、コンピュータのために2進数としてエンコードされています。

💡 Using two digits is not a random choice. <br/> Computers are built using **transistors** which are tiny little door that can be closed or open to let electricity flow. ⚡️

💡 2桁の数字を使うのは、無作為の選択ではありません。<br/>コンピュータは、**トランジスタ**という、電気を流すために閉じたり開いたりできる小さな小さなドアを使って作られています。⚡️

- 0 means the gate is closed and there is no electricity flowing 🔴
- 0はゲートが閉まっていて電気が流れていないことを意味します🔴。
- 1 means the gate is open and there is electricity flowing 🟢
- 1はゲートが開いていて電気が流れていることを意味します🟢。

This is how you **count** in binary.<br/> Notice that everytime you run of digits (when you reach 1 actually), you increase by 1 on the left and restart counting from 0 at the right most digit.

これが2進法での **数え方** です。<br/>桁が足りなくなるたびに（実際には1になるときに）、左から1ずつ増えていき、一番右の桁で0から数え始めることに注意してください。

💡 The method to count is the same as in the decimal system it's just that instead of havings 10 digits we only use 2 digits <br/>
💡数え方は10進法と同じで、10桁の代わりに2桁を使うだけです。<br/>

<table style="min-width:500px;font-size:1em">
			<tbody><tr>
				<td>Decimal</td>
				<td>Binary</td>
			</tr>
			<tr>
				<td>0</td>
				<td>0000</td>
			</tr>
			<tr>
				<td>1</td>
				<td>0001</td>
			</tr>
			<tr>
				<td>2</td>
				<td>0010</td>
			</tr>
			<tr>
				<td>3</td>
				<td>0011</td>
			</tr>
			<tr>
				<td>4</td>
				<td>0100</td>
			</tr>
			<tr>
				<td>5</td>
				<td>0101</td>
			</tr>
			<tr>
				<td>6</td>
				<td>0110</td>
			</tr>
			<tr>
				<td>7</td>
				<td>0111</td>
			</tr>
			<tr>
				<td>8</td>
				<td>1000</td>
			</tr>
			<tr>
				<td>9</td>
				<td>1001</td>
			</tr>
			<tr>
				<td>10</td>
				<td>1010</td>
			</tr>
			<tr>
				<td>11</td>
				<td>1011</td>
			</tr>
			<tr>
				<td>12</td>
				<td>1100</td>
			</tr>
			<tr>
				<td>13</td>
				<td>1101</td>
			</tr>
			<tr>
				<td>14</td>
				<td>1110</td>
			</tr>			
			<tr>
				<td>15</td>
				<td>1111</td>
			</tr>
</tbody></table>

This time each digit represents a **power** of 2.

このとき、各桁は2の**乗**を表します。

1110 = 1 x 2<sup>3</sup> + 1 x 2<sup>2</sup> + 1 x 2<sup>1</sup> + 1 x 2<sup>0</sup> = 1 x 8 + 1 x 4 + 1 x 2 + 0 x 1 = 8 + 4 + 2 = 14

(You can check the table : 1110 is indeed the **binary representation** of 14) !

(表で確認できます：1110は14の **バイナリ表現 **です）！

# Nat 8

In Motoko, there is a type called <a href="https://smartcontracts.org/docs/base-libraries/Nat8.html" target="_blank"> **Nat 8** </a>. This type is different from the type <a href="https://smartcontracts.org/docs/base-libraries/Nat8.html" target="_blank"> **Nat** </a> that we've used on Day 1.
Motokoには、<a href="https://smartcontracts.org/docs/base-libraries/Nat8.html" target="_blank">**Nat 8**</a> という型があります。このタイプは、1日目に使用した <a href="https://smartcontracts.org/docs/base-libraries/Nat8.html" target="_blank">**Nat**</a> というタイプとは異なります。


💡 8-bits is also called a **byte**. This is a term that is often used make sure to remember it.
💡 8ビットは **byte** とも呼ばれます。よく使われる言葉なので、しっかり覚えておきましょう。


**Nat 8** uses only 8-bits to represent numbers. <br/> This means you can use this type to represent any number with a binary representation between 00000000 and 11111111.

**Nat 8**は8ビットだけで数字を表現します。つまり、この型を使って、00000000から11111111の間の2進数表現を持つ任意の数を表現することができます。

 <details>
        <summary style="color:green"> 🤔 What is the number represented by 11111111 ? 🤔 11111111で表される数字は何でしょう？</summary>
         11111111 = 1 x 2 <sup>7</sup>  + 1 x 2 <sup>6</sup> + 1 x 2 <sup>5</sup> + 1 x 2 <sup>4</sup> + 1 x 2 <sup>3</sup> + 1 x 2 <sup>2</sup> + 1 x 2 <sup>1</sup> +  + 1 x 2 <sup>0</sup> = 1 x 128 + 1 x 64 + 1 x 32 + 1 x 16 + 1 x 8 + 1 x 4 + 1 x 2 + 1 x 1 = <strong> 255 </strong>.
		 <br/> <br/>
		 <p> The maximum number we can represent with the type Nat8 is 255. </p>
                 <p> Nat8型で表現できる最大の数値は255です。</p>
    </details>
	<br/>

Copy and paste the following actor declation and try deploying the actor.

以下のアクター宣言をコピー＆ペーストして、アクターのデプロイを試してみてください。


```
actor {

  let a : Nat8 = 256;

};
```

You will get this error. Again this is because there is no way to represent the number 256 with only 8 bits !

こんなエラーが出ます。これも、256という数字を8ビットで表現する方法がないからです。

```
type error [M0048], literal out of range for type Nat8
```

You can always convert a **Nat 8** to a **Nat** using the following code.

以下のコードを使用すれば、いつでも**Nat 8**を**Nat**に変換することができます。


```
import Nat8 "mo:base/Nat8";

actor {

    public func nat8_to_nat(n : Nat8) : async Nat {
      return(Nat8.toNat(n));
    };

};
```

In Motoko there are also the types : **Nat 16**, **Nat 32** and **Nat 64**. <br/> Those are similar types to **Nat 8** expect they use respectively 16-bits, 32-bits and 64-bits, so they can represent way larger numbers.

Motoko には、以下の型もあります : **Nat 16**, **Nat 32** and **Nat 64**<br/> これらは、**Nat 8**と似たような型ですが、それぞれ16ビット、32ビット、64ビットを使用するので、より大きな数を表現することができます。

 <details>
        <summary style="color:green"> 🤔 What is the maximum number represented by Nat32 ? 🤔 Nat32で表される最大の数は何でしょうか？</summary>
		<br/>
		 <p> The maximum number we can represent with the type Nat32 is 4,294,967,295. Nat32型で表現できる最大数は4,294,967,295である。</p>
    </details>
<br/>

The **Nat** type is unbounded, there is no upper limit to the maximum value it can represents. <br/>
Nat** 型は unbounded であり、表現できる最大値に上限はない。<br/>
You might be wondering why do we use **Nat 8/16/32/64** if we can always use **Nat** instead ? <br/>
なぜ、**Nat 8/16/32/64**を使うのだろうかと疑問に思うかもしれません。<br/>

This is for memory and efficiency reasons, the less bits we take to represent a number the more memory we save, and memory is expensive ! <br/> <br/>
If you know with assurance that your number will stay in a certain range (maybe because it's a constant) you can use the corresponding type to save memory. However if you have any doubt (because the value might change during your program execution) use a **Nat** and you will be safe.

これはメモリと効率のためで、数値を表現するビットが少ないほどメモリを節約できますし、メモリは高価です <br/> <br/>
もし、数値がある範囲に収まることが確実に分かっている場合（定数だからかもしれません）、メモリを節約するために対応する型を使用することができます。しかし、（プログラムの実行中に値が変わるかもしれないので）少しでも疑問がある場合は、**Nat**を使えば安全です。


# Challenge 課題🎮

Take a break and try completing challenge 1 to 3.

一息ついて、チャレンジ1～3をクリアしてみてください。

# Unicode & ASCII 📚

Now that you've understood that we can represent any number using binary, you might be wondering : what about letters and characters ? 🤔

どんな数字も2進数で表現できることが理解できたと思いますが、ここで気になるのが : 文字やキャラクターはどうなる？🤔

We can decide to associate any character with a number and then encode the number as we've seen in the previous paragraph. <br/>
Let's say we decide to encode **A** with the number **65**. This is how it would be converted to binary.

前項で見たように、任意の文字と数字の関連付けを決めて、その数字を符号化すればよいのです。<br/>
例えば、**A** を**65** という数字でエンコードすることにしたとします。これを2進数に変換すると、このようになります。

**A** --> **65** --> **01000001**.

We could use this method for all characters, we just need to associate each character that we use with a different number.

この方法はすべての文字に使えるので、使用する文字ごとに異なる番号を関連付けるだけでよいのです。

Luckily we don't need to create our standard because we already have something called **ASCII** (American Standard Code For Information Interchange) : this is the first standard that was used to encode characters. Here's a table which associate characters with their representation.

幸いなことに、私たちは独自の規格を作る必要はありません。すでに **ASCII** (American Standard Code For Information Interchange) というものがあり、これは文字をエンコードするために使われた最初の規格です。ここに、文字とその表現を関連付けた表があります。

<br/>
<br/>

<p align="center"> <img src="img/ascii.png" width="600"/> </p>

**Capital letters** (A,B,C ... Z) are represented by decimals numbers starting from 65 to 90. <br/>
****大文字**（A,B,C ... Z）は、65から90までの10進数で表します。
**Small letters** (a,b,c ... z) are represented by decimals from 97 to 122. <br/>
**小さな文字**（a,b,c ... z）は、97から122までの小数で表します。<br/>

💡 Notice that **numbers** from 0 to 9 are also represented from 48 to 59. This simply means the textual version of those numbers are represented using another number.

💡 0から9までの数字**は、48から59までの数字でも表現されることに注意してください。これは単に、それらの数字のテキスト版が、別の数字を使って表現されていることを意味します。

ASCII is an american standard that uses only 7-bits : it can encode only 128 characters. <br/> This is fine for most English character, numbers and punctuations but this is pretty limited. <br/> <br/>
We have since moved to **Unicode** which is, to put it short, an improved version of ASCII, that also takes into account characters from other languages, emojis... but even using Unicode (which is what is used in Motoko), ASCII table are still valid (this is because Unicode is compatible with ASCII).

ASCIIはアメリカの標準規格で、7ビットしか使わないので、128文字しかエンコードできません。<br/>これは、ほとんどの英字、数字、句読点には適していますが、かなり限定的です。<br/><br/>
その後、**Unicode**に移行しましたが、これは簡単に言うと、ASCIIの改良版で、他の言語の文字や絵文字も考慮されています...が、Unicodeを使用しても（Motokoではこれを使用）、ASCIIテーブルは有効です（これはUnicodeがASCIIと互換性があるからです）。

# Char & Text 💬

A value of type **Text** is composed of multiples **Char**.

Text** 型の値は、複数の **Char** で構成されます。

```
let a : Text = "Hello";
let b : Char = 'c';
```

Char values are delimited using **' '** whereas we use **" "** for Text.
You can loop through all characters of a Text value using **.chars()** as in the following expression :

文字列は **' '** で区切られますが、文字列には **" "** を使用します。
以下の式のように、**.chars()** を使用すると、Text値のすべての文字をループすることができます。

```
let a : Text = "Motoko bootcamp";
for(char in a.chars()){
	//Do something
};
```

You can also access the size (number of characters) of a Text value using **.size()** <br/>

また、Text値のサイズ（文字数）は、**.size()** を使ってアクセスすることができます。 <br/>

```
actor {
	// Return the number of characters in the text
	public func number_characters(t : Text) : async Nat {
		return(t.size());
	};
};

```

You can also concatenate multiples values of type Text together using the concatenation operator : **#**.

また、連結演算子を使って、Text型の複数の値を連結することもできます。: **#**.


```
let a : Text = "Hello";
let b : Text = "World";
let c : Text = a # " " # b; // "Hello World"

```

Finaly let's take a brief look at what Unicode looks in practice. Copy and paste this actor declaration and deploy it on your local replica.

最後に、Unicodeが実際にどのように見えるか、簡単に見てみましょう。このアクター宣言をコピー＆ペーストして、ローカル・レプリカにデプロイしてください。

```

import Char "mo:base/Char";
actor {
    //	Return the character corresponding to the unicode value n.
    public func unicode_to_character(n : Nat32) : async Text {
    	let char : Char = Char.fromNat32(n);
    	return(Char.toText(char));
    };
};

```

 <details>
        <summary style="color:green"> 🤔 What should the command : <strong> dfx canister call day_2 unicode_to_character '(63)' </strong> return ? 🤔 コマンド : <strong> dfx canister call day_2 unicode_to_character '(63)' </strong> は何を返すべきなのでしょうか？</summary>
		<br/>
		 <p> Looking at the ASCII table : the decimal number 63 corresponds to the encoding of the character  <strong> ? </strong>. This is what the command will return (try it!) </p>
ASCII表を見ると、10進数で63が文字 <strong>?</strong> のエンコーディングに相当します。これはコマンドが返すものです (試してみてください!)
    </details>
<br/>

# Challenge

Take a break and try completing challenge 4 to 6.

一息ついて、チャレンジ4～6をクリアしてみてはいかがでしょうか。

# Candid & WebAssembly 🧑‍🔬

If you take a close look at the previous actor declaration you might be wondering why we needed to convert the **char** value to a **Text** type on the last line, if the goal was only to get a character from an unicode value why not directly return it ?

前のアクター宣言をよく見ると、なぜ最後の行で **char** 型の値を **Text** 型に変換する必要があるのか、ユニコード値から文字を取得することだけが目的なら、なぜそれを直接返さないのかと思うかもしれませんね？

Let's try it out. Copy and paste the following actor declaration and deploy it on your local replica.

試してみましょう。以下のアクター宣言をコピー＆ペーストして、ローカルレプリカにデプロイしてください。

```
import Char "mo:base/Char";
actor {
    //	Return the character corresponding to the unicode value n.
    public func unicode_to_character(n : Nat32) : async Char {
    	let char : Char = Char.fromNat32(n);
    	return(char));
    };
};
```

This code is totally valid... but you might be surprised at what the following command will return

このコードは完全に有効です...しかし、次のコマンドが返す内容には驚くかもしれません。

```
dfx canister call day_2 unicode_to_character '(63)'
(63 : nat32)
```

Why are we getting a value of type **Nat 32** when we the return type of the function is **Char** ?

関数の戻り値の型は **Char** であるのに、なぜ **Nat 32** 型の値が返されるのですか？

To answer this question : we need to take a step back and explain severals things before.

この問いに答えるには、一歩下がって、いくつかの事柄を説明する必要があります。

- Contrary to what you might believe : the language that is powering canisters on the Internet Computer is **not** Motoko. You've been lied to. <br/> Motoko is used to compile (translate) your code into another language called **Web Assembly** (WASM) which is what is ultimately deployed on the IC. <br/> <br/>
- インターネットコンピュータのキャニスターを動かしている言語は、Motoko ではありません。あなたは騙されているのです。Motokoは、あなたのコードを**Web Assembly** (WASM)と呼ばれる別の言語にコンパイル（翻訳）するために使われ、最終的にIC上に配置されるものです。
- Web Assembly is a **low level** language. We have said earlier that the machine only understand binary but we do not write code in binary, we use different languages of programmation (Motoko, Rust, Javascript, C, Java ...) those languages are **high level**, this means their are closer to a human language than machine instructions.
- Webアセンブリは **低レベル** の言語です。機械はバイナリしか理解できないと言いましたが、私たちはバイナリでコードを書きません。私たちはさまざまなプログラミング言語（Motoko、Rust、Javascript、C、Javaなど）を使っていますが、これらの言語は**高レベル**で、機械語よりも人間の言語に近いということです。

<p align="center"> <img src="img/language.png" width="400"/> </p>

- A canister is similar to a container that contains the code and memory for your program : all canisters whether they were written in Motoko, in Rust or in another language are ultimately Web Assembly module.
- キャニスターは、プログラムのコードとメモリを格納する容器に似ています。Motoko、Rust、その他の言語で書かれたキャニスターは、最終的にWeb Assemblyモジュールになります。

<p align="center"> <img src="img/canister.png" width="400"/> </p>

- We need a way to being able to communicate between canister and applications written in differents languages. Let's imagine you are writting your code in Motoko and you want to be able to send a message to a canister written in Rust, how do you know how to communicate with this canister ? <br/> This is exactly like trying to speak Spanish to someone that is expecting to listen to Chinese 🇪🇸 🇨🇳. <br/>
- キャニスターと異なる言語で書かれたアプリケーションの間で通信できる方法が必要です。例えば、あなたがMotokoでコードを書いていて、Rustで書かれたcanisterにメッセージを送れるようにしたいとしましょう。<br/>これはまさに、中国語 を期待している人にスペイン語を話そうとするようなものです 🇪🇸 🇨🇳 。<br/>

- On the Internet Computer we have a **common** language 🌍 : it's called **Candid**. This is an **interface description language (IDL)** : it's primary purpose is to describe the interface of a canister so everyone knows what to expect from this canister. Here's what it looks like for a simple **counter**.
- インターネット・コンピュータには、**共通**言語🌍があります：それは**Candid**と呼ばれています。これは **インターフェース記述言語(IDL)** で、その主な目的はキャニスターのインターフェースを記述することで、誰もがこのキャニスターから何を期待すればよいかを知ることができます。以下は、単純な**カウンタ**のためのものです。

<p align="center"> <img src="img/candid.png" width="600"/> </p>

As you can see, it describes the function you can access (the **public** function in Motoko) and the type of parameters and return values.

ご覧のように、アクセスできる関数（Motokoでは**public**関数）と、パラメータと戻り値の型が記述されています。

- When you are using dfx to talk to a canister you are specifying values in a Candid format, the answer is also in Candid format.
- dfxを使用してキャニスターと対話する場合、Candid形式で値を指定しますが、その答えもCandid形式です。


```
dfx canister call day_2 unicode_to_character '(63)' <- Candid
```

Although Candid types and Motoko types are quite close, they are not the same. <br/>
In Candid there is no **Char** type, this type only exists within the Motoko code. For Candid a **Char** is abstracted as a **nat32**.

Candid 型とモトコー型はかなり近いのですが、同じではありません。<br/>
Candid には **Char** という型はなく、この型はMotokoのコード内にのみ存在します。キャンディッドでは **Char** は **nat32** として抽象化されています。

```
actor {
	public func test() : async Char {
		return('1');
	};
};
```

This is why the previous actor declaration, once deployed will return the following.

このため、先ほどのアクター宣言は、デプロイすると次のように返されます。

```
dfx canister call day_2 test '()'
(49 : nat32)
```

The '1' **Char** in Motoko is equivalent to the 49 **nat 32** of Candid (due to the Unicode representation of 1).

Motoko の '1' **Char** は Candid の 49 **nat 32** に相当します (1 の Unicode 表現による)。

# Challenge 🎮

Take a break and try completing challenge 7 to 10.

一息ついて、チャレンジ7～10をクリアしてみてください。
