---
title: Pointer Lock API
slug: Web/API/Pointer_Lock_API
---

{{DefaultAPISidebar("Pointer Lock API")}}

**Pointer Lock API** (以前は _Mouse Lock API_ と呼ばれていました) は、ビューポート内のマウスカーソルの絶対位置だけでなく、時間の経過に伴うマウスの動き (すなわち、デルタ) に基づく入力方法を提供します。これにより、マウスの動きそのものを知る、マウスイベントのターゲットをひとつの要素にロックする、マウスが一方向へどれだけ移動できるかの制限を除去する、視野からカーソルを取り除くことができます。これらは、本人視点の 3D ゲームなどで理想的です。

さらにこの API は、動きのコントロールやオブジェクトの回転、エントリーの変更にかなりのマウス操作が必要になるアプリケーションで役立ちます。例えばなんらかのボタンをクリックすることなく、マウスを動かすだけで視野角を制御できます。ボタンは他の操作のために使用できます。また、地図や衛星画像を見るアプリでも役に立ちます。

Pointer Lock では、カーソルがブラウザーやスクリーンの境界を通り過ぎるときでもマウスイベントにアクセスできます。例えばユーザーは限りなくマウスを動かすことで、3D モデルの回転や操作を続けることができます。Pointer Lock がなければ、ポインターがブラウザーまたはスクリーンの端に達したときに回転や操作が止まります。ゲームのプレイヤーはマウスカーソルがゲームのプレイ領域から外れて、別のアプリケーションを意図せずクリックしてゲームからマウスのフォーカスが外れてしまうことを心配せずに、熱中してボタンのクリックやマウスカーソルをあちこちに動かすことができるようになります。

## 基本概念

Pointer Lock は [マウスキャプチャ](/ja/docs/Web/API/Element/setCapture) と関係があります。マウスキャプチャはマウスのドラッグ中にターゲットの要素へ継続的にイベントを提供しますが、マウスのボタンを離すとイベントが停止します。Pointer Lock とマウスキャプチャの違いは以下のとおりです:

- Pointer Lock は永続的です。明示的に API が呼び出されるかユーザーが特定の解放ジェスチャを行うまで、マウスを解放しません。
- Pointer Lock はブラウザーまたはスクリーンの境界に制限されません。
- Pointer Lock はマウスボタンの状態に関係なく、イベントが発生し続けます。
- Pointer Lock はカーソルを隠します。

## メソッド/プロパティの概要

ここでは、Pointer Lock 仕様に関係するプロパティやメソッドを簡単に説明します。

### requestPointerLock()

Pointer Lock API は [Fullscreen API](/ja/docs/Web/Guide/API/DOM/Using_full_screen_mode) と同様に、新たなメソッド {{domxref("Element.requestPointerLock","requestPointerLock()")}} を追加することで DOM 要素を拡張しています。なお現在は、ベンダー接頭辞を付加しています。接頭辞が最近削除されましたので、例えば `canvas` 要素で Pointer Lock を要求したい場合は、現在は以下のように宣言します:

```js
canvas.requestPointerLock = canvas.requestPointerLock ||
                            canvas.mozRequestPointerLock;

canvas.requestPointerLock()
```

### pointerLockElement と exitPointerLock()

Pointer Lock API は {{domxref("Document")}} インターフェイスも拡張しており、新たなプロパティやメソッドを追加しています。新たなプロパティ {{domxref("Document.pointerLockElement","pointerLockElement")}} は、現在ロックしている要素がある場合に、その要素へアクセスするために使用します。また、{{domxref("Document")}} 新たなメソッドである {{domxref("Document.exitPointerLock","exitPointerLock()")}} は、名前がほのめかすとおり Pointer Lock を終えるために使用します。

{{domxref("Document.pointerLockElement","pointerLockElement")}} プロパティは要素が現在 Pointer Locked 状態であるかを判断する (例えば真偽チェックを行う) ために、またはロックされた要素があればその要素への参照を得るために有用です。

`pointerLockElement` の使用例を示します:

```js
if(document.pointerLockElement === canvas ||
  document.mozPointerLockElement === canvas) {
    console.log('The pointer lock status is now locked');
} else {
    console.log('The pointer lock status is now unlocked');
}
```

{{domxref("Document.exitPointerLock()")}} メソッドは Pointer Lock を終えるために使用され、{{domxref("Element.requestPointerLock","requestPointerLock")}} と同様に {{event("pointerlockchange")}} イベントや {{event("pointerlockerror")}} イベントを用いて非同期的に動作します。使用例は以下のとおりです。

