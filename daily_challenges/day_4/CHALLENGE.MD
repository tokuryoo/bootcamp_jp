# Challenge : day 4 🐓

TODO

# Prerequisites 前提条件 ✅

- Make sure you've read all the instructions on how to complete the challenges.
- 課題を達成するための手順をすべて読んでいることを確認してください。

- Follow along with the daily guide.
- デイリーガイドに従う。

# Coding コーディング 🧑‍💻

For the daily challenges of today, you need to create multiples files. Instead of creating a file day_4.mo, start by creating a folder day_4 and inside create the different files you'll be asked for through the challenges.

今日の毎日の課題では、複数のファイルを作成する必要があります。day_4.moというファイルを作るのではなく、まずday_4というフォルダを作り、その中に課題を通して求められるさまざまなファイルを作ってください。

- Challenge 1 : Create two files called custom.mo and main.mo, create your own type inside custom.mo and import it in your main.mo file. In main, create a public function<strong> <i> fun </i> </strong> that takes no argument but return a value of your custom type. <br/>
  Note : Be creative 🌈
- 課題1：custom.mo と main.mo という2つのファイルを作成し、custom.mo の中で独自の型を作成して main.mo ファイルでインポートしてください。main.moの中に、引数をとらず、あなたの Custom 型の値を返すパブリック関数 <strong><i>fun</i></strong>を作成する。<br/>
  Note : Be creative 🌈 <br/>
  注：工夫してください 🌈


- Challenge 2 : Create a new file called animal.mo with at least 2 property (specie of type Text, energy of type Nat), import this type in your main.mo and create a variable that will store an animal.
- 課題2：animal.moというファイルを新規に作成し、少なくとも2つのプロパティ（Text型 specie、Nat型 energy）があり、main.moでこの型をインポートして、動物を格納する変数を作成します。

- Challenge 3 : In animal.mo create a public function called animal_sleep that takes an **Animal** and returns the same Animal where the field energy has been increased by 10.
  Note : As this is a public function of a **module**, you don't need to make the return type Async !
- 課題3：animal.moにanimal_sleepというパブリック関数を作り、**Animal**を受け取り、フィールドエネルギーを10増加させた同じAnimalを返します。
  注意：これは **モジュール** のパブリック関数なので、戻り値の型を Async にする必要はありません！

- Challenge 4 : In main.mo create a public function called<strong> <i> create_animal_then_takes_a_break <T> </i> </strong> that takes two parameter : a specie of type Text, an number of energy point of type Nat and returns an animal. This function will create a new animal based on the parameters passed and then put this animal to sleep before returning it ! 💤
- 課題4：main.moに <strong><i>create_animal_then_takes_a_break <T></i></strong> というパブリック関数を作り、Text型の specie とNat型の energy point 数をパラメータとして受け取り、animal を返すようにしなさい。この関数は、渡されたパラメータに基づいて新しい animal を作成し、その animal をスリープ状態にしてから返します! 💤

- Challenge 5 : In main.mo, import the type List from the base Library and create a list that stores animal.
- 課題5：main.moで、ベースライブラリからList型をインポートして、動物を格納するリストを作成する。

- Challenge 6 : In main.mo : create a function called <strong> <i> push_animal </i> </strong> that takes an animal as parameter and returns nothing this function should add this animal to your list created in challenge 5. Then create a second functionc called <strong> <i> get_animals </i> </strong> that takes no parameter but returns an **Array** that contains all animals stored in the list.
- 課題6：main.moで animal をパラメータとして取り、何も返さない <strong></i>push_animal</i></strong> という関数を作成します。この関数は、課題5で作成したリストにこの動物を追加する必要があります。次に、<strong></i>get_animals</i></strong> という2番目の関数を作成し、パラメータを取らずに、リストに格納されているすべての動物を含む **配列** を返すようにします。

For challenges 7 to 10 : You need to start from a fresh file (call it list.mo) you **cannot** use the List module of the base library, the goal is to reimplement some functionnality of arrays.

課題7から10について：あなたは新しいファイル（それをlist.moと呼ぶ）から始める必要があり、基本ライブラリのListモジュールを使用することは **できません**。目標は、配列のいくつかの機能を再実装することです。

- Challenge 7 : Write a function <strong> <i> is_null<T> </i> </strong> that takes <strong> l </strong> of type <strong>List\<T> </strong> and returns a boolean indicating if the list is <strong> <i> null </i> </strong>.
  Tips : Try using a switch/case.
- 課題7：List<T> 型の <strong>l</strong> を受け取り、そのリストが <strong>null</strong> であるかどうかを示す真偽値を返す関数 <strong><i>is_null<T></i></strong> を作成しなさい。
  ヒント: switch/case を使ってみよう


- Challenge 8 : Write a function <strong> <i> last </i> </strong> that takes <strong> l </strong> of type <strong>List\<T> </strong> and returns the optional last element of this list.
- 課題8：<strong>List\<T></strong> 型の <strong>l</strong> を受け取り、このリストの最後の要素をオプションで返す関数 <strong><i>last</i></strong> を作成しなさい。

- Challenge 9 : Write a function <strong> <i> size </i> </strong> that takes <strong> l </strong> of type <strong>List\<T> </strong> and returns a <strong> Nat </strong> indicating the size of this list. <br/>
  Note : If l is <strong> <i> null </i> </strong>, this function will return 0.

- 課題9：<strong>List\<T></strong> 型の <strong>l</strong> を受け取り、このリストのサイズを示す <strong>Nat</strong> を返す関数 <strong><i>size</i></strong> を作成しなさい。


- Challenge 10 : Write a function <strong> <i> get </i> </strong> that takes two arguments : <strong> l </strong> of type <strong>List\<T> </strong> </strong> and <strong> n </strong> of type <strong> Nat</strong> this function should return the optional value at rank n in the list.
- 課題10：2つの引数を取る関数 <strong><i>get</i></strong> を書きなさい。: <strong>List\<T></strong> 型の <strong>l</strong> と <strong>Nat</strong> 型の <strong>n</strong> 。この関数は、リストのランクnにあるオプションの値を返す必要があります。


In case you are done with everything. 👇

万が一、全て終わってしまった場合。👇

- Challenge 11 : Write a function <strong> <i> reverse </i> </strong> that takes <strong> l </strong> of type **List** and returns the reversed list.
- Challenge 11 : **List** 型の <strong>l</strong> を受け取り、反転したリストを返す関数 <strong><i>reverse</i></strong> を作成しなさい。

<br/>
<strong> <i> Good luck 🎉 </strong> </i>
