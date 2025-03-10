---
title: 疑似クラスと疑似要素
slug: Learn/CSS/Building_blocks/Selectors/Pseudo-classes_and_pseudo-elements
---

{{LearnSidebar}}{{PreviousMenuNext("Learn/CSS/Building_blocks/Selectors/Attribute_selectors", "Learn/CSS/Building_blocks/Selectors/Combinators", "Learn/CSS/Building_blocks")}}

次に取り上げるセレクターのセットは、**疑似クラス**と**疑似要素**と呼ばれます。これらは多数あり、多くの場合、それらは非常に特定の目的に役立ちます。それらの使用方法がわかったら、リストを見て、達成しようとしているタスクに有効なものがあるかどうかを確認できます。ここでも、各セレクターに関連する MDN ページは、ブラウザーサポートの説明に役立ちます。

| 前提条件： | 基本的なコンピュータリテラシー、[インストールされている基本的なソフトウェア](/ja/Learn/Getting_started_with_the_web/Installing_basic_software)[、ファイルの操作](/ja/Learn/Getting_started_with_the_web/Dealing_with_files)に関する基本的な知識、HTML の基本（[HTML の概要を](/ja/docs/Learn/HTML/Introduction_to_HTML)学ぶ）、CSS のしくみ（[CSS の最初のステップを](/ja/docs/Learn/CSS/First_steps)学ぶ）。 |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 目的：     | 疑似クラスおよび疑似要素セレクターについて学習します。                                                                                                                                                                                                                                                                                                                                                        |

## 疑似クラスとは何ですか？

疑似クラスは、特定の状態にある要素を選択するセレクターです。たとえば、それらはそのタイプの最初の要素であるか、マウスポインターによってホバーされています。それらは、ドキュメントの一部にクラスを適用したかのように振る舞う傾向があり、マークアップの余分なクラスを削減し、より柔軟で保守可能なコードを提供するのに役立ちます。

疑似クラスは、コロンで始まるキーワードです。

```
:疑似クラス名
```

### 単純な疑似クラスの例

簡単な例を見てみましょう。以下の最初の例に示すように、記事の最初の段落を大きく太字にしたい場合は、その段落にクラスを追加してから、そのクラスに CSS を追加できます。

{{EmbedGHLiveSample("css-examples/learn/selectors/first-child.html", '100%', 800)}}

ただし、これを維持するのは面倒な場合があります。ドキュメントの上部に新しい段落が追加された場合はどうなりますか？クラスを新しい段落に移動する必要があります。クラスを追加する代わりに、{{cssxref(":first-child")}} 疑似クラスセレクターを使用できます。これにより、*常に*記事の最初の子要素がターゲットになり、HTML を編集する必要がなくなります（これは、CMS によって生成された可能性があるため、とにかく常に可能であるとは限りません。）

{{EmbedGHLiveSample("css-examples/learn/selectors/first-child2.html", '100%', 700)}}

すべての疑似クラスは、この同じ方法で動作します。特定の状態にあるドキュメントの一部をターゲットにして、HTML にクラスを追加したかのように動作します。MDN の他の例をいくつか見てみましょう。

- [`:last-child`](/ja/docs/Web/CSS/:last-child)
- [`:only-child`](/ja/docs/Web/CSS/:only-child)
- [`:invalid`](/ja/docs/Web/CSS/:invalid)

### ユーザーアクション疑似クラス

一部の疑似クラスは、ユーザーが何らかの方法でドキュメントを操作したときにのみ適用されます。これらの**ユーザーアクションの**疑似クラスは、**動的疑似クラス**と呼ばれることもあり、ユーザーが要素を操作したときに、要素にクラスが追加されたかのように動作します。例は次のとおりです。

- [`:hover`](/ja/docs/Web/CSS/:hover) — 上記の通り; これは、ユーザーが要素（通常はリンク）の上にポインターを移動した場合にのみ適用されます。
- [`:focus`](/ja/docs/Web/CSS/:focus) — ユーザーがキーボードコントロールを使用して要素にフォーカスした場合にのみ適用されます。

{{EmbedGHLiveSample("css-examples/learn/selectors/hover.html", '100%', 500)}}

## 疑似要素とは何ですか？

