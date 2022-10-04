# Token Standards トークン標準

## About Me 私について

- I'm Jorgen (pronounced "yorn")
- 私は Jorgen です（発音："yorn"）
- @jorgenbuilder on Twitter
- Twitter は @jorgenbuilder
- Indie dev / Saga Tarot founder
- インディー開発者／サガ・タロット創設者
- (Minor) contributor to stoic wallet, entrepot market, plug wallet, earth wallet, etc.
- （マイナー）ストイックウォレット、エントレポットマーケット、プラグウォレット、アースウォレットなどの貢献者。

## Learning Objectives 学習目標

- Token standard review
- トークン標準レビュー
    - Basic anatomy
    - 基本的な解剖学
    - Importance of standards
    - 規格の重要性
    - Choosing a standard
    - 規格の選択
    - DIP721 breakdown
    - DIP721の内訳
- Hands on: implement your own standards compliant NFT from scratch
- ハンズオン：標準に準拠した独自のNFTをゼロから実装する

## Notice! 注意！

- Standards are currently still in flux! I've tried to future proof the information here, but an ICP developer must be more ready for change than most 😅. Those that can tolerate the ambiguity will earn a place on the future best blockchain for NFTs!
- 現在、規格はまだ流動的なのです 私はここで情報を将来的に証明しようとしましたが、ICP開発者は他の人よりも変化に対する準備ができているはずです😅。曖昧さを許容できる人は、NFTのための未来の最高のブロックチェーンで場所を得ることができるでしょう
- Tools for deploying an NFT project will eventually mature to the point where having low level implementation knowledge for token standards is not strictly necessary.
- NFTプロジェクトを展開するためのツールは、いずれ成熟し、トークン標準の低レベルの実装知識は厳密には必要ないところまで到達するでしょう。

訳注：現在、既に ICRC-1 という標準規格があります(2022/8)。

## Token Standard Review トークン標準レビュー

- We'll be talking about Non-Fungible Tokens today
- 今日はNon-Fungible Tokenについてお話します。

### The basic anatomy of a token contract トークンコントラクトの基本的な構造

- A token contract is an authoritative source of state
- トークンコントラクトは、国家の権威ある情報源である
    - Who owns what, i.e. the ledger
    - 誰が何を所有しているか、すなわち台帳
    - What a token is, i.e. token metadata
    - トークンが何であるか（トークン・メタデータ
- A token contract provides functionality to query and update its state
- トークンコントラクトは、その状態を照会し、更新する機能を提供します。
    - Ownership transfer
    - 所有権の移転
    - Delegating signing authority on tokens
    - トークンの署名権限の委譲
    - Balance queries
    - 残高クエリ
    - Metadata queries
    - メタデータクエリ
    - And so on...
    - などなど...

### The purpose of a token standard
### トークン規格の目的

- Tokens are highly portable: anyone anywhere can interact with them
- トークンは移植性が高い：誰でもどこでもやりとりできる
- Contracts and dapps need a "lingua franca"
- コントラクトやDappsには "共通言語 "が必要
- Standards prescribe:
- 標準が規定する
    - the token methods (interface)
    - トークンのメソッド(インターフェース)
    - and how they work (implementation)
    - とその動作方法（実装）を規定

## Choosing a token standard トークン標準の選択

Why I currently endorse DIP721

私が現在DIP721を支持する理由

- Dfinity "endorsed" it with an upcoming tutorial series
- Dfinityが今後のチュートリアルシリーズで "お墨付き "を与える
- Follows the proven Ethereum standard
- 実績のあるEthereumの標準に従う
- Psychedelic DAO has many transparent common infrastructure projects (i.e. wasm validation w/ Cover, provenance w/ CAP, discovery w/ DAB, ETH bridge w/ Terebithia, etc.)
- Psychedelic DAOは、多くの透明な共通インフラプロジェクトを持っています（例：CoverによるWasm検証、CAPによる証明、DABによる発見、TerebithiaによるETHブリッジ、等）。
- Psychedelic has many staff developers to engage community developers
- Psychedelicは、コミュニティ開発者を巻き込むために多くのスタッフ開発者を抱えています。
- EXT lacks critical documentation and has major process bottlenecks
- EXTは、重要なドキュメントが不足しており、プロセスのボトルネックがある。

## Breaking down the DIP721 standard // DIP721規格を分解してみる

