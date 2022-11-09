# Challenge : day 5 🦆

# Prerequisites 前提条件 ✅

- Make sure you've read all the instructions on how to complete the challenges.

- 課題を達成するための手順をすべて読んでいることを確認してください。

- Follow along with the daily guide.

- デイリーガイドに沿ってください。

# Coding コーディング 🧑‍💻

- Challenge 1 : Write a function <strong> <i> is_anonymous </i> </strong> that takes no arguments but returns **true** is the caller is anonymous and **false** otherwise.

- 課題1：引数を取らず、呼び出し元が匿名であれば **true**、そうでなければ **false** を返す関数 <strong><i>is_anonymous</i></strong> を作成しなさい。

- Challenge 2 : Create an HashMap called favoriteNumber where the keys are **Principal** and the value are **Nat**.
- 課題2：favoriteNumber というHashMapを作成し、キーは**Principal**、値は**Nat**とする。

- Challenge 3 : Write two functions :
  - <strong> <i> add_favorite_number </i> </strong> that takes n of type **Nat** and stores this value in the HashMap where the key is the principal of the caller. This function has no return value.
  - <strong> <i> show_favorite_number </i> </strong> that takes no argument and returns n of type **?Nat**, n is the favorite number of the person as defined in the previous function or null if the person hasn't registered.

- 課題3：関数を2つ書け。
  - <strong><i>add_favorite_number</i></strong> は n を **Nat** 型で受け取り，この値を HashMap (キーは呼び出し元の principal) に格納する関数である．この関数には戻り値はない。
  - <strong><i>show_favorite_number</i></strong> は引数を取らず、型 **?Nat** の n を返し、n は前の関数（訳注 add_favorite_number のこと）で定義したその人(訳注 msg.caller)のお気に入り番号、またはその人が登録していない場合は null を返します。


- Challenge 4 : Rewrite your function <strong> <i> add_favorite_number </i> </strong> so that if the caller has already registered his favorite number, the value in memory isn't modified. This function will return a text of type **Text** that indicates "You've already registered your number" in that case and "You've successfully registered your number" in the other scenario.

- 課題4：関数 <strong><i>add_favorite_number</i></strong> を、呼び出し元が既にお気に入り番号を登録していた場合、メモリ内の値が変更されないように書き直せ。この関数は、その場合は "You've already registered your number"、それ以外の場合は "You've successfully registered your number" を示す **Text** 型のテキストを返します。

- Challenge 5 : Write two functions
  - <strong> <i> update_favorite_number </strong> </i>
  - <strong> <i> delete_favorite_number </strong> </i>

- 課題5：2つの関数を書きなさい。
  - <strong> <i> update_favorite_number </strong> </i>
  - <strong> <i> delete_favorite_number </strong> </i>

- Challenge 6 : Write a function <strong> <i> deposit_cycles </strong> </i> that allow anyone to deposit cycles into the canister. This function takes no parameter but returns n of type **Nat** corresponding to the amount of cycles deposited by the call.
- 課題6：誰でもサイクルをキャニスタに預けられるようにする関数 <strong><i>deposit_cycles</i></strong> を書きなさい。この関数はパラメータを取らず、呼び出しによって預けられたサイクルの量に対応する型**Nat**の n を返す。
  - 訳注：ヒント１。関数名は wallet_receive にすると良い。ウォレットキャニスターの 関数 wallet_send を経由して、wallet_receive を呼び出す。
  - 訳注：ヒント２。ほぼ答え。https://github.com/dfinity/examples/tree/master/motoko/hello_cycles

- Challenge 7 (hard ⚠️) : Write a function <strong> <i> withdraw_cycles </strong> </i> that takes a parameter n of type **Nat** corresponding to the number of cycles you want to withdraw from the canister and send it to caller asumming the caller has a callback called deposit_cycles()<br/>
  Note : You need two canisters. <br/>
  Note 2 : Don't do that in production without admin protection or your might be the target of a **cycle draining** attack.

- 課題7（難しい⚠️）: キャニスターから引き出したいサイクルの数に対応する **Nat** 型のパラメータ n を受け取り、呼び出し元が deposit_cycles() というコールバックを持っているとして呼び出し元に送信する関数 <strong><i>withdraw_cycles</i></strong> を書く。<br/>
  注意：キャニスターは2つ必要です。<br/>
  注2：管理者の保護がない本番環境では行わないでください。さもないと、**サイクルの枯渇**攻撃の標的になる可能性があります。

- Challenge 8 : Rewrite the counter (of day 1) but this time the counter will be kept accross ugprades. Also declare a variable of type **Nat** called versionNumber that will keep track of how many times your canister has been upgraded.

- 課題8 : (1日目の)カウンターを書き直しますが、今回はアップグレードの回数を記録することにします。また、versionNumber という **Nat** 型の変数を宣言し、キャニスターが何回アップグレードされたかを記録しましょう。
  - 訳注：１日目のカウンター。day1 の Challenge 4 のこと。

- Challenge 9 : In a new file, copy and paste the functionnalities you've created in challenges 2 to 5. This time the hashmap and all records should be preserved accross upgrades.

- 課題9：新しいファイルに、課題2〜5で作成した機能をコピー＆ペーストしてください。このとき、ハッシュマップとすべてのレコードは、アップグレード先へ、保存する必要があります。

- Challenge 10 (optional) : In autonomy, write a CRUD canister, you can add as much functionnalities as you want, a few examples :

  - Anonymous principal rejection.
  - Cycle functionnality for registration.
  - Admin management.

- 課題10 (任意) : 自主的に、CRUDキャニスターを書いてください。あなたが望むだけの機能を追加することができます。
  - 匿名 Principal 拒否。
  - 登録のためのサイクル機能
  - 管理者管理

Note : Only practice challenge 10 if you wish to, this is optional and it will not be taken into account for any ranking.

注意：チャレンジ10の練習は、希望者のみ。

<br/>
<strong> <i> Good luck 🎉 </strong> </i>
