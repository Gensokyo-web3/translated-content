---
title: CSS によるサイズ設定
slug: Learn/CSS/Building_blocks/Sizing_items_in_CSS
---

{{LearnSidebar}}{{PreviousMenuNext("Learn/CSS/Building_blocks/Values_and_units", "Learn/CSS/Building_blocks/Images_media_form_elements", "Learn/CSS/Building_blocks")}}

これまでのさまざまなレッスンで、CSS を使用してウェブページ上のアイテムのサイズを調整するいくつかの方法に出会いました。デザイン作業をしていくうえで、それぞれの手法がどれほど大事かを理解することが重要です。このレッスンでは、CSS によって要素のサイズを設定する方法をまとめ、サイジングに役立ついくつかの用語を定義します。

| 前提条件: | 基本的なコンピューターリテラシー、[基本的なソフトウェアがインストールされている](/ja/Learn/Getting_started_with_the_web/Installing_basic_software)こと、[ファイルの扱い](/ja/Learn/Getting_started_with_the_web/Dealing_with_files)、HTML の基本（[HTML 入門](/ja/docs/Learn/HTML/Introduction_to_HTML)）および CSS に関するアイデア（[CSS の第一歩](/ja/docs/Learn/CSS/First_steps)）に関する基本的な知識を得ている。 |
| --------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 目的:     | CSS によるさまざまなサイズ設定の方法を理解する。                                                                                                                                                                                                                                                                                                                                                                       |

## 要素固有のサイズ

HTML 要素には自然なサイズがあり、CSS の影響を受ける前に設定されます。簡単な例は画像です。画像には、ページに埋め込む画像ファイルで定義された幅と高さがあります。このサイズは**固有のサイズ**と呼ばれ、画像自体に由来します。

`<img>` タグまたは CSS の属性を使用してページに画像を配置し、その高さと幅を変更しない場合、その固有のサイズを使用して表示されます。以下の例では、ファイルの範囲を確認できるように画像に境界線を付けています。

{{EmbedGHLiveSample("css-examples/learn/sizing/intrinsic-image.html", '100%', 600)}}

ただし、空の {{htmlelement("div")}} には独自のサイズはありません。コンテンツのない HTML に {{htmlelement("div")}} を追加し、画像で行ったように境界線を付けると、ページに線が表示されます。これは、要素の折りたたまれた境界線です。開いたままにするコンテンツはありません。以下の例では、その境界線はコンテナの幅まで伸びています。これはブロックレベルの要素であるため、慣れ親しんだ動作になるはずです。コンテンツがないため、高さ（またはブロックディメンションのサイズ）はありません。

{{EmbedGHLiveSample("css-examples/learn/sizing/intrinsic-text.html", '100%', 500)}}

上記の例では、空の要素内にテキストを追加してみてください。要素の高さがコンテンツによって定義されているため、境界線にはそのテキストが含まれています。したがって、`<div>` ブロックディメンションにおけるこのサイズは、コンテンツのサイズに由来します。繰り返しますが、これは要素の固有のサイズです。そのサイズはコンテンツによって定義されます。

## サイズの指定

もちろん、デザインの要素に特定のサイズを与えることもできます。要素にサイズが指定されている場合（およびそのコンテンツがそのサイズに収まる必要がある場合）、それを**外部サイズ**と呼びます。上記の例の `<div>` を見てみます。特定の {{cssxref("width")}} と {{cssxref("height")}} の値を指定できるため、そ コンテンツがどのように配置されても、そのサイズになります。 [前のオーバーフローに関するレッスンで](/ja/docs/Learn/CSS/Building_blocks/Overflowing_content)見たように、要素の中に収まるスペースよりも多くのコンテンツがある場合、高さを設定するとコンテンツがオーバーフローする可能性があります。

{{EmbedGHLiveSample("css-examples/learn/sizing/height.html", '100%', 600)}}

このオーバーフローの問題のため、要素の高さを長さまたはパーセンテージで固定することは、Web 上で非常に注意深く行う必要があります。

### 比率指定