"DIP721 is an ERC-721 (Ethereum Request for Comments) style non-fungible token standard built mirroring its Ethereum counterpart and adapting it to the Internet Computer, maintaining the same interface.

"DIP721は、ERC-721（Ethereum Request for Comments）スタイルの非腐敗型トークン規格で、Ethereumのカウンターパートをミラーリングしてインターネットコンピュータに適合させ、同じインターフェースを維持したまま構築されています。

This standard aims to adopt the EIP-721 (Ethereum Improvement Proposal) to the Internet Computer; providing a simple, non-ambiguous, extendable API for the transfer and tracking ownership of NFTs..."

この規格は、EIP-721（Ethereum Improvement Proposal）をインターネットコンピュータに採用することを目的としており、NFTの所有権の移転と追跡のためのシンプルで曖昧でない拡張可能なAPIを提供する...。"

From the [official DIP721 specification](https://github.com/Psychedelic/DIP721/blob/develop/spec.md)

[DIP721 公式仕様書](https://github.com/Psychedelic/DIP721/blob/develop/spec.md)より。


### Basic Interface overview 基本的なインターフェイスの概要

```candid
name: () -> (opt text) query;
logo: () -> (opt text) query;
symbol: () -> (opt text) query;

totalSupply: () -> (nat) query;
balanceOf: (user: principal) -> (nat) query;
ownerOf: (tokenId: nat) -> (variant { ok = opt Principal; err = NftError }) query;

tokenMetadata: (tokenId: nat) -> (variant { ok = TokenMetadata; err = NftError }) query;
ownerTokenMetadata: (user: principal) -> (variant { ok = vec TokenMetadata; err = NftError }) query;

transferFrom: (from: principal, to: principal, tokenId: nat) -> (variant { ok = Nat; err = NftError });
```

*Note: the DIP721 method suffix (i.e. `nameDIP721`, `ownerOfDIP721`, etc) has been deprecated.*

*注：DIP721 メソッドのサフィックス（例：`nameDIP721`、`ownerOfDIP721`など）は非推奨となりました*。


## Let's build a DIP721 compliant NFT // DIP721準拠のNFTを作ろう

We're going to build a super simple DIP721 compliant NFT. The end result won't exactly be production ready, but we'll learn many basics and look ahead at how to become production ready.

今回は、超シンプルなDIP721準拠のNFTを製作します。最終的な結果は、必ずしも生産に適したものではありませんが、多くの基本を学び、生産に適した方法を見据えることができます。

### Bootstrap a new project 新しいプロジェクトを立ち上げる

We'll start by creating a super barebones motoko project.
まずは超ベアボーンなmotokoプロジェクトを作成します。

```sh
mkdir my-dip-nft
cd my-dip-nft
echo ".dfx" > .gitignore
echo "actor {}" > main.mo
echo '{
    "dfx": "0.8.4",
    "canisters": {
        "my-dip-nft": {
            "type": "motoko",
            "main": "main.mo"
        }
    }
}' > dfx.json
```

Then we'll start our local replica and run a test deployment.

そして、ローカルレプリカを起動し、テストデプロイメントを実行します。

```sh
dfx start --clean --background
dfx deploy
```

Then we will open our code editor to get to work.

そして、コードエディタを開いて作業を開始します。

```sh
code .
```

### Determine our error cases エラーケースの判定

Lucky us, the DIP standard tells us which known error cases our contract should be able to handle. Let's import these into our project.

幸運なことに、DIP標準は、コントラクトが処理できるべき既知のエラーケースを教えてくれます。これをプロジェクトにインポートしてみましょう。

```sh
echo 'module {
    public type NftError = {
        #Unauthorized;
        #OwnerNotFound;
        #OperatorNotFound;
        #TokenNotFound;
        #ExistedNFT;
        #SelfApprove;
        #SelfTransfer;
        #TxNotFound;
        #Other : Text;
    }
}' > errors.mo
```

And we will import this at the top of our `main.mo`.

そして、これを `main.mo` の先頭でインポートします。

```motoko
import NftErrors "errors";
```

Now is a good time to make sure that our Motoko language server is running, so that our editor will highlight any mistakes we make in realtime.

今、Motokoの言語サーバーが稼働していることを確認し、エディターがリアルタイムで間違いを強調してくれるようにする良い機会です。

On VSCode: `cmd + shift + p "motoko lang" enter`

VSCodeの場合 : `cmd + shift + p "motoko lang" enter`

### Our canister's metadata 当社キャニスターのメタデータ

The DIP721 methods `name`, `logo` and `symbol` all provide basic metadata describing our NFT canister. Let's implement them!

DIP721 のメソッド `name`, `logo`, `symbol` はすべて、NFT キャニスターを説明する基本的なメタデータを提供します。これらを実装してみましょう。

As long as we expose the correct methods and comply with critical implementation details, we can build our contract however we like behind the scenes. We'll do a very simple hardcoded approach for the moment.

正しいメソッドを公開し、重要な実装の詳細を遵守する限り、裏側で好きなようにコントラクトを構築することができるのです。ここでは、非常に単純なハードコード方式を採用することにします。

```motoko
public query func name () : async ?Text {
    ?"My DIP NFT";
};

public query func logo () : async ?Text {
    // We will put any old image URI here for now.
    ?"https://random.imagecdn.app/400/400";
};

public query func symbol () : async ?Text {
    // All hail the supreme Diamond Giraffe Peanut NFT!!!
    ?"💎🦒🥜";
};
```

### Check your work! 自分の作品をチェックしよう

Let's make sure that what we've written so far is working by calling each of our new methods from the command line.

ここまでで書いたものが機能していることを、コマンドラインからそれぞれの新しいメソッドを呼び出して確認してみましょう。

```sh
dfx deploy --no-wallet
> ...

dfx canister call my-dip-nft name
> (opt "My DIP NFT")

dfx canister call my-dip-nft logo
> (opt "https://random.imagecdn.app/400/400")

dfx canister call my-dip-nft symbol
> (opt "💎🦒🥜")
```

### Setting up canister state キャニスターの状態を設定する

We need to keep track of a few things: 1) what each token is (metadata), 2) who owns which token (ownership ledger).

