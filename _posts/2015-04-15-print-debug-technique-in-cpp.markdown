---
layout: post
title: "競技プログラミングで使えるC++プリントデバッグテクニック ~ Operator Overloading 編 ~"
categories: 競プロ
---

C++の "Operator Overloading" という仕組みを使うことで、`std::pair`や`std::vector`などの複雑な型を簡単に出力できるようにします。この仕組みを使えば、どんな複雑な型でも`cout << N`のように気軽に出力できるようになり便利です。

Operator Overloadingについて正しく理解していないのですが、動作のイメージとしては`std::ostream`クラスに対して`operator<<(任意の型)`というメソッドを後から定義している、と考えていいのではないかと思っています。`std::ostream`というのは`std::cout`オブジェクトや`std::cerr`オブジェクトのクラスで、`std::cout << 42;`という式は`std::cout.operator<<(42);`(`std::cout`オブジェクトに対する`operator<<`というメソッドの呼び出し)という式と等価らしいです。

## std::pair

まずは`std::pair`に対する`operator<<`を拡張してみます。(ちなみに`<<`は"insertion operator"というらしい)

<code data-gist-id='0c96c31a214c61d02816' data-gist-file="pair.cpp"></code>

これの出力は以下のようになります。

<code data-gist-id='0c96c31a214c61d02816' data-gist-file="pair.cpp.out"></code>

4行目が`operator<<`をoverloadingしている部分です。8行目の`cout << p << endl;`という式で`std::pair`を簡単に出力できて便利ですね！

## std::vector

`std::vector`も、`operator<<`を拡張しておけば出力するたびに毎回ループを書かなくてすみます。2次元`vector`にも応用可能です！

<code data-gist-id='0c96c31a214c61d02816' data-gist-file="vector.cpp"></code>

これの出力は以下のようになります。

<code data-gist-id='0c96c31a214c61d02816' data-gist-file="vector.cpp.out"></code>

9行目で`vector`の区切り文字にタブ文字を使用しているので見やすいです。こんな感じで出力を好きなように加工できるのも便利です。

## std::map

`std::map`はあまり出力する機会がない気がしますが、operator overloadingで出力を工夫すると綺麗に出力できます。

<code data-gist-id='0c96c31a214c61d02816' data-gist-file="map.cpp"></code>

これの出力は以下のようになります。

<code data-gist-id='0c96c31a214c61d02816' data-gist-file="map.cpp.out"></code>

## まとめ

Operator Overloading使ってデバッグを楽にしよう！という記事でした。オレオレマクロとかオレオレ拡張がし放題なのも競技プログラミングの楽しさの1つですね(こっちの方が楽しくなりすぎて練習が捗らないこともしょっちゅうです...)。僕の競プロ用C++テンプレートは [ここ](https://github.com/Genki-S/dotfiles/blob/master/clicoder.d/template.cpp) にあるのでよかったらみてみてください。何かアドバイスとかあれば是非コメントください！(競プロ勢のテンプレートまとめみたいなの欲しいなぁ)

実行したやつ: [Ideone.com - 68ibRf](http://ideone.com/68ibRf)

## 参考

この辺しっかり読めばOperator Overloadingマスターになれるかも

- [operator overloading - cppreference.com](http://en.cppreference.com/w/cpp/language/operators)
- [ostream - C++ Reference](http://www.cplusplus.com/reference/ostream/ostream/)
- [ostream::operator<< - C++ Reference](http://www.cplusplus.com/reference/ostream/ostream/operator%3C%3C/)