疑似要素は同様に動作しますが、既存の要素にクラスを適用するのではなく、まったく新しい HTML 要素をマークアップに追加したかのように動作します。疑似要素はダブルコロンで始まり `::` ます。

```
::疑似要素名
```

> **Note:** 一部の初期の疑似要素では、単一のコロン構文が使用されていたため、コードまたは例でこれを見ることがあるでしょう。最新のブラウザーは、後方互換性のためにシングルまたはダブルコロン構文で初期の疑似要素をサポートしています。

たとえば、段落の最初の行を選択する場合は、それを `<span>` 要素にラップして要素セレクターを使用できます。ただし、ラップした単語の数が親要素の幅よりも長いまたは短い場合は、失敗します。1 行にいくつの単語が収まるかわからない傾向があるため（画面の幅やフォントサイズが変わると、単語数が変わるため）、HTML を追加してこれを確実に行うことは不可能です。

`::first-line` 擬似要素セレクタは確実にあなたのためにこれを行います-それはまだ最初の行のみを選択します言葉の数が増加した場合と減少します。

{{EmbedGHLiveSample("css-examples/learn/selectors/first-line.html", '100%', 800)}}

それはまるで最初のフォーマットされた行を `<span>` で魔法のように包み、行の長さが変更されるたびに更新されるかのように動作します。

これにより、両方の段落の最初の行が選択されていることがわかります。

## 疑似クラスと疑似要素を組み合わせる

最初の段落の最初の行を太字にしたい場合は `:first-child` 、 `::first-line` セレクターとセレクターをチェーンすることができます。前のライブ例を編集して、次の CSS を使用するようにしてください。\<article>要素内にある最初の `<p>` 要素の最初の行を選択したいと言っています。

```css
 article p:first-child::first-line {
  font-size: 120%;
  font-weight: bold;
}
```

## :: before および:: after を使用したコンテンツの生成

CSS を使用してコンテンツをドキュメントに挿入するための [`content`](/ja/docs/Web/CSS/content) プロパティと共に使用される特別な疑似要素がいくつかあります。

以下のライブ例のように、これらを使用してテキストの文字列を挿入できます。{{cssxref("content")}} プロパティのテキスト値を変更してみて、出力でそれを確認してください。 `::before` 疑似要素を `::after` に変更して、要素の最初ではなく最後に挿入されたテキストを表示することもできます。

{{EmbedGHLiveSample("css-examples/learn/selectors/before.html", '100%', 400)}}

CSS からテキストの文字列を挿入することは、実際には Web で頻繁に行うことではありません。そのテキストは一部のスクリーンリーダーにはアクセスできず、将来誰かが見つけて編集するのが難しい場合があるためです。

これらの疑似要素のより有効な使用法は、アイコンを挿入することです。たとえば、以下の例で追加された小さな矢印は、スクリーンリーダーで読みたくない視覚的なインジケーターです。

{{EmbedGHLiveSample("css-examples/learn/selectors/after-icon.html", '100%', 400)}}

これらの疑似要素は、空の文字列を挿入するためにも頻繁に使用され、ページ上の要素と同じようにスタイルを設定できます。

次の例では、 `::before` 疑似要素を使用して空の文字列を追加しています。幅と高さでスタイルを設定できるように、これを `display: block` に設定しました。次に、CSS を使用して、他の要素と同じようにスタイルを設定します。CSS をいじって、CSS の外観と動作を変更できます。

{{EmbedGHLiveSample("css-examples/learn/selectors/before-styled.html", '100%', 500)}}

