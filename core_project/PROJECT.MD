# Motoko bootcamp : core project 👷

# Motivation モチベーション❓

The first goal of the Motoko bootcamp is for each student to acquire as much experience and knowledge as possible. <br/> The bootcamp is not a hackathon and shouldn't be approched as a competitive event, this is first and foremost a way for the community to join in a common effort to promote the Internet Computer, Motoko and train a wave of new developers. <br/>

Motokoブートキャンプの第一の目標は、各受講者ができるだけ多くの経験と知識を習得することです。<br/> このブートキャンプはハッカソンでもなく、競争イベントとしてアプローチされるべきではなく、これは何よりもまず、インターネットコンピュータ、モトコの普及と新しい開発者の波を養成するために、コミュニティが共通の努力に参加する方法なのです。

With that in mind : we believe having to work on a complete project in autonomy and with different requirements will provide the following benefits :

その意味で、私たちは、自律的に、さまざまな要件を満たす完全なプロジェクトに取り組むことで、次のようなメリットが得られると考えています。

- Reinforce knowledge acquired through lectures and daily challenges.
- Increase motivation to follow all lectures by having a concrete end goal.
- Challenge autonomy and creativity of each student.
- Distribute prizes to most deserving students.
- Give a small taste of what being a developer and working on a project looks like to beginner students.
- Having live-project to showcase how cool is the Motoko-bootcamp. 😎

- 講義や日々のチャレンジで得た知識を強化する。
- 具体的な最終目標があることで、すべての講義についていけるモチベーションを高める。
- 学生一人ひとりの自主性と創造性に挑戦する。
- 優秀な学生には賞品を授与する。
- 初心者に、開発者としての自覚やプロジェクトに取り組む姿勢を少しでも感じてもらう。
- Motoko-bootcampがいかにクールであるかを示すために、ライブプロジェクトを行う。😎

For **intermediate** students, there is also the strong possibility that some Dev Mentors will be reviewing your core project as they look to fill job roles, so your core project is also a way to shine and showcase your talents. 🔥

また、**中級**の学生にとっては、Dev Mentorが求人のためにあなたのコアプロジェクトを確認する可能性が高いので、コアプロジェクトはあなたの才能を輝かせ、アピールする方法にもなります。🔥

# Requirements 必要条件 🎯

The core project is to create a live: **Basic NFT minter**.

コアプロジェクトは、ライブを作成することです。**基本的なNFTの採掘機**です。

In it's most simple version, the project should be composed of one webpage where the user can login, click on a button and then mint an nft that will belong to the user.

最も単純なバージョンでは、プロジェクトは、ユーザーがログインし、ボタンをクリックし、そのユーザーに属するnftをミントすることができる1つのWebページで構成される必要があります。

- One webpage composed of a **login button** using a wallet.
- One backend canister using the **DIP 721** standard.
- One **mint button** that will mint one or more NFT(s) for the user which consists of SVG artwork (stock artwork provided below).
- A way to display the NFT sent to the user, either by displaying it within the webpage or redirecting the user to the raw NFT image.

- ウォレットを使用した**ログインボタン**で構成されるウェブページ1つ。
- **DIP 721** 規格を使用したバックエンドキャニスター1つ。
- SVGアートワークで構成される、1つまたは複数のNFTをユーザーに送る**ミントボタン**（ストックアートワークは以下に提供されます）。
- ウェブページに表示するか、ユーザーを生のNFT画像にリダイレクトすることにより、ユーザーに送信されたNFTを表示する方法。

## Beginner 初心者 👦

Those requirements are probably already challenging enough for beginners, but you can still improve your own project by being creative, here are some ideas.

これらの要件は、初心者にとってはすでに十分な難易度でしょうが、工夫次第で自分のプロジェクトを向上させることができますので、ここでいくつかのアイデアを紹介しましょう。

- Add some form of customization to the NFT. (random or user-selection)
- Creative design for the webpage.
- Add some functionality around the NFT : (login, private access ...).

- NFTに何らかのカスタマイズを追加する。(ランダムまたはユーザー選択)
- ウェブページのクリエイティブなデザイン。
- NFTの機能追加：（ログイン、プライベートアクセス...）

## Intermediate 中級者 👨

For intermediate students, we are adding two additional requirements:

中級者向けには、さらに2つの要件を追加しています。

1. We want you to integrate some form of token transactions into your application. We don't want to involve any tokens with actual value and the current workflow to verify payment on the IC is quite cumbersome, so we have created a **Motoko bootcamp token** that you'll need to use in one way or another in your own project. These have no value and will be burned after the bootcamp is over. We will very soon be releasing a token faucet where you can get as many tokens as you might need. The most basic way to use tokens would be to make user pay a few tokens before allowing the mint process, but we are excited to see what other creative ways students will fullfill this token requirement.