私たちはいくつかのことを記録しておく必要があります。1) 各トークンが何であるか（メタデータ）、2) 誰がどのトークンを所有しているか（所有権台帳）。

DIP721 prescribes what the metadata for a token should look like, so let's import that into our project.

DIP721では、トークンのメタデータがどのようなものであるべきかが規定されていますので、それをプロジェクトにインポートしてみましょう。

```sh
echo 'module {

    public type TokenMetadata = {
        token_identifier    : Text;
        owner               : Principal;
        properties          : [(Text, GenericValue)];
        minted_at           : Nat64;
        minted_by           : Principal;
        operator            : ?Principal;
        transferred_at      : ?Nat64;
        transferred_by      : ?Principal;
    };

    public type GenericValue = {
        #BoolContent    : Bool;
        #TextContent    : Text;
        #BlobContent    : [Nat8];
        #Principal      : Principal;
        #NatContent     : Nat;
        #Nat8Content    : Nat8;
        #Nat16Content   : Nat16;
        #Nat32Content   : Nat32;
        #Nat64Content   : Nat64;
        #IntContent     : Int;
        #Int8Content    : Int8;
        #Int16Content   : Int16;
        #Int32Content   : Int32;
        #Int64Content   : Int64;
    };

}' > metadata.mo
```

Now we can import this metadata type into our `main.mo`, and create some very simple state for our canister.

このメタデータを `main.mo` にインポートして、Canister のための非常にシンプルな状態を作成します。

```motoko
import Metadata "metadata";
```

```motoko
stable var ledger : [Metadata.TokenMetadata] = [];
```

That should do it for now! For a production project, we would likely prefer a more efficient data structure, but this will do for the moment. Thanks to orthogonal persistence on the IC, this is all we need to maintain our "database" of token ownership and metadata.

今のところ、これで十分です。実際のプロジェクトでは、もっと効率的なデータ構造が望ましいのですが、今のところこれで十分です。ICの直交永続化のおかげで、トークンの所有権とメタデータの「データベース」を維持するのに必要なのは、これだけです。

### Implementing token query methods トークンクエリメソッドの実装

Now that we have our state in place, we can write our implementations for the various query methods in DIP721.

これで状態が整ったので、DIP721の様々なクエリメソッドの実装を書くことができるようになりました。

- We'll also look at what each method is for beside the implementation.
- また、実装の横で各方法が何のためにあるのかを見ていきます。
- We'll include the DIP721 prescription for each method in a comment. 
- 各メソッドのDIP721の処方箋をコメントで記載します。

