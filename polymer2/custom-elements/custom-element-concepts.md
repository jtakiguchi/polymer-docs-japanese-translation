# Polymerドキュメント(日本語) Custom elements/Custom element concepts 〜カスタム要素のコンセプト〜

カスタム要素(Custom Elements)は、Webにコンポーネントモデルを提供します。カスタム要素の仕様は次の通りです。：

- クラスをカスタム要素の名前に関連付けるためのメカニズム。
- カスタム要素のインスタンスの状態が変化した（例えば、ドキュメントに追加またはドキュメントから削除された）際に呼び出される一連のライフサイクルコールバック。
- インスタンス上で指定した属性グループのいずれかが変更された際に呼び出されるコールバック。

まとめると、これらの機能を利用することで、状態変化に応じて処理を行う独自のパブリックAPIを持った要素が構築できます。

このドキュメントでは、Polymerに関連するカスタム要素の概要について説明します。カスタム要素のより詳細な概要については、[Custom Elements v1: Reusable Web Components](https://developers.google.com/web/fundamentals/getting-started/primers/customelements)を参照してください。

カスタム要素を定義するには、ES6のクラスを作成し、それをカスタム要素の名前に関連付けます。

~~~javascript
// Create a class that extends HTMLElement (directly or indirectly)
class MyElement extends HTMLElement { … };

// Associate the new class with an element name
window.customElements.define('my-element', MyElement);
~~~

標準の要素と同じように、カスタム要素を利用できます。：

~~~
<my-element></my-element>
~~~

または：

~~~
var myEl = document.createElement('my-element');
~~~

または：

~~~
var myEl = new MyElement();
~~~

要素のクラスには、その動作(behavior)とパブリックAPIを定義します。クラスは、`HTMLElement`クラスまたは、そのサブクラスの一つ（例えば、他のカスタム要素）を拡張しなければいけません。

> 仕様上、***カスタム要素の名前は、小文字のASCII文字で始まり、ダッシュ(-)を含まなければなりません。***既出の名前は短いリストで管理され、それに一致する命名は禁止されています。詳細については、HTML仕様の[Custom elements core concepts](https://html.spec.whatwg.org/multipage/scripting.html#custom-elements-core-concepts)を参照してください。

Polymerは、基本的なカスタム要素の仕様に対して付加的な機能群を提供します。これらの機能を要素に付加するには、Polymer要素の基底クラス`Polymer.Element`を拡張します。：

~~~html
<link rel="import" href="/bower_components/polymer/polymer_element.html">

<script>
  class MyPolymerElement extends Polymer.Element {
    static get is() { return 'my-polymer-element'; }
  }

  window.customElements.define(MyPolymerElement.is, MyPolymerElement);
</script>
~~~

Polymerでは、クラスは要素名を返すgetterメソッドとして`is`を準備する必要があります。
Polymerは基本的なカスタム要素に対して以下の機能を付与します。

- 一般的なタスクを処理するためのインスタンスメソッド。
- 対応する属性に応じてプロパティを設定するなど、プロパティと属性を自動的に処理するための機能。
- `<template>`の記述を元に要素のインスタンスにShadow DOMツリーを生成する。
- データバインディング、プロパティ変更のオブザーバーや算出プロパティをサポートするデータシステム。

### カスタム要素のライフサイクル

カスタム要素の仕様では、「カスタム要素の反応(reactions)」と呼ばれる一連のコールバックが定義されています。これによって、特定のライフサイクルの変化に応じてユーザーコードを実行することができます。

|**コールバック/リアクション**|**タイミング**|
|:--|:--|
|constructor|要素がアップグレードされたとき（つまり、要素が作成されたとき(created)、あるいは以前に作成された要素が定義された(defined)とき）に呼び出されます。|
|connectedCallback|要素がドキュメントに追加されたときに呼び出されます。|
|disconnectedCallback|要素がドキュメントから削除されたときに呼び出されます。|
|attributeChangedCallback|要素のいずれかの属性が変更、追加、削除または置換されたときに呼び出されます。|

各リアクション(訳注：リアクションはコールバックの仕様上の呼称)は、実装の最初の行で、スーパークラスのコンストラクタまたはリアクションを呼び出す必要があります。`constructor`の場合には、以下のように単に`super()`を呼び出すだけです。

~~~javascript
constructor() {
  super();
  // …
}
~~~

その他リアクションについては、スーパークラスのメソッドを呼び出します。これは、Polymerが要素にライフサイクルコールバックを導入するために必要になります。

~~~javascript
connectedCallback() {
  super.connectedCallback();
  // …
}
~~~

要素のコンストラクタにはいくつか特別な制限があります。：

- コンストラクタ本体の最初の行で、`super`メソッドを引数なしで呼び出さなければなりません。
- 単純な早期return（`return`または`return this`）を意図とするのでない限り、コンストラクタにreturn文を含めることはできません。
- コンストラクタで要素自身の属性や子を調べたり追加したりすることはできません。

コンストラクタの制限事項について完全なリストは、WHATWGが公開するHTML仕様の[Requirements for custom element constructors](https://html.spec.whatwg.org/multipage/scripting.html#custom-element-conformance)を参照してください。

可能であれば常に、コンストラクタ内ではなく、`connectedCallback`より後に遅延して実行するようにしてください。

#### ワンタイムの初期化

カスタム要素の仕様では、ワンタイムの初期化コールバックは提供されません。そこでPolymerは、要素がDOMに初めて追加されたときだけ呼び出される`ready`コールバックを用意しています。

~~~
ready() {
  super.ready();
  // When possible, use afterNextRender to defer non-critical
  // work until after first paint.
  Polymer.RenderStatus.afterNextRender(this, function() {
    ...
  });
}
~~~

`Polymer.Element`クラスは、`ready`コールバックの中で要素のテンプレートやデータシステムを初期化します。したがって、`ready`コールバックを上書きする場合には、独自の`ready`のどこかで`super.ready()`呼び出す必要があります。

スーパークラスの`ready`メソッドから戻ると、要素のテンプレートはインスタンス化され、初期プロパティ値が設定された状態になります。ただし、Light DOM要素は、`ready`が呼び出された時点で割り当てられて(distributed)いないかもしれません。

要素のLight DOMの子やプロパティ値のように、動的な値を元に要素を初期化する場合には、`ready`コールバックを使用しないでください。代わりに、プロパティの変更であれば[オブザーバー](https://github.com/jtakiguchi/polymer-docs-japanese-translation
/blob/master/docs/polymer2/data-system/observer-and-computed-properties.md)を設定し、追加・削除される子に対しては`observeNodes`メソッドや`slotChanged`イベントで監視を行ってください。

関連トピック：
- [DOMテンプレート](https://github.com/jtakiguchi/polymer-docs-japanese-translation
/blob/master/docs/polymer2/shadow-dom-and-styling/dom-templating.md)
- [データシステムのコンセプト](https://github.com/jtakiguchi/polymer-docs-japanese-translation
/blob/master/docs/polymer2/data-system/data-system-concepts.md)
- [オブザーバーと算出プロパティ](https://github.com/jtakiguchi/polymer-docs-japanese-translation
/blob/master/docs/polymer2/data-system/observer-and-computed-properties.md)
- [子の追加と削除を監視](https://github.com/jtakiguchi/polymer-docs-japanese-translation
/blob/master/docs/polymer2/shadow-dom-and-styling/shadow-dom-concepts.md#observe-added and-removed-children)


## 要素のアップグレード

仕様によれば、カスタム要素は定義する前であっても利用することができます。要素の定義を追加すると、既存の要素のインスタンスはすべてカスタムクラスにアップグレードされます。

例として、次のようなコードを考えます。：

~~~html
<my-element></my-element>
<script>
  class MyElement extends HTMLElement { ... };

  // ...some time much later...
  window.customElements.define('my-element', MyElement);
</script>
~~~

このページを解析すると、ブラウザはスクリプトを解析して実行する前に`<my-element>`のインスタンスを作成します。この場合、要素は`MyElement`ではなく`HTMLElement`のインスタンスとして生成されます。要素が定義されると、`<my-element>`のインスタンスはアップグレードされ適切なクラス(`MyElement`)になります。クラスのコンストラクタは、アップグレードの過程で呼び出され、その後他の待機中のライフサイクルコールバックが続けて呼び出されます。

要素をアップグレードさせることで、要素の初期化にかかるコストを遅延させながらDOMに追加することができます。これは進歩的な機能の強化といえるでしょう。

要素は、次のいずれかの*カスタム要素の状態*を持っています。

- "uncustomized"：要素には有効なカスタム要素名がありません。これは、ビルトイン要素(`<p>`、`<input>`)または、カスタム要素になることができない未知の要素(`<nonsense>`)のどちらかです。
- "undefined"：要素に有効なカスタム要素名(例えば、my-elementのような)はありますが、まだ定義されていません。
- "custom"：要素は有効なカスタム要素名を持ち、定義もなされ、アップグレードもされています。
- "failed"：要素のアップグレードに失敗しました（例えば、クラスが無効な場合）。

*カスタム要素の状態*はプロパティとして公開はされませんが、要素が定義済みかどうかに関わらずスタイルを設定することができます。

"custom"及び"uncustomized"状態にある要素は、定義済み(defied)であるとみなされます。定義済みの要素に対しては、擬似クラスセレクタ`:defined`を使用することができます。これを利用して、要素がアップグレードされる前のプレースホルダ用スタイルを提供できます。：

~~~~javascript
my-element:not(:defined) {
  background-color: blue;
}
~~~~

## 他の要素の拡張

カスタム要素は、HTMLElementだけでなく他のカスタム要素を拡張することもできます。：

~~~javasctipt
class ExtendedElement extends MyElement {
  static get is() { return 'extended-element'; }

  static get properties() {
    return {
      thingCount: {
        value: 0,
        observer: '_thingCountChanged'
      }
    }
  }
  _thingCountChanged() {
    console.log(`thing count is ${this.thingCount}`);
  }
};
window.customElements.define(ExtendedElement.is, ExtendedElement);
~~~

> **Polymerは現在、ビルトイン要素の拡張をサポートしていません。**カスタム要素の仕様では、`<button>`や`<input>`のようなビルトイン要素を拡張するためのメカニズムを用意します。仕様では、これらの要素を「カスタマイズされたビルトイン要素(customized built-in elements)」と呼んでいます。__カスタマイズされたビルトイン要素__には、多くの利点があります。（例えば、`<button>`や`<input>`のようなビルトインUI要素でユーザー補助機能(accessibility feature)を利用することができます）しかし、すべてのブラウザベンダーが__カスタマイズされたビルトイン要素__をサポートすることに同意おらず、現時点でPolymerはそれらをサポートしていません。

### クラス式のミックスインでコードを共有

ES6のクラスでは単一継承のみサポートしており、異なる要素間でコードを共有するには困難が伴います。クラス式のミックスインを利用すると、要素間でコードを共有できるようになります。

クラス式のミックスインは基本的にクラスのファクトリーとして機能する関数です。以下の例のように、スーパークラスを渡すことで、関数はミックスインのメソッドを使いスーパークラスを拡張した新たなクラスを生成します。

~~~javascript
MyMixin = function(superClass) {

  return class extends superClass {

    constructor() {
      super()
      this.addEventListener('keypress', e => this.handlePress(e));
    }

    static get properties() {
      return {
        bar: {
          type: Object
        }
      }
    }

    static get observers() {
      return [ '_barChanged(bar.*)' ]
    }

    _barChanged(bar) { ... }

    handlePress(e) { console.log('key pressed: ' + e.charCode) }
  }
}
~~~

ミックスインは、通常の要素のクラスのように、プロパティ、オブザーバーやメソッドを定義することができます。

要素にミックスインを追加するには以下のように記述します。：

~~~javascipt
class MyElement extends MyMixin(Polymer.Element) {
  static get is() { return 'my-element' }
}
~~~

これにより、`MyMixin`ファクトリ関数を使って定義された新しいクラスが生成されます。継承の階層は次のようになります。

~~~javascipt
MyElement <= MyMixin(Polymer.Element) <= Polymer.Element
~~~

複数のミックスインを順々に(in sequence)適用することもできます。：

~~~javascipt
class AnotherElement extends AnotherMixin(MyMixin(Polymer.Element)) { … }
~~~

## 参考情報

詳細情報：[Custom Elements v1：reusable web components](https://developers.google.com/web/fundamentals/primers/customelements/?hl=ja)