```js
document.exitPointerLock = document.exitPointerLock    ||
                           document.mozExitPointerLock;

// ロック解除を試みる
document.exitPointerLock();
```

## pointerlockchange イベント

Pointer Lock の状態が変化したとき、例えば {{domxref("Element.requestPointerLock","requestPointerLock()")}} や {{domxref("Document.exitPointerLock","exitPointerLock()")}} を呼び出したときや、ユーザーが ESC キーを押下したときなどに、{{event("pointerlockchange")}} イベントが `document` に発生します。これはシンプルなイベントであり、付加的なデータは含まれません。

```js
if ("onpointerlockchange" in document) {
  document.addEventListener('pointerlockchange', lockChangeAlert, false);
} else if ("onmozpointerlockchange" in document) {
  document.addEventListener('mozpointerlockchange', lockChangeAlert, false);
}

function lockChangeAlert() {
  if(document.pointerLockElement === canvas ||
  document.mozPointerLockElement === canvas) {
    console.log('The pointer lock status is now locked');
    // 応答として役に立つ処理
  } else {
    console.log('The pointer lock status is now unlocked');
    // 応答として役に立つ処理
  }
}
```

## pointerlockerror イベント

{{domxref("Element.requestPointerLock","requestPointerLock()")}} または {{domxref("Document.exitPointerLock","exitPointerLock()")}} の呼び出しによりエラーが発生したときは、{{event("pointerlockerror")}} イベントが `document` に発生します。これはシンプルなイベントであり、付加的なデータは含まれません。

```js
document.addEventListener('pointerlockerror', lockError, false);
document.addEventListener('mozpointerlockerror', lockError, false);

function lockError(e) {
  alert("Pointer lock failed");
}
```

> **Note:** Firefox 50 まで、上記のイベントは `moz` 接頭辞を付加していました。

## Mouse イベントの拡張

Pointer Lock API は通常の {{domxref("MouseEvent")}} インターフェイスを、movement 属性で拡張します。新たな 2 つの属性 {{domxref("MouseEvent.movementX","movementX")}} および {{domxref("MouseEvent.movementY","movementY")}} が、マウスポインタの位置の変化を提供します。パラメーターの値は {{domxref("MouseEvent")}} のプロパティである {{domxref("MouseEvent.screenX","screenX")}} および {{domxref("MouseEvent.screenY","screenY")}} の値同士の差と同じであり、それらのプロパティは 2 つ続いて発生する {{event("mousemove")}} イベント `eNow` および `ePrevious` に保存されます。言い換えると、Pointer Lock のパラメーター `movementX` は、`eNow.screenX - ePrevious.screenX` になります。

### ロックされた状態

Pointer Lock が有効であるとき、標準 {{domxref("MouseEvent")}} のプロパティである {{domxref("MouseEvent.clientX","clientX")}}、{{domxref("MouseEvent.clientY","clientY")}}、{{domxref("MouseEvent.screenX","screenX")}}、{{domxref("MouseEvent.screenY","screenY")}} は、マウスが動いていないかのように値が固定されます。{{domxref("MouseEvent.movementX","movementX")}} プロパティおよび {{domxref("MouseEvent.movementY","movementY")}} プロパティが、マウスの位置の変化を提供し続けます。マウスが一方向へ連続的に移動するとしても、{{domxref("MouseEvent.movementX","movementX")}} および {{domxref("MouseEvent.movementY","movementY")}} の値に制限はありません。マウスカーソルは存在せず、ウィンドウから外れたりスクリーンの端で止まったりしないという考え方です。

### ロックが解除された状態

パラメーター {{domxref("MouseEvent.movementX","movementX")}} および {{domxref("MouseEvent.movementY","movementY")}} はマウスのロック状態にかかわらず有効であり、ロックされていない状態でも利便性のために使用できます。

マウスのロックが解除されると、システムカーソルが存在するようになり、ブラウザーがウィンドウ表示に戻ります。このとき、{{domxref("MouseEvent.movementX","movementX")}} および {{domxref("MouseEvent.movementY","movementY")}} は 0 に設定されるかもしれません。

## シンプルな例のウォークスルー