#### Total Supply (1/n) 総供給量 (1/n)

*Purpose: How many NFTs exist in this contract?*

*目的：このコントラクトにはいくつのNFTが存在するか？*

```motoko
// @DIP721: () -> (nat) query;
public query func totalSupply () : async Nat {
    ledger.size();
};
```

- We determine that total supply is equivalent to the number of tokens in our ledger.
- 総供給量は台帳のトークン数と同じと判断する。

#### Balance Of (2/n)

*Purpose: How many NFTs does a given principal own?*

*目的：あるプリンシパルはいくつのNFTを保有しているか？*


```motoko
// @DIP721: (user: principal) -> (nat) query;
public query func balanceOf (
    user : Principal,
) : async Nat {
    Array.filter<Metadata.TokenMetadata>(Array.freeze(ledger), func (t) {
        t.owner == user
    }).size();
};
```

- We search our ledger for tokens owned by the given principal, and return the size of that list.
- 指定されたプリンシパルが所有するトークンを台帳から検索し、そのリストのサイズを返します。
- `Array.filter` expects an immutable array, so we must `freeze` our mutable ledger array before we can filter it.
- `Array.filter` は不変の配列を期待するので、フィルタリングする前に、可変の元帳配列を `freeze` しなければなりません。

#### Owner Of (3/n)

*Purpose: Who owns a given token?*

*目的：与えられたトークンを誰が所有するか？*

```motoko
// @DIP721: (tokenId: nat) -> (variant { ok = opt Principal; err = NftError }) query;
public query func ownerOf (
    tokenId : Nat,
) : async Result.Result<?Principal, NftError.NftError> {
    if (tokenId < ledger.size()) {
        #ok(?ledger[tokenId].owner);
    } else {
        #err(#TokenNotFound);
    };
};
```

- A little more interesting now!

- 少しは面白くなったかな!

#### Token Metadata (4/n)

*Purpose: Retrieve metadata for a given token token.*

*目的: 指定されたトークンのメタデータを取得する。*


```motoko
// @DIP721: (tokenId: nat) -> (variant { ok = TokenMetadata; err = NftError }) query;
public query func tokenMetadata (
    tokenId : Nat,
) : async Result.Result<Metadata.TokenMetadata, NftError.NftError> {
    if (tokenId < ledger.size()) {
        #ok(ledger[tokenId]);
    } else {
        #err(#TokenNotFound);
    };
};
```

#### Owner Token Metadata (5/n)

*Purpose: Retrieve metadata for all the tokens a given principal owns.*

*目的 指定されたプリンシパルが所有するすべてのトークンのメタデータを取得する。*

```motoko
// @DIP721: (user: principal) -> (variant { ok = vec TokenMetadata; err = NftError }) query;
public query func ownerTokenMetadata (
    user : Principal,
) : async Result.Result<[Metadata.TokenMetadata], NftError.NftError> {
    #ok(
        Array.filter<Metadata.TokenMetadata>(Array.freeze(ledger), func (t) {
            t.owner == user
        })
    );
};
```

### Taking the query methods for a spin クエリメソッドを試しに使ってみる

```sh
dfx deploy --no-wallet

dfx canister call my-dip-nft totalSupply
(0 : nat)

dfx canister call my-dip-nft balanceOf "principal \"$(dfx identity get-principal)\""
(0 : nat)

dfx canister call my-dip-nft ownerOf 0
(variant { err = variant { TokenNotFound } })

dfx canister call my-dip-nft tokenMetadata 0
(variant { err = variant { TokenNotFound } })

dfx canister call my-dip-nft ownerTokenMetadata "principal \"$(dfx identity get-principal)\""
(variant { ok = vec {} })
```

Everything is working as expected. Of course, we don't find anything too interesting, because we haven't minted any NFTs yet. Let's do that!

すべてが期待通りに動いています。もちろん、まだNFTを鋳造していないので、あまり面白いものは見当たりません。やってみよう

### Minting NFTs NFTの発行

- The DIP721 standard prescribes a mint method, so let's implement it!
- DIP721規格ではミント方式が規定されていますので、これを実装してみましょう。
- Note that this is not part of the basic DIP721 module, so you can consider it "extra".
- なお、これはDIP721の基本モジュールには含まれないので、「おまけ」だと思ってください。
- Everything in the core DIP721 module is "must have."
- DIP721のコアモジュールにあるものは全て "必須 "です。
- Minting can be quite unique to each project, and often it is not exposed to the public, so you can really do minting anyway you want.
- ミントはプロジェクトごとにかなり独自性があり、一般には公開されないことが多いので、本当に好きなようにミントを行うことができます。

