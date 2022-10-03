# Challenge : day 6 🐉

# Prerequisites 前提条件 ✅

- Make sure you've read all the instructions on how to complete the challenges.

- 課題をクリアするための手順をすべて読んでいることを確認してください。

- Follow along with the daily guide.

- デイリーガイドに従う。

# Coding コーディング 🧑‍💻

The goal of today is to create our own NFT standard. 😎

今日の目標は、自分たちのNFT規格を作ることです。😎

- Challenge 1 : Create an actor in **main.mo** and declare the following types.
  - **TokenIndex** of type **Nat**.
  - **Error** which is a variant type with multiples tags :

- 課題1 : **main.mo**にアクターを作成し、以下の型を宣言してください。
  - 型 **Nat** の **TokenIndex** です。
  - 複数のタグを持つバリアントタイプである **Error**

- Challenge 2 : Declare an HashMap called **registry** with Key of type **TokenIndex** and value of type **Principal**. This will keeep track of which principal owns which TokenIndex.
- 課題2：キーが **TokenIndex** 型、値が **Principal** 型の **registry** という HashMap を宣言してください。これは、どのプリンシパルがどのTokenIndexを所有しているかを追跡するものである。

- Challenge 3 : Declare a variable of type **Nat** called nextTokenIndex, initialized at 0 that will keep track of the number of minted NFTs. <br/>
  Write a function called <strong> <i> mint </strong> </i> that takes no argument. <br/>
  This function should :

  - Returns a result of type **Result** and indicate an error in case the caller is anonymous.
  - If the user is authenticated : associate the current TokenIndex with the caller (use the HashMap we've created) and increase nextTokenIndex.

- 課題3：nextTokenIndexという**Nat**型の変数を宣言し、0に初期化して、鋳造されたNFTの数を記録するようにします。<br/>
  引数を取らない関数 <strong><i>mint</i></strong>を書いてください。<br/>
  この関数は
  - 結果を **Result** 型で返し、呼び出し元が匿名の場合はエラーを表示する。
  - ユーザが認証された場合 : 現在の TokenIndex を呼び出し元に関連付け (作成した HashMap を使用)、nextTokenIndex を増加させる。

- Challenge 4 : Write a function called <strong> <i> transfer </strong> </i> that takes two arguments :

  - **to** of type **Principal**.
  - **tokenIndex** of type **Nat**.

This function will transfer ownership of tokenIndex to the specified principal. You will check for eventuals errors and returns a result of type **Result**.

- 課題4：引数を2つ取る関数 <strong><i>transfer</i></strong> を作成する。
  - タイプ **Principal** の **to** です。
  - nat** 型の **tokenIndex** です。

この関数は、tokenIndex の所有権を指定された principal に移譲します。偶発的なエラーをチェックし、**Result** 型の結果を返します。

- Challenge 5 : Write a function called <strong> <i> balance </strong> </i> that takes no arguments but returns a list of tokenIndex owned by the called.
- 課題5：引数を取らず、呼び出された人が所有するtokenIndexのリストを返す関数 <strong><i>balance</i></strong> を書いてください。

- Challenge 6 : Write a function called <strong> <i> http_request </strong> </i> that should return a message indicating the number of nft minted so far and the principal of the latest minter. (Use the section on http request in the daily guide).
- 課題6：これまでに鋳造されたnftの数と最新の鋳造者の元本を示すメッセージを返す <strong><i>http_request</i></strong> という関数を作成しなさい。(デイリーガイドのhttpリクエストのセクションを使用)。

- Challenge 7 : Modify the actor so that you can safely upgrade it without loosing any state.

Well... you've just created your own NFT standard 🔥.

Bonus : **intercanister calls**.

- 課題7：状態を崩さずに安全にアップグレードできるようにアクターを修正する。

えっと...NFTの規格🔥が出来ましたね。

ボーナス : **インターキャニスターコール**。


- Challenge 8 : Create another canister and use to mint a NFT by calling the mint method of your first canister.

- 課題8：別のキャニスターを作成し、最初のキャニスターのmintメソッドを呼び出して、NFTをミントするのに使用します。

Well... you just created your own on-chain wallet. 🔒

なるほど...オンチェーンウォレットを作ったんですね 🔒

Bonus optional (Only take on those challenges if you have nothing else to do today...)

ボーナスオプション(他にやることがない場合のみチャレンジしてください...)

Ledger canister 💰

台帳キャニスター 💰

- Challenge 9 : In a new actor implement a function called <strong> <i> default_account </strong> </i> that returns the address of the subbacount 0 for the canister.

- 課題9：新しいアクターで、キャニスターのサブアカウント0のアドレスを返す「default_account」という関数を実装してください。

- Challenge 10 : Write two functions :
  - <strong> <i> balance </strong> </i> : takes no arguments and returns the balance of icps of the canister defaul account.
  - <strong> <i> transfer </strong> </i> : takes

- 課題10：関数を2つ書け。
  - "balance" : 引数を取らず、キャニスターのデフォルト口座のicpsの残高を返す。
  - "transfer" : 取る

Ressources for challenge 9 & 10.

- Lectures on the ledger canister :
- Example of icp in canister :

チャレンジ9と10のためのリソース。
- 台帳キャニスターのレクチャー:
- キャニスターのicpの例 :

<br/>
<strong> <i> Good luck 🎉 </strong> </i>