1. 私たちは、あなたのアプリケーションに何らかの形でトークン・トランザクションを組み込んで欲しいと思っています。私たちは実際の価値を持つトークンを巻き込みたくないし、IC上での支払いを確認する現在のワークフローはかなり面倒なので、あなた自身のプロジェクトで何らかの形で使用する必要がある**Motoko bootcamp token**を作成しました。このトークンには価値がなく、ブートキャンプ終了後に焼却されます。トークンは、ブートキャンプ終了後に焼却される予定です。トークンの最も基本的な使用方法は、ミントプロセスを許可する前にユーザーに数トークンを支払わせることですが、私たちは学生がこのトークン要件を満たすために、他のどんな創造的な方法を見ることに興奮しています。

2. We want you to create a front end that displays all of the NFTs from your collection held by the wallet of a logged in user, as well as a way to view some other NFTs minted in your collection not owned by the user. This could simply be a log of mint history, a directory of other users and their NFTs, a social feed of some kind, but basically we expect your application to display more NFTs than what's expected from the beginner project.

2. ログインしているユーザーのウォレットが保有しているNFTを表示するフロントエンドと、そのユーザーが保有していないNFTを表示するフロントエンドを作成することを希望します。これは単純に造幣局の履歴のログ、他のユーザーとそのNFTのディレクトリ、ある種のソーシャルフィードでも構いませんが、基本的にはビギナープロジェクトで予想されるものよりも多くのNFTを表示するアプリケーションを期待しています。

## Example 👀

Here's a website called **<a href="https://qmr4u-2yaaa-aaaad-qbaxa-cai.ic0.app/about" target="\_blank"> Bob nfts </a>** that is a good example of a live avatar minter on the Internet Computer.

ここに **<a href="https://qmr4u-2yaaa-aaaad-qbaxa-cai.ic0.app/about" target="\_blank">Bob nfts</a>** というウェブサイトがありますが、これはインターネットコンピュータ上の live avatar minter の良い例です。


This website allow users to login using **<a href="\_https://github.com/Toniq-Labs/stoic-wallet" target="\_blank"> Stoic Wallet </a>**, to access some informations about the project once you're logged in and then use the mint button to create an NFT based on any content on the Internet Computer (by providing the url), you can also add some customization options around the NFTs with some Bob flairs. 🎨

このサイトでは、 **<a href="\_https://github.com/Toniq-Labs/stoic-wallet" target="\_blank">Stoic Wallet</a>** でログインし、プロジェクトに関するいくつかの情報にアクセスした後、ミントボタンを使ってインターネットコンピュータ上の任意のコンテンツに基づいてNFTを作成します（URLを提供）、またNFTの周りにいくつかのカスタマイズオプションを追加して、いくつかのボブフレアを使用できます。🎨

The source ode for this project is available **<a href="https://github.com/Toniq-Labs/creator-nfts" target="\_blank"> on this public GitHub repo</a>**.

このプロジェクトのソースコードは、 **<a href="https://github.com/Toniq-Labs/creator-nfts" target="\_blank"> この公開GitHubリポジトリ</a>** で入手可能です。

If you want to know more about this specific project, it's utility and roadamp you can **<a href="https://www.dfinitycommunity.com/a-closer-look-at-epic-nfts-bobnfts-and-the-future-of-nfts-on-the-internet-computer/" target="\_blank"> read about it here </a>**. </i>
このプロジェクトの詳細、実用性、ロードランプについて知りたい方は、**<a href="https://www.dfinitycommunity.com/a-closer-look-at-epic-nfts-bobnfts-and-the-future-of-nfts-on-the-internet-computer/" target="\_blank">ここをお読みください</a>** とあります。

Don't freak out if this seems way too much work for one week, the goal is to make the best project you can. <br/> Even if you don't succeed in making NFTs in one week (and if you are a beginner this will probably be really difficult), the goal is to create something with your own hands, get some practice and try to learn a few things along the way.

1週間では大変だと感じても気にしないでください。目標は、最高のプロジェクトを作ることです。
たとえ1週間でNFTを作ることに成功しなかったとしても（初心者の場合、これは本当に難しいでしょう）、目標は自分の手で何かを作り、練習し、その過程でいくつかのことを学ぼうとすることなのです。


# Faucet 蛇口💰

**<a href="https://bootcamp-faucet.vercel.app/" target="\_blank"> Here is the URL </a>** for the Motoko Bootcamp Tokens.

Motoko Bootcamp Tokenの **<a href="https://bootcamp-faucet.vercel.app/" target="\_blank">URLはこちら</a>**。

If you would like to few the code for the faucet, **<a href="https://github.com/stopak/bootcamp_faucet" target="\_blank"> you can find that here </a>**.