```motoko
// @DIP721: (principal, nat, vec record { text; GenericValue }) -> (variant { Ok : nat; Err : NftError })
public shared ({ caller }) func mint (
    to          : Principal,
    tokenId     : Nat,
    properties  : [(Text, Metadata.GenericValue)],
) : async Nat {
    ledger := Array.tabulateVar<Metadata.TokenMetadata>(ledger.size() + 1, func (i) {
        if (i < ledger.size()) {
            ledger[i];
        } else {
            {
                owner               = to;
                token_identifier    = i;
                properties          = properties;
                minted_at           = Nat64.fromNat(Int.abs(Time.now()));
                minted_by           = caller;
                operator            = null;
                transferred_at      = null;
                transferred_by      = null;
            };
        }
    });
    // DIP721 expects the returned Nat to be the id of the token
    ledger.size() - 1;
};
```

### Let's mint!

Let's mint an NFT with our new method! In fact, let's mint two. Don't worry that the properties don't make sense yet. They will...

新しい方法でNFTを発行してみよう 実際、2つ作ってみましょう。プロパティがまだ意味をなしていないことは気にしないでください。いずれは...

```sh
dfx deploy --no-wallet

dfx canister call my-dip-nft mint "(
    principal \"$(dfx identity get-principal)\",
    0 : nat,
    vec {
        record { \"family\"; variant { TextContent = \"paint\" }; };
        record { \"refinement\"; variant { NatContent = 0 : nat } }
    }
)"
(0 : nat)

dfx canister call my-dip-nft mint "(
    principal \"$(dfx identity get-principal)\",
    0 : nat,
    vec {
        record { \"family\"; variant { TextContent = \"paint\" }; };
        record { \"refinement\"; variant { NatContent = 20 : nat } }
    }
)"
(1 : nat)
```

Now that we have some NFTs in our canister, let's try our query methods again.

さて、キャニスターにNFTがいくつか入っているので、もう一度クエリーの方法を試してみましょう。

```sh
dfx canister call my-dip-nft balanceOf "principal \"$(dfx identity get-principal)\""
(2 : nat)

dfx canister call my-dip-nft ownerTokenMetadata "principal \"$(dfx identity get-principal)\""
(
  variant {
    ok = vec {
      record {
        transferred_at = null;
        transferred_by = null;
        owner = principal "bhvmm-kkp5p-pzycc-apxyy-26mff-zazxc-gyotq-dlvtq-ilprx-g47sw-zae";
        operator = null;
        properties = vec {
          record { "family"; variant { TextContent = "paint" } };
          record { "refinement"; variant { NatContent = 0 : nat } };
        };
        token_identifier = 0 : nat;
        minted_at = 1_646_357_190_890_513_000 : nat64;
        minted_by = principal "bhvmm-kkp5p-pzycc-apxyy-26mff-zazxc-gyotq-dlvtq-ilprx-g47sw-zae";
      };
      record {
        transferred_at = null;
        transferred_by = null;
        owner = principal "bhvmm-kkp5p-pzycc-apxyy-26mff-zazxc-gyotq-dlvtq-ilprx-g47sw-zae";
        operator = null;
        properties = vec {
          record { "family"; variant { TextContent = "paint" } };
          record { "refinement"; variant { NatContent = 10 : nat } };
        };
        token_identifier = 1 : nat;
        minted_at = 1_646_357_286_725_236_400 : nat64;
        minted_by = principal "bhvmm-kkp5p-pzycc-apxyy-26mff-zazxc-gyotq-dlvtq-ilprx-g47sw-zae";
      };
    }
  },
)
```

### Managing Assets 資産の管理

- This is great and all, but where are the images? Great point. Let's associate our NFTs with assets.
- これは素晴らしいことだが、画像はどこにあるのだろう？素晴らしい指摘だ。NFTをアセットと関連付けましょう。
- Managing assets for your NFT project could be a lecture of its own.
- NFTプロジェクトのアセットを管理することは、それだけで1つの講義になる可能性があります。
- This part of the tutorial is illustrative of one way to manage assets.
- このチュートリアルでは、アセットを管理する1つの方法について説明します。

