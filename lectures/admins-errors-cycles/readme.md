# Access Control, Error Handling, and Cycles アクセス制御、エラー処理、サイクル

Learning objective: by the end of this lecture you see how to implement access control, gracefully handle errors, and use the experimental cycles library.

学習目標：この講義の終わりまでに、アクセス制御の実装、エラーの優雅な処理、および実験サイクルライブラリの使用方法を理解する。

Level: intermediate

レベル：中級

Follow along with the slides here: [Google Slides](https://docs.google.com/presentation/d/1wrMGJQd6h31IzUH083l559-Yo2_2ANG9bIZN6wyiOco/edit?usp=sharing)

こちらのスライドでフォローしてください。[Google スライド](https://docs.google.com/presentation/d/1wrMGJQd6h31IzUH083l559-Yo2_2ANG9bIZN6wyiOco/edit?usp=sharing)

**Examples 例**

- [Access control basic](./motoko/access-control-basic.mo)
- [アクセス管理基本編](./motoko/access-control-basic.mo)
- [Access control multiple admins](./motoko/access-control-multi.mo)
- [複数管理者のアクセス制御](./motoko/access-control-multi.mo)
- [Error handling](./motoko/error-handling.mo)
- [エラー処理](./motoko/error-handling.mo)
- [Experimental cycles part A (Grandma's canister)](./motoko/experimental-cycles-a.mo)
- [実験サイクルそのA(おばあちゃんのキャニスター)](./motoko/experimental-cycles-a.mo)
- [Experimental cycles part B (consumer canister)](./motoko/experimental-cycles-b.mo)
- [実験サイクルそのB（消費者用キャニスター）](./motoko/experimental-cycles-b.mo)

This document contains the rough lecture notes with all of the examples in one place.

この資料は、例題をまとめた大まかな講義ノートを収録しています。

## Access Control アクセス制御

- For those times when you don't want let everyone access literally everything.
- すべての人に文字通りすべてのことにアクセスさせたくないときのために。
- A very simple case: admin-only things like minting, configuring metadata, managing assets, etc.
- とてもシンプルなケースです。ミンティング、メタデータの設定、アセットの管理など、管理者だけができることです。

### Really Simple Admin-Only Functions 本当にシンプルな管理者専用機能

- When you create a canister, your principal is provided as the caller (same as when you call a public method.)
- キャニスターを作成すると、プリンシパルが呼び出し元として提供されます (パブリック・メソッドを呼び出す場合と同じです)。
- You can capture this principal as an `owner` variable, and then only allow that principal to do certain things.
- このプリンシパルを `owner` 変数として取得し、そのプリンシパルにのみ特定の処理を許可することができます。
- The simplest way to check that the caller is the owner is using `assert`.
- 呼び出し元がオーナーであるかどうかを確認する最も簡単な方法は、 `assert` を使用することです。

```motoko
shared ({ caller = creator }) actor class MyCanister() = {

    stable var owner : Principal = creator;

    public shared ({ caller }) func mySecret () : async Text {
        assert(caller == owner);
        "Grandma's secret lasagne recipe...";
    };

}};
```

- Execute this as owner and no owner.
- オーナーとして実行する場合と、オーナーではない状態で実行する場合があります。

```zsh
dfx deploy --no-wallet access-control-basic
dfx canister call access-control-basic mySecret
dfx identity use alternate
dfx canister call access-control-basic mySecret
```

### Changing The Owner 所有者の変更

Of course, we would like to be able to change the owner.

もちろん、オーナーチェンジもできるようにしたい。

```motoko
shared ({ caller }) actor class MyCanister() = {

    stable var owner : Principal = caller;

    public shared ({ caller }) func mySecret () : async Text {
        assert(caller == owner);
        "Grandma's secret lasagne recipe...";
    };

    public shared ({ caller }) func setOwner (
        newOwner : Principal,
    ) : async () {
        assert(caller == owner);
        owner := newOwner;
    };

}
```

- Very brief demo ごく簡単なデモ

```zsh
dfx identity use main
dfx deploy --no-wallet access-control-multi
principal=$(dfx identity use alternate && dfx identity get-principal)
dfx identity use main
dfx canister call access-control-basic getOwner
dfx canister call access-control-basic setOwner "principal \"$(echo $principal)\""
dfx identity use alternate
dfx canister call access-control-basic mySecret
```

### Multiple Administrators 複数の管理者

- What if I want to share power?
- 権限を共有したい場合はどうすればいいですか？
- We can instead maintain a list of admins.
- 代わりに管理者のリストを管理することができます。

```motoko
import Array "mo:base/Array";
import Option "mo:base/Option";

shared ({ caller = creator }) actor class MyCanister() = {

    stable var admins : [Principal] = [creator];

    private func isAdmin (
        principal : Principal,
    ) : Bool {
        switch (Array.find<Principal>(admins, func (x) { x == principal })) {
            case (?a) true;
            case _ false;
        };
    };

    public shared ({ caller }) func addAdmins (
        newAdmins : [Principal]
    ) : async () {
        assert(isAdmin(caller));
        admins := Array.append(admins, Array.filter<Principal>(newAdmins, func (x) {
            // Briefly: we filter out admins which are already in the list
            Option.isNull(Array.find<Principal>(admins, func (y) { x == y }));
        }));
    };

    public shared ({ caller }) func mySecret () : async Text {
        assert(isAdmin(caller));
        "Grandma's secret lasagne recipe...";
    };

};
```

- Show it off 見せびらかす

```zsh
principal=$(dfx identity use alternate && dfx identity get-principal)
dfx identity use main
dfx deploy --no-wallet access-control-multi
dfx canister call access-control-multi addAdmins "(vec { principal \"$principal\"; })";
dfx identity use alternate
dfx canister call access-control-multi mySecret
```

- There are some more methods you might want in the example source code.
- サンプルのソースコードには、さらに必要なメソッドがいくつかあります。

### Permission Systems パーミッションシステム

- Real world scenarios often call for more nuanced access control systems.
- 現実の世界では、より微妙なニュアンスの入退室管理システムが必要とされることが多い。
    - Perhaps certain individuals or groups of individuals should be able to access certain things, but not others.
    - ある個人または個人のグループは特定のものにアクセスでき、他のものはアクセスできないようにすべきかもしれません。
    - Perhaps an individual should only be able to access their own data.
    - おそらく、個人は自分自身のデータにしかアクセスできないようにすべきなのでしょう。
- Challenge! Create a simple permission system with multiple roles or individuals that have unique permissions profiles.
- チャレンジ! ユニークな権限プロファイルを持つ複数のロールまたは個人を持つ、シンプルな権限システムを作成します。
    - Principals with minter role can call a mint method (which simply returns #ok())
    - minterの役割を持つプリンシパルは、mintメソッド(単純に#ok()を返す)を呼び出すことができます。
    - Principals with configurator role can call a configure method (which simply returns #ok())
    - configuratorの役割を持つプリンシパルは、configureメソッドを呼び出すことができます（単純に#ok()を返します）。

### Access Control Wrap-Up アクセス制御のまとめ

- Get the source code from the github link
- githubのリンクからソースコードを入手する
- Try adding access control to one of your contracts
- あなたのコントラクトにアクセス制御を追加してみる


## Error Handling エラー処理

- Reading materials: https://smartcontracts.org/docs/language-guide/errors.html
- 読み物： https://smartcontracts.org/docs/language-guide/errors.html
- With the admin system, we used `assert` to trap the contract based on an expression.
- 管理システムでは、式に基づいてコントラクトをトラップするために、`assert`を使用しました。
- Trapping a contract: when a contract traps, the request is thrown out and none of the state changes committed (exception to this (brief): async / async)
- コントラクトのトラップ：コントラクトがトラップされると、リクエストは投げ出され、状態の変更は一切コミットされません（この例外（概要）：sync / async）。
- Assert is quick to write, but it provides incredibly useless error messages.
- Assertは素早く書けますが、信じられないほど無駄なエラーメッセージを出します。
- Motoko provides two modules which are much better for error handling: `Result` and `Error`.
- Motoko は、エラー処理に適した 2 つのモジュール、 `Result` と `Error` を提供しています。
- The Option value primitive is also good for certain error cases.
- また、Option 値プリミティブは、特定のエラーケースに適している。

### Option Values as Errors エラーとなるオプション値

- Any time you have an option value in your program, Motoko will force you to deal with the `null` case.
- プログラム中にオプション値がある場合、Motoko は `null` のケースを処理するように強制します。
- `null` doesn't really tell you anything about what went wrong, which makes option values a great choice in cases where additional information isn't needed. For example, when our `Array.find` example above returns `null` it's completely obvious that it's because we couldn't *find* the value we sought.
- `null` は何が悪かったのかについて何も教えてくれないので、追加情報が必要ない場合にオプション値を使うのはとても良い選択です。例えば、上記の `Array.find` の例で `null` を返した場合、求めていた値を *find* できなかったからであることは完全に明らかです。
- It's bad in cases where several different things might go wrong, because we would not be able to diagnose the problem without somehow instrumenting the code.
- これは、いくつかの異なる問題が発生する可能性がある場合には、コードを何らかの方法で計測しなければ問題を診断することができないため、好ましくありません。

```
// Bad.
func foo () : ?Nat {
    if (not bar()) {
        return null;
    };
    if (not baz()) {
        return null;
    };
    return 1337;
};

foo() // if null, then how do I know what went wrong???
```

### To Error is Human (To Result Divine) 誤りは人なり（結果は神なり）

- `Error` and `Result` both allow us to provide more context for a given failure.
- `Error` と `Result` はどちらも、与えられた失敗に対してより多くのコンテキストを提供することができます。
- However, the Motoko docs encourage us to prefer `Result`. Whereas “exceptions should only be used to signal unexpected error states.”
- しかし、Motoko のドキュメントでは、 `Result` を選択するように勧めています。例外は予期しないエラー状態を知らせるためにのみ使用されるべきである" ということだ。
- Using `Result` makes your API safer by forcing consumers to unpack and handle all eventual cases.
- `Result` を使用することで、コンシューマはすべてのケースをアンパックして処理することを強制され、APIがより安全になります。
- Using a `Result` uses the variant type to allow us to define a data type for a successful result (`#ok()`), and a data type for an error result (`#err()`).
- `Result` を使用することで、成功した結果 (`#ok()`) のデータ型と、エラーの結果 (`#err()`) のデータ型を定義することができます。
- Let's look at an example...
- 例を見てみましょう...

```
import Array "mo:base/Array";
import Option "mo:base/Option";
import Result "mo:base/Result";

shared ({ caller = creator }) actor class MyCanister() = {

    stable var owner : Principal = creator;
    stable var folks : [Text] = ["Alice", "Bob", "Charlie"];

    // By using a variant type, we can even be explicit about certain error cases.
    type Errors = {
        #Restricted;
        #NotFound;
    };

    public shared ({ caller }) func renameFolk (
        name    : Text,
        newName : Text,
    ) : async Result.Result<(), Errors> {
        if (caller != owner) {
            return #err(#Restricted);
        };
        if (Option.isNull(Array.find<Text>(folks, func (x) { x == name }))) {
            return #err(#NotFound);
        };
        // ...
        #ok()
    }

};
```

```
dfx identity use main
dfx deploy --no-wallet error-handling
dfx canister call error-handling renameFolk '("Randall", "Randy")'
dfx identity use alternate
dfx canister call error-handling renameFolk '("Randall", "Randy")'
```

### Error Handling Wrap Up エラー処理のまとめ

- Stick to `Result` as much as possible, and steer clear of `Error` for now.
- Pull down the github source code and try it out for yourself

- できるだけ `Result` にこだわって、今のところ `Error` は使わないでください。
- githubのソースコードをダウンロードして、自分で試してみてください。

## Cycles

- We use cycles to pay for computation on the internet computer.
- Motoko provides a module to send and receive cycles in calls from other cansters and principals.
- As an example, let's create a paid API for Grandma's lasagne recipe.

- インターネットコンピュータでの計算の対価としてサイクルを使用するのです。
- Motokoは、他のカンスタやプリンシパルからの呼び出しでサイクルを送受信するモジュールを提供します。
- 例として、おばあちゃんのラザニアレシピの有料APIを作成してみましょう。

```motoko
// This is Grandma's canister.
// これはおばあちゃんのキャニスターです。

import Cycles "mo:base/ExperimentalCycles";
import Result "mo:base/Result";

shared ({ caller = creator }) actor class MyCanister() = {

    let owner : Principal = creator;
    let price : Nat = 1_000_000; // 1 trillion cycles = 1 XDR. 1 million cycles = fractions of a penny 

    public shared ({ caller }) func recipe () : async Result.Result<Text, Text> {
        let cycles = Cycles.available();
        if (caller != owner) {
            if (cycles < price) {
                return #err("Sorry sunny, boy! Pay up or ship off!");
            } else {
                ignore Cycles.accept(price);
            };
        };
        #ok("Grandma's secret lasagne recipe...");
    };

};
```

```motoko
// This is the consumer canister
// これが消費者用キャニスターです

import Cycles "mo:base/ExperimentalCycles";
import Debug "mo:base/Debug";
import Nat "mo:base/Nat";
import Principal "mo:base/Principal";
import Result "mo:base/Result";

shared ({ caller = creator }) actor class MyCanister (grandmasCanister : Principal) = {

    public shared ({ caller }) func getRecipe (
        pay : Bool,
    ) : async Result.Result<Text, Text> {
        Debug.print("Current balance: " # Nat.toText(Cycles.balance()));
        let grandma : actor { recipe : () -> async Result.Result<Text, Text>; } = actor(Principal.toText(grandmasCanister));
        if (pay) {
            // We know the price is 1 million cycles, but we want to send grandma a little extra...
            Cycles.add(1_000_100);
        };
        let recipe = await grandma.recipe();
        Debug.print("Unused balance: " # Nat.toText(Cycles.refunded()));
        recipe;
    };

};
```

```zsh
dfx identity use main
dfx deploy --no-wallet experimental-cycles-a
principal=$(dfx canister id experimental-cycles-a)
dfx deploy --no-wallet experimental-cycles-b --argument "(principal \"$principal\")"
# call without paying...
dfx canister call experimental-cycles-b getRecipe "(false)"
# call again, buy pay this time
dfx canister call experimental-cycles-b getRecipe "(true)"
```

- An example of Cycles in the real world: CAP
- Cyclesの実例をご紹介します: CAP
