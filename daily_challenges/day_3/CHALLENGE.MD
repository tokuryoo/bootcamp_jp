# Challenge : day 3 🐥

TODO

# Prerequisites 前提条件 ✅

- Make sure you've read all the instructions on how to complete the challenges.
- 課題を達成するための手順をすべて読んでいることを確認してください。

- Follow along with the daily guide.
- デイリーガイドに従う。

# Coding 🧑‍💻

- Challenge 1 : Write a <strong> private </strong> function <strong> <i> swap </i> </strong> that takes 3 parameters : a <strong> mutable array </strong>, an index <strong> j </strong> and an index <strong> i </strong> and returns the same <strong> array </strong> but where value at index <strong> i </strong> and index <strong> j </strong> have been swapped.
- 課題1：3つのパラメータ（<strong>mutable 配列</strong>、インデックス <strong>j</strong>、インデックス <strong>i</strong>）を受け取り、インデックス <strong>i</strong> とインデックス <strong>j</strong> の値を交換した同じ <strong>配列</strong> を返す <strong>プライベート</strong> 関数 <strong><i>swap</i></strong> を作成しなさい。

- Challenge 2 : Write a function <strong> <i>init_count </i></strong> that takes a Nat <strong> n </strong> and returns an <strong> array [Nat] </strong> where value is equal to it's corresponding index. <br/>
- 課題2：Nat <strong>n</strong> を受け取り、対応するインデックスに等しい値を持つ <strong>配列[Nat]</strong> を返す関数 <strong><i>init_count</i></strong> を作成しなさい。<br/>
  Note : init_count(5) -> [0,1,2,3,4]. <br/>
  注 : init_count(5) -> [0,1,2,3,4]. <br/>
  Note 2 : Do <strong> not </strong> use Array.append.<br/>
  注2：Array.append を使わ<strong>ない</strong>でください。

- Challenge 3 : Write a function <strong> <i>seven </i></strong> that takes an <strong> array</strong> [Nat] and returns "Seven is found" if one digit of ANY number is 7. Otherwise this function will return "Seven not found".
- 課題3：<strong>配列</strong> [Nat]を受け取り、任意の数の1桁が7であれば "Seven is found" と返し、それ以外は "Seven not found" と返す関数 <strong><i>seven</i></strong> を作成しなさい。

- Challenge 4 : Write a function <strong> <i> nat_opt_to_nat </i></strong> that takes two parameters : <strong> n </strong> of type <strong> ?Nat </strong> and <strong> m </strong> of type <strong> Nat </strong>. This function will return the value of n if n is <strong> not </strong> <strong> <i> null </strong> </i> and if n is <strong> <i> null </strong> </i> it will default to the value of <strong> m</strong>.
- 課題4：関数 <strong>nat_opt_to_nat</strong> を作成し、<strong>？Nat</strong> 型の <strong>n</strong> と <strong>Nat</strong> 型の <strong>m</strong> をパラメータとする。この関数は n が <strong>null でなければ</strong> n の値を返し、n が <strong>null</strong> であれば <strong>m</strong> の値がデフォルトとなる。

- Challenge 5 : Write a function <strong> <i> day_of_the_week </i></strong> that takes a <strong> Nat n </strong> and returns a Text value corresponding to the day. If n doesn't correspond to any day it will return<strong> <i> null </i></strong>.
- 課題5：<strong>Nat n</strong> を受け取り、その日に対応するテキスト値を返す関数 <strong><i>day_of_the_week</i></strong> を作成しなさい。もし、n がどの日にも該当しない場合は、<strong>null</strong> を返します。<br/>
  <strong> <i> day_of_the_week </i></strong>(1) -> "Monday". <br/>
  <strong> <i> day_of_the_week </i></strong>(7) -> "Sunday". <br/>
  <strong> <i> day_of_the_week </i></strong>(12) -> null. <br/>

- Challenge 6 : Write a function <strong> <i> populate_array </i></strong> that takes an <strong> array [?Nat] </strong> and returns an <strong> array [Nat] </strong> where all <strong> <i> null </strong> </i> values have been replaced by 0. <br/>
- 課題6：<strong>配列[?Nat]</strong> を受け取り、すべての<strong>null</strong>値を<strong>0</strong>に置き換えた<strong>配列[Nat]</strong> を返す関数 <strong>populate_array</strong> を作成しなさい。<br/>
  Note : Do <strong> not </strong> use a loop.<br/>
  注：ループは使用<strong>しない</strong>でください。

- Challenge 7 : Write a function <strong> <i> sum_of_array </i></strong> that takes an <strong> array [Nat] </strong> and returns the sum of a values in the array. <br/>
- 課題7：<strong>配列[Nat]</strong> を受け取り、配列内の値の合計を返す関数 <strong><i>sum_of_array</i></strong> を作成しなさい。
  Note : Do <strong> not </strong> use a loop.<br/>
  注：ループは使用<strong>しない</strong>でください。

- Challenge 8 : Write a function <strong> <i> squared_array </i></strong> that takes an<strong> array [Nat] </strong> and returns a new array where each value has been squared. <br/>
- 課題8：<strong>配列[Nat]</strong> を受け取り、各値を二乗した新しい配列を返す関数 <strong><i>squared_array</i></strong> を作成しなさい。
  注：ループは使用<strong>しない</strong>でください。

- Challenge 9 : Write a function <strong> <i> increase_by_index </i></strong> that takes an <strong> array [Nat] </strong> and returns a new array where each number has been increased by it's corresponding index.<br/>
- 課題9：<strong>配列[Nat]</strong>を受け取り、各数値が対応するインデックスだけ増加した新しい配列を返す関数 <strong><i>increase_by_index</i></strong> を作成しなさい。<br/>
  Note : <strong> <i> increase_by_index </i></strong>[1, 4, 8, 0] -> [1 + 0, 4 + 1 , 8 + 2 , 0 + 3] = [1,5,10,3] <br/>
  注 : <strong> <i> increase_by_index </i></strong>[1, 4, 8, 0] -> [1 + 0, 4 + 1 , 8 + 2 , 0 + 3] = [1,5,10,3] <br/>
  Note 2 : Do <strong> not </strong> use a loop.<br/>
  注２：ループは使用<strong>しない</strong>でください。

- Challenge 10 : Write a higher order function <strong> <i> contains\<A> </i></strong> that takes 3 parameters : an array <strong> [A] </strong>, <strong> a </strong> of type <strong> A </strong> and a function f that takes a tuple of type <strong> (A,A) </strong> and returns a boolean. <br/> This function should return a boolean indicating whether or not <strong> a </strong> is present in the array.
- 課題10：配列<strong>[A]</strong>、<strong>A</strong>型の<strong>a</strong>、<strong>(A,A)</strong>型のタプルを受け取りブール値を返す関数fの3つのパラメータを受け取る高階関数<strong><i>contains\<A></i></strong>を作成しなさい。
この関数は、<strong>a</strong> が配列に存在するかどうかを示すブール値を返す必要があります。

<br/>
<strong> <i> Good luck 🎉 </strong> </i>