#### DIP721 Asset Prescriptions // DIP721 資産処方箋

- Assets are linked to a token via that token's metadata. DIP specifies metadata fields for this purpose: https://github.com/Psychedelic/DIP721/blob/develop/spec.md#predefined-key-value-pairs
- 資産は、そのトークンのメタデータを介してトークンにリンクされます。DIPはこの目的のためにメタデータのフィールドを指定します: https://github.com/Psychedelic/DIP721/blob/develop/spec.md#predefined-key-value-pairs
- dab-js uses the location field: https://github.com/Psychedelic/DAB-js/blob/main/src/standard_wrappers/nft_standards/dip_721.ts#L86
- dab-jsはlocationフィールドを使用します: https://github.com/Psychedelic/DAB-js/blob/main/src/standard_wrappers/nft_standards/dip_721.ts#L86


#### Adding Assets 資産の追加

We'll use an asset canister!

アセットキャニスターを使おう!

Clone this repo for some ready-to-use art, [created by an AI](https://colab.research.google.com/github/dribnet/clipit/blob/master/demos/PixelDrawer.ipynb#scrollTo=qQOvOhnKQ-Tu).

このレポをクローンして、すぐに使えるアート作品を手に入れよう。[created by an AI](https://colab.research.google.com/github/dribnet/clipit/blob/master/demos/PixelDrawer.ipynb#scrollTo=qQOvOhnKQ-Tu)

```sh
git clone git@github.com:jorgenbuilder/diamond-giraffe-peanut.git assets
```

Add our assets canister to `dfx.json`

アセットキャニスターを `dfx.json` に追加します。

```json
{
    "dfx": "0.8.4",
    "canisters": {
        "my-dip-nft": {
            "type": "motoko",
            "main": "main.mo"
        },
        "assets": {
            "type": "assets",
            "source": [
                "assets"
            ]
        }
    }
}
```

Deploy our asset canister and test it out.

アセットキャニスターを配備し、テストする。

```sh
dfx deploy assets --no-wallet
echo "http://$(dfx canister id assets).localhost:8000/24.png"
```

#### Linking assets to tokens アセットとトークンの関連付け


- As prescribed by DIP721, all we need to do is put the asset's location into the token's metadata.
- DIP721で規定されているように、アセットの位置をトークンのメタデータに入れるだけでよいのです。

Let's wipe out the tokens we minted, so we can mint them again with the correct metadata.

発行したトークンを消去して、正しいメタデータで再び発行できるようにしましょう。

```sh
dfx deploy --no-wallet my-dip-nft --mode=reinstall
> YOU WILL LOSE ALL DATA IN THE CANISTER.
> yes
```

Now we remint them.

今、私たちはそれらを再発行します。

```sh
dfx canister call my-dip-nft mint "(
    principal \"$(dfx identity get-principal)\",
    0 : nat,
    vec {
        record { \"family\"; variant { TextContent = \"paint\" }; };
        record { \"refinement\"; variant { NatContent = 0 : nat } };
        record { \"location\"; variant { TextContent = \"http://$(dfx canister id assets).localhost:8000/16.png\" } };
    }
)"
(0 : nat)

dfx canister call my-dip-nft mint "(
    principal \"$(dfx identity get-principal)\",
    0 : nat,
    vec {
        record { \"family\"; variant { TextContent = \"paint\" }; };
        record { \"refinement\"; variant { NatContent = 14 : nat } };
        record { \"location\"; variant { TextContent = \"http://$(dfx canister id assets).localhost:8000/31.png\" } };
    }
)"
(1 : nat)

dfx canister call my-dip-nft mint "(
    principal \"$(dfx identity get-principal)\",
    0 : nat,
    vec {
        record { \"family\"; variant { TextContent = \"pixel\" }; };
        record { \"refinement\"; variant { NatContent = 0 : nat } };
        record { \"location\"; variant { TextContent = \"http://$(dfx canister id assets).localhost:8000/1.png\" } };
    }
)"
(2 : nat)

dfx canister call my-dip-nft mint "(
    principal \"$(dfx identity get-principal)\",
    0 : nat,
    vec {
        record { \"family\"; variant { TextContent = \"pixel\" }; };
        record { \"refinement\"; variant { NatContent = 10 : nat } };
        record { \"location\"; variant { TextContent = \"http://$(dfx canister id assets).localhost:8000/11.png\" } };
    }
)"
(3 : nat)
```

#### Check your work! 自分の作品をチェックしよう

We now have several NFTs minted with assets! Let's call our NFT canister to verify.

現在、資産で鋳造されたNFTが複数あります! NFTキャニスターに電話して確認しましょう。

```sh
dfx canister call my-dip-nft ownerTokenMetadata "principal \"$(dfx identity get-principal)\""
```

### Finishing Touches 仕上げ

- We've nearly created a DIP721 compliant token
- DIP721に準拠したトークンをほぼ作成できました。
- We're missing one critical method: `transferFrom`
- 重要なメソッドが一つ足りません: `transferFrom` です。

```motoko
// @DIP721: (from: principal, to: principal, tokenId: nat) -> (variant { ok = Nat; err = NftError });
public shared ({ caller }) func transferFrom (
    from    : Principal,
    to      : Principal,
    tokenId : Nat,
) : async Result.Result<Nat, NftError.NftError> {
    if (tokenId >= ledger.size()) {
        // If the token id exceeds the size of our ledger, this is an invalid token id for us
        return #err(#TokenNotFound);
    };
    let token = ledger[tokenId];
    if (token.owner != caller) {
        // Only the owner may act upon a token
        return #err(#Unauthorized);
    };
    ledger[tokenId].owner := {
        // Update the owner of the NFT
        owner               = to;
        // Leave everything else the same
        token_identifier    = token.token_identifier;
        properties          = token.properties;
        minted_at           = token.minted_at;
        minted_by           = token.minted_by;
        operator            = token.operator;
        transferred_at      = token.transferred_at;
        transferred_by      = token.transferred_by;
    };
    // DIP721 expects the Nat returned to be the ID of a transaction history record. However, we will not be implementing this for now.
    #ok(0);
};
```

#### Check your work! 自分の作品をチェックしよう

```sh
dfx identity new alternate
dfx identity use alternate
altprinc=$(dfx identity get-principal)
dfx canister call my-dip-nft transferFrom "(principal \"$(dfx identity get-principal)\", principal \"$altprinc\", 0)"
> (variant { ok = 0 : nat })

dfx canister call my-dip-nft balanceOf "principal \"$principal\""
> (1 : nat)

dfx canister call my-dip-nft transferFrom "(principal \"$(dfx identity get-principal)\", principal \"$altprinc\", 0)"
> (variant { err = variant { Unauthorized } })
```

### Next Steps 次のステップ

- Wallet integration
- ウォレットの統合
    - Submit to DAB
    - DABに提出
    - Any wallet that integrates DAB will now work with your NFT! (Plug, hopefully others soon i.e. stoic, earth, etc.)
    - DABを統合したウォレットがNFTで動作するようになりました。(プラグ、ストイック、アースなど、他のウォレットもすぐに使えるようになることを期待します)
- Access control (don't let just anyone call the mint method)
- アクセス制御（誰でもmintメソッドを呼び出せるようにしない）
- Marketplace integration
- マーケットプレイスとの連携
    - Current marketplaces are built upon EXT
    - 現在のマーケットプレイスは、EXTをベースに構築されている
    - DIP721 marketplaces are on the horizon (ex Crowns market)
    - DIP721のマーケットプレイスが登場（例：クラウンズマーケット）。


## References & Notes 参考文献と注意事項

The DIP721 spec is being refactored as we speak, so these references are all varying degrees of out of date. Expect an updated spec and motoko reference in the coming weeks.

DIP721の仕様は現在調整中であり、これらのリファレンスはすべて古いものとなっています。今後数週間のうちに、最新の仕様とmotokoのリファレンスが公開されることを期待しています。

- [Hazel's DIP721 from May 2021 (out of date)](https://github.com/SuddenlyHazel/DIP721/blob/main/src/DIP721/DIP721.mo)
- [Remco's DIP721 from 2022 (out of date)](https://github.com/ICCards/dip721-motoko-library/blob/main/dip721_motoko/main.mo)
- [Official DIP721 spec (out of date)](https://github.com/Psychedelic/DIP721/blob/develop/spec.md)
- [Official DIP721 rust repo](https://github.com/Psychedelic/DIP721)
- [Remapping of legacy methods](https://github.com/Psychedelic/DIP721/blob/develop/nft-v2/src/legacy.rs)