多くの点で、パーセンテージは長さの単位のように機能[し、値と単位に関するレッスンで説明したように、](/ja/docs/Learn/CSS/Building_blocks/Values_and_units#Percentages)多くの場合、長さと同じ意味で使用できます。パーセンテージを使用している場合、あなたはそれが*何に対する*比率であるかを認識する必要があります。別のコンテナー内のボックスの場合、子ボックスに幅のパーセンテージを与えると、親コンテナーの幅のパーセンテージになります。

{{EmbedGHLiveSample("css-examples/learn/sizing/percent-width.html", '100%', 600)}}

これは、パーセンテージがそれを包含するブロックのサイズに対して解決されるためです。パーセンテージを適用しない `<div>` 場合、これはブロックレベルの要素であるため、使用可能なスペースの 100％を占めます。パーセンテージの幅を指定すると、これは通常埋められるスペースに対するの比率になります。

### マージンとパディングの比率

パーセンテージとして `margin` と `padding` を設定すると、奇妙な動作に気付く場合があります。以下の例では、ボックスがあります。内部ボックスに 10％の {{cssxref("margin")}} と 10％の {{cssxref("padding")}} を与えました。ボックスの上下の padding と margin は、左右の margin と同じサイズです。

{{EmbedGHLiveSample("css-examples/learn/sizing/percent-mp.html", '100%', 700)}}

例えば、上下のマージンのパーセンテージは要素の高さのパーセンテージであり、左右のマージンのパーセンテージは要素の幅のパーセンテージであると予想するかもしれません。しかし、そうではありません。

マージンとパディングをパーセンテージで設定する場合、値は**インラインサイズ**から計算されます。したがって横書きの言語で作業するときの幅になります。この例では、マージンとパディングはすべて幅の 10％です。つまり、ボックス全体で同じサイズのマージンとパディングを使用できます。この方法でパーセンテージを使用する場合、これは覚えておかなければならない事実です。

## 最小サイズ、最大サイズ

固定サイズを与えることに加えて、要素に最小サイズまたは最大サイズを与えるよう CSS に要求できます。さまざまな量のコンテンツを含む可能性のあるボックスがあり、常に特定の高さ*以上*にしたい場合は、そのボックスに {{cssxref("min-height")}} プロパティを設定できます。ボックスは常にこの高さ以上になりますが、ボックスの最小高さでのスペースよりも多くのコンテンツがある場合は、ボックスの高さが高くなります。

以下の例では、2 つのボックスがあり、どちらも 150 ピクセルの高さが定義されています。左側のボックスの高さは 150 ピクセルです。右側のボックスには、より多くのスペースを必要とするコンテンツがあるため、150 ピクセルよりも高くなっています。

{{EmbedGHLiveSample("css-examples/learn/sizing/min-height.html", '100%', 800)}}

これは、オーバーフローを回避しながら、可変量のコンテンツを処理するのに非常に役立ちます。

{{cssxref("max-width")}} の一般的な用途は、固有の幅で表示するための十分なスペースがない場合に画像を縮小し、その幅よりも大きくならないようにすることです。

例として、画像に `width: 100%` を設定する場合、その固有の幅がコンテナーよりも小さいと、画像は強制的に引き伸ばされて大きくなり、ピクセル化されたように見えます。固有の幅がコンテナーよりも大きい場合、オーバーフローします。どちらの場合も、あなたが起こりたいことではないでしょう。

代わりに `max-width: 100%` を使用すると、画像は本来のサイズよりも小さくなりますが、サイズの 100％で止まります。

以下の例では、同じ画像を 2 回使用しています。最初の画像には `width: 100%` が指定されており、それよりも大きいコンテナー内にあるため、コンテナーの幅まで拡大されます。2 番目の画像には `max-width: 100%` が設定されているため、コンテナを埋めるために引き伸ばされることはありません。3 番目のボックスにも同じ画像が含まれており、 `max-width: 100%` も設定されています。この場合、ボックスに収まるように縮小された様子を確認できます。

{{EmbedGHLiveSample("css-examples/learn/sizing/max-width.html", '100%', 800)}}

この手法は、画像を*レスポンシブ*にするために使用されます。そのため、より小さなデバイスで表示すると、適切に縮小されます。ただし、この手法を使用して非常に大きな画像を読み込んでから、ブラウザーで縮小するべきではありません。画像は、デザインに表示される最大サイズに必要なサイズよりも大きくならないように適切なサイズにするべきです。大きすぎる画像をダウンロードすると、サイトが遅くなり、ユーザーが従量制の接続を使用している場合は、より多くの費用がかかる可能性があります。

> **Note:** [レスポンシブ画像技術の](/ja/docs/Learn/HTML/Multimedia_and_embedding/Responsive_images)詳細をご覧ください。

## ビューポートに関する単位

ビューポート（サイトの表示に使用しているブラウザーでのページの表示領域）にもサイズがあります。CSS には、ビューポートのサイズに関連する単位（ビューポートの幅 `vw` とビューポートの高さ `vh` ）があります。これらの単位を使用すると、ユーザーのビューポートを基準にしてサイズを変更できます。

`1vh` はビューポートの高さの 1％に等しく、`1vw` はビューポートの幅の 1％に等しい。これらの単位を使用して、ボックスだけでなくテキストのサイズも変更できます。以下の例では、20vh と 20vw のサイズのボックスがあります。ボックスには、 {{cssxref("font-size")}} が 10vh の文字 `A` が含まれています。

{{EmbedGHLiveSample("css-examples/learn/sizing/vw-vh.html", '100%', 600)}}

**`vh` との `vw` 値を変更すると、ボックスまたはフォントのサイズが変更されます。ビューポートに相対的なサイズであるため、ビューポートのサイズを変更しても、サイズが変更されます。ビューポートのサイズを変更したときにサンプルの変更を確認するには、サイズを変更できる新しいブラウザーウィンドウにサンプルを読み込む必要があります（上記の例を含む埋め込み `<iframe>` がビューポートであるため）。[サンプルを開き](https://mdn.github.io/css-examples/learn/sizing/vw-vh.html)、ブラウザーウィンドウのサイズを変更して、ボックスとテキストのサイズがどうなるかを観察します。**

ビューポートに応じてサイズを調整することは、デザインに役立ちます。例えば、全ページのヒーローセクション(hero section)を他のコンテンツの前に表示させたい場合、ページのその部分を 100vh の高さにすると、残りのコンテンツはビューポートの下に押しやられてしまい、ドキュメントがスクロールされたときにのみ表示されます。

## まとめ

このレッスンでは、Web 上のサイズを決定するときに遭遇する可能性があるいくつかの重要な問題の概要を説明しました。[CSS レイアウト](/ja/docs/Learn/CSS/CSS_layout)に移ると、さまざまなレイアウトメソッドを習得する際にサイズ設定が非常に重要になるため、先に進む前に、ここで概念を理解しておくことをお勧めします。

{{PreviousMenuNext("Learn/CSS/Building_blocks/Values_and_units", "Learn/CSS/Building_blocks/Images_media_form_elements", "Learn/CSS/Building_blocks")}}

## このモジュール

1. [カスケードと継承](/ja/docs/Learn/CSS/Building_blocks/Cascade_and_inheritance)
2. [CSS セレクター](/ja/docs/Learn/CSS/Building_blocks/Selectors)

    - [要素・クラス・ID によるセレクター](/ja/docs/Learn/CSS/Building_blocks/Selectors/Type_Class_and_ID_Selectors)
    - [属性によるセレクター](/ja/docs/Learn/CSS/Building_blocks/Selectors/Attribute_selectors)
    - [擬似クラスおよび疑似要素によるセレクター](/ja/docs/Learn/CSS/Building_blocks/Selectors/Pseudo-classes_and_pseudo-elements)
    - [結合子](/ja/docs/Learn/CSS/Building_blocks/Selectors/Combinators)

3. [ボックスモデル](/ja/docs/Learn/CSS/Building_blocks/The_box_model)
4. [背景と枠線](/ja/docs/Learn/CSS/Building_blocks/Backgrounds_and_borders)
5. [テキスト方向の操作](/ja/docs/Learn/CSS/Building_blocks/Handling_different_text_directions)
6. [要素のはみ出し（オーバーフロー）](/ja/docs/Learn/CSS/Building_blocks/Overflowing_content)
7. [CSS の値と単位](/ja/docs/Learn/CSS/Building_blocks/Values_and_units)
8. [CSS によるサイズ設定](/ja/docs/Learn/CSS/Building_blocks/Sizing_items_in_CSS)
9. [画像・メディア・フォーム要素](/ja/docs/Learn/CSS/Building_blocks/Images_media_form_elements)
10. [表のスタイリング](/ja/docs/Learn/CSS/Building_blocks/Styling_tables)
11. [CSS のデバッグ](/ja/docs/Learn/CSS/Building_blocks/Debugging_CSS)
12. [CSS の整理](/ja/docs/Learn/CSS/Building_blocks/Organizing)