Pointer Lock の使用方法やシンプルな制御システムの設定方法を示すため、[シンプルな Pointer Lock のデモ](https://mdn.github.io/dom-examples/pointer-lock/) を作成しました ([ソースコードを確認する](https://github.com/mdn/dom-examples/tree/master/pointer-lock))。デモは以下のようなものです:

![A red circle on top of a black background.](https://mdn.mozillademos.org/files/7953/pointer-lock.png)

このデモでは、JavaScript を使用して {{htmlelement("canvas")}} 要素上にボールを描画します。canvas をクリックすると Pointer Lock がマウスポインターを取り除いて、マウスを使用してボールを直接動かすことができます。このデモの仕組みを見ていきましょう。

canvas 内の、x および y の初期位置を設定します:

```js
var x = 50;
var y = 50;
```

現在は Pointer Lock のメソッドに接頭辞がついていますので、ブラウザー実装ごとに処理を分けています。

```js
canvas.requestPointerLock = canvas.requestPointerLock ||
                            canvas.mozRequestPointerLock;

document.exitPointerLock = document.exitPointerLock ||
                           document.mozExitPointerLock;
```

canvas がクリックされたときに、canvas で `requestPointerLock()` メソッドを実行するイベントリスナーを設定します。これは、Pointer Lock を開始します。

```js
canvas.onclick = function() {
  canvas.requestPointerLock();
}
```

Pointer Lock イベント `pointerlockchange` のイベントリスナーを設定します。イベントが発生したら、Pointer Lock の変更を制御するために `lockChangeAlert()` という名前の関数を実行します。

```js
// Pointer Lock のイベントリスナー

// さまざまなブラウザ向けに、Pointer Lock の状態変化イベントをフックする
document.addEventListener('pointerlockchange', lockChangeAlert, false);
document.addEventListener('mozpointerlockchange', lockChangeAlert, false);
```

この関数は、pointLockElement プロパティが canvas を示しているかを確認します。示している場合は、マウスの移動を扱うためにイベントリスナーへ `updatePosition()` 関数を設定します。示していない場合は、イベントリスナーを再び削除します。

```js
function lockChangeAlert() {
  if (document.pointerLockElement === canvas ||
      document.mozPointerLockElement === canvas) {
    console.log('The pointer lock status is now locked');
    document.addEventListener("mousemove", updatePosition, false);
  } else {
    console.log('The pointer lock status is now unlocked');
    document.removeEventListener("mousemove", updatePosition, false);
  }
}
```

updatePosition() 関数が、canvas 内のボールの位置 (`x` および `y`) を更新します。また、ボールが canvas の端からはみ出すかをチェックする `if()` 文が含まれています。ボールがはみ出す場合は、反対側の端にボールを描画します。また、[`requestAnimationFrame()`](/ja/docs/Web/API/window/requestAnimationFrame) がすでに呼び出されたかを確認しており、呼び出された場合は必要に応じて再び呼び出して、canvas のシーンを更新するために `canvasDraw()` 関数を呼び出します。さらに、参照用に X および Y の位置を表示するための tracker も設定します。

```js
var tracker = document.getElementById('tracker');

var animation;
function updatePosition(e) {
  x += e.movementX;
  y += e.movementY;
  if (x > canvas.width + RADIUS) {
    x = -RADIUS;
  }
  if (y > canvas.height + RADIUS) {
    y = -RADIUS;
  }
  if (x < -RADIUS) {
    x = canvas.width + RADIUS;
  }
  if (y < -RADIUS) {
    y = canvas.height + RADIUS;
  }
  tracker.textContent = "X position: " + x + ", Y position: " + y;

  if (!animation) {
    animation = requestAnimationFrame(function() {
      animation = null;
      canvasDraw();
    });
  }
}
```

`canvasDraw()` 関数は、現在の `x` および `y` の位置にボールを描画します:

```js
function canvasDraw() {
  ctx.fillStyle = "black";
  ctx.fillRect(0, 0, canvas.width, canvas.height);
  ctx.fillStyle = "#f00";
  ctx.beginPath();
  ctx.arc(x, y, RADIUS, 0, degToRad(360), true);
  ctx.fill();
}
```

## iframe の制限

Pointer Lock は一度に 1 つだけの iframe をロックできます。iframe をひとつロックすると、別の iframe をロックしてターゲットを切り替えようとすることはできません。Pointer Lock はエラーになります。この制限を避けるため、始めにロックされた iframe のロックを解除してから別の iframe をロックしてください。

iframe の既定の動作では、"サンドボックス化された" iframe が Pointer Lock をブロックします。`<iframe sandbox="allow-pointer-lock">` という属性/値の組み合わせによってこの制限を避けられることが、Chrome でまもなく可能になる予定です。

## 仕様

| 仕様書                               | 策定状況                         | コメント   |
| ------------------------------------ | -------------------------------- | ---------- |
| {{SpecName('Pointer Lock')}} | {{Spec2('Pointer Lock')}} | 最初の仕様 |

## ブラウザー実装状況

{{Compat("api.Element.requestPointerLock")}}

## 関連情報

- {{domxref("MouseEvent")}}