`content` プロパティとともに `::before` と `::after` 擬似要素を使用することは、CSS では「生成されたコンテンツ」と呼ばれ、この手法がさまざまなタスクに使用されているのをよく目にします。良い例は、[CSS Arrow Please Please](http://www.cssarrowplease.com/)のサイトで、[CSS で矢印](http://www.cssarrowplease.com/)を生成するのに役立ちます。矢印を作成するときに CSS を見ると、{{cssxref("::before")}} および {{cssxref("::after")}} 疑似要素が使用されていることがわかります。これらのセレクターが表示されたら、{{cssxref("content")}} プロパティを見て、ドキュメントに何が追加されているかを確認してください。

## 参照セクション

疑似クラスと疑似要素は多数あり、参照するリストがあると便利です。以下に、MDN のリファレンスページへのリンクとともに、それらをリストした表を示します。これをリファレンスとして使用して、ターゲットにできるものの種類を確認します。

### 疑似クラス

| セレクタ                                             | 説明                                                                                                                                                                                                                                                                                         |
| ---------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| {{cssxref(":active")}}                         | ユーザーが要素をアクティブ化（たとえばクリック）すると一致します。                                                                                                                                                                                                                           |
| {{cssxref(":any-link")}}                     | リンクの `:link` と `:visited` 状態の両方に一致します。                                                                                                                                                                                                                                      |
| {{cssxref(":blank")}}                         | 入力値が空の[`<input>` 要素に](/ja/docs/Web/HTML/Element/input)一致します。                                                                                                                                                                                                                  |
| {{cssxref(":checked")}}                     | 選択状態のラジオボタンまたはチェックボックスに一致します。                                                                                                                                                                                                                                   |
| {{cssxref(":current")}}                     | 現在表示されている要素または要素の祖先と一致します。                                                                                                                                                                                                                                         |
| {{cssxref(":default")}}                     | 類似要素のセットの中でデフォルトである 1 つ以上の UI 要素に一致します。                                                                                                                                                                                                                      |
| {{cssxref(":dir")}}                             | 方向性（HTML [`dir`](/ja/docs/Web/HTML/Global_attributes/dir) 属性または CSS [`direction`](/ja/docs/Web/CSS/direction) プロパティの値）に基づいて要素を選択します。                                                                                                                          |
| {{cssxref(":disabled")}}                     | 無効な状態のユーザーインターフェイス要素に一致します。                                                                                                                                                                                                                                       |
| {{cssxref(":empty")}}                         | オプションの空白以外の子を持たない要素に一致します。                                                                                                                                                                                                                                         |
| {{cssxref(":enabled")}}                     | 有効な状態のユーザーインターフェイス要素に一致します。                                                                                                                                                                                                                                       |
| {{cssxref(":first")}}                         | [ページ媒体](/ja/docs/Web/CSS/Paged_Media)では、最初のページと一致します。                                                                                                                                                                                                                   |
| {{cssxref(":first-child")}}                 | 兄弟の中で最初にある要素に一致します。                                                                                                                                                                                                                                                       |
| {{cssxref(":first-of-type")}}             | 兄弟の中で最初にある特定のタイプの要素に一致します。                                                                                                                                                                                                                                         |
| {{cssxref(":focus")}}                         | 要素にフォーカスがあるときに一致します。                                                                                                                                                                                                                                                     |
| {{cssxref(":focus-visible")}}             | 要素にフォーカスがあり、そのフォーカスがユーザーに表示される場合に一致します。                                                                                                                                                                                                               |
| {{cssxref(":focus-within")}}                 | フォーカスを持つ要素と、フォーカスを持つ子孫を持つ要素に一致します。                                                                                                                                                                                                                         |
| {{cssxref(":future")}}                         | 現在の要素の後の要素に一致します。                                                                                                                                                                                                                                                           |
| {{cssxref(":hover")}}                         | ユーザーが要素にカーソルを合わせると一致します。                                                                                                                                                                                                                                             |
| {{cssxref(":indeterminate")}}             | 値が不確定な状態の UI 要素、通常は[チェックボックスに](/ja/docs/Web/HTML/Element/input/checkbox)一致し[ます](/ja/docs/Web/HTML/Element/input/checkbox)。                                                                                                                                     |
| {{cssxref(":in-range")}}                     | 範囲制限を持つ要素で、要素の値が範囲内にある場合にマッチします。                                                                                                                                                                                                                             |
| {{cssxref(":invalid")}}                     | 無効な状態の `<input>` のような要素に一致します。                                                                                                                                                                                                                                            |
| {{cssxref(":lang")}}                         | 言語（HTML [lang](/ja/docs/Web/HTML/Global_attributes/lang)属性の値）に基づいて要素を[照合し](/ja/docs/Web/HTML/Global_attributes/lang)ます。                                                                                                                                                |
| {{cssxref(":last-child")}}                 | 兄弟の中で最後にある要素に一致します。                                                                                                                                                                                                                                                       |
| {{cssxref(":last-of-type")}}                 | 兄弟の中で最後にある特定のタイプの要素に一致します。                                                                                                                                                                                                                                         |
| {{cssxref(":left")}}                         | [ページ媒体](/ja/docs/Web/CSS/CSS_Pages)では、左側のページと一致します。                                                                                                                                                                                                                     |
| {{cssxref(":link")}}                         | 未訪問のリンクに一致します。                                                                                                                                                                                                                                                                 |
| {{cssxref(":local-link")}}                 | 現在のドキュメントと同じサイトにあるページを指すリンクに一致します。                                                                                                                                                                                                                         |
| {{cssxref(":is", ":is()")}}                 | 渡されたセレクターリスト内の任意のセレクターに一致します。                                                                                                                                                                                                                                   |
| {{cssxref(":not")}}                             | このセレクターに値として渡されるセレクターで一致しないものと一致します。                                                                                                                                                                                                                     |
| {{cssxref(":nth-​​child")}}             | 兄弟のリストの要素に一致します — 兄弟は*an+b*の形式の式で一致します（たとえば、2n + 1 は 1、3、5、7 番目などの要素に一致します。すべてが奇数です）。                                                                                                                                         |
| {{cssxref(":nth-​​of-type")}}         | 特定のタイプの兄弟（ `<p>` 要素など）のリストの要素に一致します — 兄弟は*、an+b*という形式の式で一致します（たとえば、2n + 1 は、その要素のタイプの 1、3、5 、7 番目などに一致します。すべて奇数です。）                                                                                     |
| {{cssxref(":nth-​​last-child")}}     | 兄弟のリストの要素を末尾から逆に数えて一致させます。兄弟は*an+b*の形式の式で一致します（たとえば、2n + 1 はシーケンスの最後の要素、次にその 2 つ前の要素、次にその 2 つ前の要素などと一致します。最後から数えてすべての奇数の要素。）                                                        |
| {{cssxref(":nth-​​last-of-type")}} | 特定のタイプの兄弟のリスト（ `<p>` 要素など）の要素を最後から逆に数えて一致させます。兄弟は*、an+b*という形式の式で一致します（たとえば、2n + 1 は、シーケンス内のそのタイプの最後の要素、次にその 2 つ前の要素、次にその 2 つ前の要素などと一致します。最後から数えてすべての奇数の要素。） |
| {{cssxref(":only-child")}}                 | 兄弟がない要素に一致します。                                                                                                                                                                                                                                                                 |
| {{cssxref(":only-of-type")}}                 | 兄弟間でそのタイプの唯一の要素である要素に一致します。                                                                                                                                                                                                                                       |
| {{cssxref(":optional")}}                     | 不要なフォーム要素に一致します。                                                                                                                                                                                                                                                             |
| {{cssxref(":out-of-range")}}                 | 範囲制限を持つ要素で、要素の値が範囲外にある場合にマッチします。                                                                                                                                                                                                                             |
| {{cssxref(":past")}}                         | 現在の要素より前の要素に一致します。                                                                                                                                                                                                                                                         |
| {{cssxref(":placeholder-shown")}}         | プレースホルダーテキストを表示している input 要素に一致します。                                                                                                                                                                                                                              |
| {{cssxref(":playing")}}                     | 「再生」または「一時停止」できるオーディオ、ビデオ、または類似のリソースを表す要素が「再生中」のときに一致します。                                                                                                                                                                           |
| {{cssxref(":paused")}}                         | 「再生」または「一時停止」できるオーディオ、ビデオ、または類似のリソースを表す要素が「一時停止」されている場合に一致します。                                                                                                                                                                 |
| {{cssxref(":read-only")}}                     | ユーザーが変更できない要素と一致します。                                                                                                                                                                                                                                                     |
| {{cssxref(":read-write")}}                 | ユーザーが変更可能な要素と一致します。                                                                                                                                                                                                                                                       |
| {{cssxref(":required")}}                     | 必要なフォーム要素に一致します。                                                                                                                                                                                                                                                             |
| {{cssxref(":right")}}                         | [ページ媒体](/ja/docs/Web/CSS/CSS_Pages)では、右側のページに一致します。                                                                                                                                                                                                                     |
| {{cssxref(":root")}}                         | ドキュメントのルートである要素に一致します。                                                                                                                                                                                                                                                 |
| {{cssxref(":scope")}}                         | スコープ要素であるすべての要素に一致します。                                                                                                                                                                                                                                                 |
| {{cssxref(":valid")}}                         | `<input>` 要素などで要素が有効な状態のときに一致します。                                                                                                                                                                                                                                     |
| {{cssxref(":target")}}                         | 現在の URL のターゲットである場合（つまり、現在の[URL フラグメントに](https://en.wikipedia.org/wiki/Fragment_identifier)一致する ID を持つ場合）、要素に一致し[ます](https://en.wikipedia.org/wiki/Fragment_identifier)。                                                                    |
| {{cssxref(":visited")}}                     | 訪問したリンクに一致します。                                                                                                                                                                                                                                                                 |

### 疑似要素

| セレクタ                                 | 説明                                                                                 |
| ---------------------------------------- | ------------------------------------------------------------------------------------ |
| {{cssxref("::after")}}             | 元の要素の実際のコンテンツの後に現れるスタイル可能な要素と一致します。               |
| {{cssxref("::before")}}         | 元の要素の実際のコンテンツの前に現れるスタイル可能な要素と一致します。               |
| {{cssxref("::first-letter")}} | 要素の最初の文字と一致します。                                                       |
| {{cssxref("::first-line")}}     | 含まれている要素の最初の行と一致します。                                             |
| {{cssxref("::grammar-error")}} | ブラウザーによってフラグが立てられた文法エラーを含むドキュメントの一部に一致します。   |
| {{cssxref("::marker")}}         | 通常は箇条書きまたは番号が含まれているリストアイテムのマーカーボックスに一致します。 |
| {{cssxref("::selection")}}     | 選択されたドキュメントの部分に一致します。                                           |
| {{cssxref("::spelling-error")}} | ブラウザーによってフラグが付けられた、スペルミスを含むドキュメントの一部に一致します。 |

{{PreviousMenuNext("Learn/CSS/Building_blocks/Selectors/Attribute_selectors", "Learn/CSS/Building_blocks/Selectors/Combinators", "Learn/CSS/Building_blocks")}}

## このモジュールでは

1. [カスケードと継承](/ja/docs/Learn/CSS/Building_blocks/Cascade_and_inheritance)
2. [CSS セレクター](/ja/docs/Learn/CSS/Building_blocks/Selectors)

    - [タイプ、クラス、ID セレクター](/ja/docs/Learn/CSS/Building_blocks/Selectors/Type_Class_and_ID_Selectors)
    - [属性セレクター](/ja/docs/Learn/CSS/Building_blocks/Selectors/Attribute_selectors)
    - [疑似クラスと疑似要素](/ja/docs/Learn/CSS/Building_blocks/Selectors/Pseudo-classes_and_pseudo-elements)
    - [コンビネーター](/ja/docs/Learn/CSS/Building_blocks/Selectors/Combinators)

3. [ボックスモデル](/ja/docs/Learn/CSS/Building_blocks/The_box_model)
4. [背景と枠線](/ja/docs/Learn/CSS/Building_blocks/Backgrounds_and_borders)
5. [異なるテキスト方向の処理](/ja/docs/Learn/CSS/Building_blocks/Handling_different_text_directions)
6. [あふれるコンテンツ](/ja/docs/Learn/CSS/Building_blocks/Overflowing_content)
7. [値と単位](/ja/docs/Learn/CSS/Building_blocks/Values_and_units)
8. [CSS でのアイテムのサイズ変更](/ja/docs/Learn/CSS/Building_blocks/Sizing_items_in_CSS)
9. [画像、メディア、フォーム要素](/ja/docs/Learn/CSS/Building_blocks/Images_media_form_elements)
10. [スタイリングテーブル](/ja/docs/Learn/CSS/Building_blocks/Styling_tables)
11. [CSS のデバッグ](/ja/docs/Learn/CSS/Building_blocks/Debugging_CSS)
12. [CSS の整理](/ja/docs/Learn/CSS/Building_blocks/Organizing)