蛇口のコードは、 **<a href="https://github.com/stopak/bootcamp_faucet" target="\_blank">こちら</a>** にございますので、そちらをご参照ください。

Other useful info:

その他の役立つ情報:

1. The canister id キャニスターID : yeeiw-3qaaa-aaaah-qcvmq-cai
2. Your account ID if someone needs to send you more tokens.誰かがあなたにトークンを送る必要がある場合、あなたのアカウントID。</br>```import { getAccountId, getTokenIdentifier } from '../utils'; getAccountId(Principal.from('```**[YOUR PRINCPLE ID]**```'))``` </br>using plug api from 右記プラグイン・アプリを使用しています。: https://docs.plugwallet.ooo/getting-started/connect-to-plug/#requestconnectrequestconnectparams
3. URL to the plug article on exporting your wallet to dfx: https://twitter.com/plug_wallet/status/1429947938248314881<br/>
   dfxにウォレットをエクスポートするプラグの記事のURL: https://twitter.com/plug_wallet/status/1429947938248314881
4. A sample send command so you know how to send your tokens </br>
   トークンの送信方法を知るための送信コマンドのサンプル
```dfx canister --network ic call yeeiw-3qaaa-aaaah-qcvmq-cai send_dfx 'record{memo=0; amount=record{e8s=AMOUNT_X_10^8;};fee=record{e8s=PROPER_FEEE}; from_subaccount=null; to="DEST_ACCOUNTID_NOT_PRINCIPAL"; created_at_time=null;}'```

# Submission 提出 📝

Please **<a href="https://forms.gle/NxPyjU3ciG3UEQxa7" target="_blank" > fill out this form </a>** to submit your core project.

コアプロジェクトのご応募は、**<a href="https://forms.gle/NxPyjU3ciG3UEQxa7" target="_blank" > こちらのフォームにご記入ください</a>**。

# Ressources & Artwork リソース＆アートワーク 📚

Here are some ressources for you to complete this project :
このプロジェクトを完成させるためのリソースをいくつか紹介します。

- DIP 721 standard in **<a href="https://github.com/SuddenlyHazel/DIP721/blob/main/src/DIP721/DIP721.mo" target="_blank" > Motoko </a>** and **<a href="https://github.com/Psychedelic/DIP721" target="_blank"> Rust. </a>** (The Motoko implementation is not complete but this is already enough for this project).
- DIP 721規格の **<a href="https://github.com/SuddenlyHazel/DIP721/blob/main/src/DIP721/DIP721.mo" target="_blank" > Motoko </a>** と **<a href="https://github.com/Psychedelic/DIP721" target="_blank"> Rust</a>** （Motokoの実装は完了していませんが、このプロジェクトでは既に十分です）。
- We commissioned (3) different sets of SVG artwork from (3) different artists for you to use for your core project. You can find all of this artwork in **<a href="https://drive.google.com/drive/folders/1JKkOq1bpqAQ9hVbs12CkhuvPkCMYDwph?usp=sharing" target="_blank" > this Google Drive Folder</a>**.
- 私たちは、あなたのコアプロジェクトに使用するために、（3）異なるアーティストにSVGアートワークの（3）セットを依頼しました。このアートワークはすべて **<a href="https://drive.google.com/drive/folders/1JKkOq1bpqAQ9hVbs12CkhuvPkCMYDwph?usp=sharing" target="_blank" >このGoogle Driveフォルダ</a>** にあります。
- SVG layers can be easily recombined/manipulated with javascript, and you can style or even animate SVG elements with CSS! **<a href="https://www.w3schools.com/graphics/svg_intro.asp" target="_blank" >w3schools has a great SVG tutorial here</a>**.
- SVGレイヤーはjavascriptで簡単に組み替え/操作できますし、CSSでSVG要素のスタイルやアニメーションを設定することもできます。**<a href="https://www.w3schools.com/graphics/svg_intro.asp" target="_blank" >w3schoolsに素晴らしいSVGチュートリアルがあります。</a>**
- Tweaking the design of SVG images can be done with free tools like **<a href="https://inkscape.org/" target="_blank" >Inkscape</a>** (or even a text editor).
- SVG 画像のデザインの微調整は、**<a href="https://inkscape.org/" target="_blank" >Inkscape</a>** のような無料のツール (あるいはテキストエディター) で行うことができます。

# Prizes 🎁

Based on all submissions, best students for each track (beginner & intermediate) will receive prizes. <br/>
You can **<a href="https://www.dfinitycommunity.com/motoko-bootcamp-prizes/">read more details here </a>**.

応募作品の中から、初級・中級の各コースで優秀な生徒には賞品を贈呈します。<br/>
詳しくは、**<a href="https://www.dfinitycommunity.com/motoko-bootcamp-prizes/">こちら</a>** をご覧ください。
