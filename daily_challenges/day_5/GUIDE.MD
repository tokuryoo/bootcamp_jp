# Daily guide : day 5 🦆

Welcome into the **day 5** of the Motoko Bootcamp ! <br/>
Motoko Bootcamp の **day 5** へようこそ!<br/>

Today we will cover the following topics : **Principal**, **Hashmap**, **Cycles** (how to deal with upgrades) & **stable variables**.

本日は、以下のトピックを取り上げます。: **Principal**, **Hashmap**, **Cycles**（アップグレードの対処法）と **stable** について説明します。

You can access the official documentation for each topic.

各トピックの公式ドキュメントにアクセスすることができます。

- <a href="https://smartcontracts.org/docs/language-guide/caller-id.html" target="_blank"> Principal </a>.
- <a href="https://smartcontracts.org/docs/base-libraries/HashMap.html" target="_blank"> Hashmap </a>.
- <a href="https://smartcontracts.org/docs/language-guide/upgrades.html" target="_blank"> Stable variables & upgrade </a>.
- <a href="https://smartcontracts.org/docs/developers-guide/concepts/tokens-cycles.html" target="_blank"> Cycles </a>.

# Prerequisites 前提条件 ✅

- Make sure you have dfx installed on your machine.
- お使いのマシンにdfxがインストールされていることを確認してください。

  ```
  dfx --version
  ```

- Before reading this guide I recommend watching those two lectures.
- このガイドを読む前に、この2つの講義を見ることをお勧めします。

  - Create, Read, Upgrade & Delete & Hashmap. (entire lecture)
  - 作成、読み込み、アップグレード、削除、ハッシュマップ（全講義）。
  - Cycle managament (TODO : ADD TIME)
  - サイクルマネージメント（TODO : 時間を追加）

# Principal 🆔

The notion of **Principal** is specific to the Internet Computer. <br/> A principal is a unique identifier fo all entities on the IC

**Principal** という概念は、Internet Computer に特有のものである。<br/>
Principal とは、IC 上のすべてのエンティティを一意に識別するものである。


- A canister has it's own principal (which corresponds to the canister id)
- Each user has it's own principal.
- Your wallet has it's own principal.
- キャニスタは独自のプリンシパルを持ちます (これはキャニスタ ID に対応します)。
- 各ユーザは独自のプリンシパルを持ちます。
- あなたの財布は独自のプリンシパルを持っています。

You can access the principal of your dfx identity running the following command.

以下のコマンドを実行することで、dfx IDのプリンシパルにアクセスすることができます。

```
dfx identity get-principal
ubetf-42t5l-l64h6-ljrqr-6ztbu-tanvs-jrwiv-a45x4-ucoxp-cqr4i-mqe //My dfx principal
```

<p align="center"> <img src="img/plug.png" width="400"/> </p>

Here we also have a principal.
ここでは、プリンシパルもあります。

Each message on the IC contains the information about the principal of the caller.
You can access this information in Motoko with the following syntax.

IC上の各メッセージには、発呼側のプリンシパルに関する情報が含まれています。
Motokoでは、以下の構文でこの情報にアクセスすることができます。

```
public shared(msg) func whoami() : async Principal {
    let principal_caller = msg.caller;
    return(principal_caller);
};
```

The principal is accessible using msg.caller.
You can also use this syntax.

プリンシパルは msg.caller を使ってアクセスできます。
また、この構文も使用できます。

```
public shared({caller}) func whoami() : async Principal {
    return(caller);
};
```

On the Internet Computer there is a special principal, it's called the **Anonymous** principal.
The textual version of this principal is **2vxsx-fae**. It corresponds to any user that is not authenticated.

Internet Computer には特別なプリンシパルがあり、それは **Anonymous** プリンシパルと呼ばれています。
このプリンシパルのテキストバージョンは、**2vxsx-fae** です。これは、認証されていないすべてのユーザーに対応します。

Finally, in Motoko there is a <a href="https://smartcontracts.org/docs/base-libraries/Principal.html" target="_blank"> **Principal** </a> module for basic operations on principals.

最後に、Motoko には、プリンシパルに対する基本的な操作を行うための <a href="https://smartcontracts.org/docs/base-libraries/Principal.html" target="_blank"> **Principal** </a> モジュールが用意されています。

# Challenge 🎮

Take a break and try completing challenge 1.

一息ついて、チャレンジ1をクリアしてみてはいかがでしょうか。

# HashMap 🗝

An HashMap is a **key** / **value** store that allow you to store elements of type **value** and later retrieve them using an element of type **key**.
Usually, we note the type of the keys : **K** & the type of the values : **V**.

HashMap は、**key** / **value** 型のストアで、**value** 型の要素を保存し、後で **key** 型の要素を使用してそれらを取得することができるものである。
通常、キーの型は**K**と表記します。値の型は **V** と表記します。

You can create an HashMap and use it by importing the **HashMap** module (don't forget the capital M). <br/>
This is how you would instantiate your first HashMap, with **Keys** of type **Principal** and value of type **Name**.

HashMap を作成し、それを使用するには、**HashMap** モジュールをインポートします（大文字のMを忘れないでください）。
これは、最初のHashMapをインスタンス化する方法で、**Keys** は **Principal** 型で、valueは **Name** 型である。

```
import HashMap "mo:base/HashMap";
import Principal "mo:base/Principal";
actor {

    let anonymous_principal : Principal = Principal.fromText("2vxsx-fae");
    let users = HashMap.HashMap<Principal, Text>(0, Principal.equal, Principal.hash);
    users.put(anonymous_principal, "This is the anonymous principal");

    public func test() : async ?Text {
        return(users.get(Principal.fromText("2vxsx-fae")));
    };


};
```

There is a lot going on. At this point you're probably not surprised by the Motoko syntax : HashMap.HashMap, it simply means that we import the HashMap object from the HashMap module. <br/>

いろいろあるのです。この時点で、Motoko 構文 : HashMap.HashMap には驚かないでしょう。これは、単に HashMap モジュールから HashMap オブジェクトをインポートしていることを意味します。<br/>

Then we have three arguments to instantiate the HashMap.

そして、HashMapをインスタンス化するための3つの引数を用意します。

- 0 corresponds to the initial capacity of the HashMap. The capacity will automatically grow for you everytime you reach the maximum capacity of the HashMap, you don't need to worry about it 🥳.

- 0は、HashMapの初期容量に相当します。HashMapの最大容量に達するたびに、自動的に容量が大きくなるので、心配する必要はありません 🥳。

- Principal.equal is needed to compare the Keys.

- Keyの比較には、Principal.equalが必要です。

- Principal.hash is needed to hash the Keys.

- Principal.hashはKeyをハッシュ化するために必要です。

If you are not familiar with the concept of **hash** and **hash table**, I recommend watching this <a href="https://www.youtube.com/watch?v=KyUTuwz_b7Q" target="_blank"> video </a>.

もし、**ハッシュ**と**ハッシュテーブル**の概念に馴染みがなければ、この<a href="https://www.youtube.com/watch?v=KyUTuwz_b7Q" target="_blank"> ビデオ</a>を見ることをお勧めします。

I really encourage you to understand the inner working of the HashMap, that way you'll get why we need to provide Principal.equal & Principal.hash.

HashMapの内部構造を理解することで、なぜPrincipal.equalとPrincipal.hashを提供する必要があるのかを理解することができます。


Let's move to the pratical application.
You can add values inside the HashMap using the following syntax.

では、実際に応用してみましょう。
HashMapの内部に値を追加するには、以下の構文を使用します。

```
import HashMap "mo:base/HashMap";
import Principal "mo:base/Principal";
actor {

    let anonymous_principal : Principal = Principal.fromText("2vxsx-fae");
    let users = HashMap.HashMap<Principal, Text>(0, Principal.equal, Principal.hash);
    users.put(anonymous_principal, "This is the anonymous principal");

    public func test() : async ?Text {
        return(users.get(Principal.fromText("2vxsx-fae")));
    };

};
```

Here I have added the value **"This is the anonymous principal"** with the **Key** that corresponds to the anonymous principal.
ここでは、値 **"This is the anonymous principal "** と匿名プリンシパルに対応する **Key** を追加しています。

Let's try to retrieve our value.

値を取得してみましょう。

```
import HashMap "mo:base/HashMap";
import Principal "mo:base/Principal";
actor {

    let anonymous_principal : Principal = Principal.fromText("2vxsx-fae");
    let users = HashMap.HashMap<Principal, Text>(0, Principal.equal, Principal.hash);
    users.put(anonymous_principal, "This is the anonymous principal");

    public func test() : async ?Text {
        return(users.get(Principal.fromText("2vxsx-fae")));
    };


};
```

Deploying this actor in the Motoko playground and running the test will return :

このアクタを Motoko プレイグラウンドに配置してテストを実行すると、:

```
(opt "This is the anonymous principal")
```

# Challenge 課題 🎮

Take a break and try completing challenge 2 to 5.

一息ついて、チャレンジ2～5をクリアしてみてください。

# Cycles 💰

Every canister on the Internet Computer consumes **cycles**. Those are used to
measure and pay for **computation** and **storage**. <br/>

Internet Computer のすべてのキャニスターは、**Cycle** を消費しています。これは
**コンピューティング** と **ストレージ** を測定し、料金を支払うために使用されます。<br/>

This is a table summing up the cost of each common operation in cycles.

これは、一般的な各操作のコストをサイクルでまとめた表です。

<table class="tableblock frame-all grid-all stretch">
<caption class="title">Table 1. Cycles Cost per Transaction (as of July 26, 2021)</caption>
<colgroup>
<col style="width: 33.3333%;">
<col style="width: 33.3333%;">
<col style="width: 33.3334%;">
</colgroup>
<thead>
<tr>
<th class="tableblock halign-left valign-top">Transaction</th>
<th class="tableblock halign-left valign-top">Description</th>
<th class="tableblock halign-right valign-top">All Application Subnets</th>
</tr>
</thead>
<tbody>
<tr>
<td class="tableblock halign-left valign-top"><p class="tableblock">Canister Created</p></td>
<td class="tableblock halign-left valign-top"><p class="tableblock">For creating canisters on a subnet</p></td>
<td class="tableblock halign-right valign-top"><p class="tableblock">100,000,000,000</p></td>
</tr>
<tr>
<td class="tableblock halign-left valign-top"><p class="tableblock">Compute Percent Allocated Per Second</p></td>
<td class="tableblock halign-left valign-top"><p class="tableblock">For each percent of the reserved compute allocation (a scarce resource).</p></td>
<td class="tableblock halign-right valign-top"><p class="tableblock">100,000</p></td>
</tr>
<tr>
<td class="tableblock halign-left valign-top"><p class="tableblock">Update Message Execution</p></td>
<td class="tableblock halign-left valign-top"><p class="tableblock">For every update message executed</p></td>
<td class="tableblock halign-right valign-top"><p class="tableblock">590,000</p></td>
</tr>
<tr>
<td class="tableblock halign-left valign-top"><p class="tableblock">Ten Update Instructions Execution</p></td>
<td class="tableblock halign-left valign-top"><p class="tableblock">For every 10 instructions executed when executing update type messages</p></td>
<td class="tableblock halign-right valign-top"><p class="tableblock">4</p></td>
</tr>
<tr>
<td class="tableblock halign-left valign-top"><p class="tableblock">Xnet Call</p></td>
<td class="tableblock halign-left valign-top"><p class="tableblock">For every inter-canister call performed (includes the cost for sending the request and receiving the response)</p></td>
<td class="tableblock halign-right valign-top"><p class="tableblock">260,000</p></td>
</tr>
<tr>
<td class="tableblock halign-left valign-top"><p class="tableblock">Xnet Byte Transmission</p></td>
<td class="tableblock halign-left valign-top"><p class="tableblock">For every byte sent in an inter-canister call (for bytes sent in the request and response)</p></td>
<td class="tableblock halign-right valign-top"><p class="tableblock">1,000</p></td>
</tr>
<tr>
<td class="tableblock halign-left valign-top"><p class="tableblock">Ingress Message Reception</p></td>
<td class="tableblock halign-left valign-top"><p class="tableblock">For every ingress message received</p></td>
<td class="tableblock halign-right valign-top"><p class="tableblock">1,200,000</p></td>
</tr>
<tr>
<td class="tableblock halign-left valign-top"><p class="tableblock">Ingress Byte Reception</p></td>
<td class="tableblock halign-left valign-top"><p class="tableblock">For every byte received in an ingress message</p></td>
<td class="tableblock halign-right valign-top"><p class="tableblock">2,000</p></td>
</tr>
<tr>
<td class="tableblock halign-left valign-top"><p class="tableblock">GB Storage Per Second</p></td>
<td class="tableblock halign-left valign-top"><p class="tableblock">For storing a GB of data per second</p></td>
<td class="tableblock halign-right valign-top"><p class="tableblock">127,000</p></td>
</tr>
</tbody>
</table>

Each canister has it's own cycle balance and can transfer cycles to other canisters through messages. <br/>
In Motoko, you can use the <a href="https://smartcontracts.org/docs/base-libraries/ExperimentalCycles.html" target="_blank"> ExperimentalCycles </a> module to play and experiment with cycles. (This module is likely to be modified in the future).

各キャニスターは独自のサイクルバランスを持ち、メッセージによって他のキャニスターにサイクルを転送することができます。<br/>
Motoko では、<a href="https://smartcontracts.org/docs/base-libraries/ExperimentalCycles.html" target="_blank"> ExperimentalCycles </a> モジュールを使って、サイクルで遊んだり実験したりすることができます。(このモジュールは将来的に修正される可能性があります）。

This is how you can access the balance of a canister.

このようにして、キャニスターの残高にアクセスすることができるのです。

```
import Cycles "mo:base/ExperimentalCycles";
actor {

    public func balance() : async Nat {
        return(Cycles.balance())
    };
};
```

Each message sent on the IC contains a number of cycles attached to it.
You can look the available amount with the following code.

ICで送信される各メッセージには、サイクル数が付加されています。
次のコードで使用可能な量を見ることができます。

```
import Cycles "mo:base/ExperimentalCycles";
actor {

    public func message_available() : async Nat {
        return(Cycles.available())
    };
};
```

If you want to make your users pay in cycles to access a functionality, you can do so.

ある機能を利用するために、ユーザーにサイクル払いをさせたい場合、そのようにすることができます。

```
import Cycles "mo:base/ExperimentalCycles";
actor {

    let AMOUNT_TO_PAY : Nat = 100_000;
    public func pay_to_access() : async Text {
        if(Cycles.available() < 100_000) {
            return("This is not enough, send more cycles.");
        }:
        let received = Cycles.accept(AMOUNT_TO_PAY);
        return("Thanks for paying, you are now a premium user 😎");
    };
};
```

# Challenge 課題

Take a break and try completing challenge 6 & 7.

一息ついて、チャレンジ6＆7をクリアしてみてください。

# Stable variables // Stable変数✏️

By default, when you upgrade a canister you'll will loose all state. 😢 <br/>
Let's say we have a variable called **counter** that been previously incremented; the value of this variable will be reset after an upgrade.
デフォルトでは、キャニスターをアップグレードすると、すべてのステートが失われます。😢<br/>
例えば、**counter**という変数があり、以前はこの変数がインクリメントされていたとします。この変数の値は、アップグレード後にリセットされます。

```
actor {

    var my_name : Text = "";

    public func change_name(name : Text) : async () {
        ny_name := name;
    };

    public func show_name() : async Text {
        return(my_name)
    };

};
```

Here's what you can experiment with this actor (after deployment on the Motoko playground)

このアクターを使った実験を紹介します（Motokoのプレイグラウンドに展開後）。

```
change_name("Motoko");
show_name()  // "Motoko"
```

Now let's try to add something and redeploy our canister, we are trying to run an upgrade.

```
actor {

    var new_value : Text = "Let's upgrade";
    var my_name : Text = "";

    public func change_name(name : Text) : async () {
        my_name := name;
    };

    public func show_name() : async Text {
        return(my_name)
    };


};
```

```
show_name() // ""
```

Looks like the canister has forgotten his name..
Fortunately there is a way to keep state accross upgrades in Motoko. <br/> You can do so with **stable variable** !

キャニスターは自分の名前を忘れたようだ。 幸いなことに、Motokoではアップグレードのたびに状態を保持する方法があります。<br/>
**stable 変数** を使えば可能です。

```
actor {

    stable var my_name : Text = "";

    public func change_name(name : Text) : async () {
        my_name := name;
    };

    public func show_name() : async Text {
        return(my_name)
    };

};
```

If you try the same suite of operations with this actor, you'll notice that the value of the counter is kept accross the upgrade.

このアクターで同じ操作を試すと、カウンターの値がアップグレードの間、保持されていることに気づくでしょう。

Unfortunately only some variables/objects can be defined as stable. <br/> An HashMap for instance, cannot be defined as stable. <br/>

残念ながら，安定と定義できるのは一部の変数/オブジェクトだけです．<br/>
例えば、HashMap は安定と定義することができません。

In those cases, you need to use the following systems hooks.

そのような場合は、以下のシステムフックを使用する必要があります。


```
 system func preupgrade() {
    // Do something before upgrade
  };

  system func postupgrade() {
    // Do something after upgrade
  };
}
```

The trick is to use the **preupgrade** method to put all data into stable variables, and use to stable variables to reinitialize your canister state.

コツは、**preupgrade** メソッドを使用してすべてのデータを安定変数に入れ、安定変数を使用してキャニスターの状態を再初期化することです。

(For more informations : https://smartcontracts.org/docs/language-guide/upgrades.html)

(詳細はこちら : https://smartcontracts.org/docs/language-guide/upgrades.html)

# Challenge 課題 🎮

Take a break and try completing challenge 8 to 10.

一息ついてから、チャレンジ8～10をクリアしてみてください。
