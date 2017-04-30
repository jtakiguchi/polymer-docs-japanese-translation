Web Componetsとは何か？

> この記事は、[WebComponents.org/Introduction](https://www.webcomponents.org/introduction)の翻訳です。

## Web Componentsとは何か？
Web componentsは、WebページやWebアプリケーションの中で新たに、再利用可能でカプセル化された独自のHTMLタグを作成するためのWebプラットフォームのAPIです。独自に作成したコンポーネントやウィジェットは、Web componentsの標準をベースに構築されているので、あらゆるモダンブラウザ上で動作するでしょう。また、HTMLと連動して動作するどんなJavascriptライブラリやフレームワークとも併用できます。

Web componentsは、既存のWeb標準をベースにしています。 Web componentsのサポート機能は現在HTMLやDOMの仕様に追加されており、Web開発者はカプセル化されたスタイリングとカスタムの動作を使い新たな要素で簡単にHTMLを拡張できます。

## 仕様

Webコンポーネントは、主に四つの仕様をベースにしています。：

#### Custom Elements

[Custom Elementsの仕様](https://w3c.github.io/webcomponents/spec/custom/)は、
新しいタイプのDOM要素の設計と利用の基盤となります。	

#### Shadow DOM

[Shadow DOMの仕様](https://w3c.github.io/webcomponents/spec/shadow/)は、Web componentsにおけるカプセル化されたスタイルとマークアップの利用法を定義しています。

#### HTML imports

[HTML importsの仕様](https://w3c.github.io/webcomponents/spec/imports/)は、HTML文書の他のHTML文書への取り込みとその再利用を定義しています。

#### HTML Template

[HTML template elementの仕様](https://html.spec.whatwg.org/multipage/scripting.html#the-template-element/)は、マークアップのフラグメント(断片)を宣言する方法を定義しています。このマークアップは、ページの読み込む際は使用されませんが、実行後にインスタンス化される可能性があります。

## どのようにWeb componentsを利用するか？

[WEBCOMPONENTS.ORG](https://www.webcomponents.org/)のコンポーネントは、WebページやWebアプリケーションで使用できる新たなHTML要素を提供します。

カスタム要素を使用するには、それをインポートしHTML文書に新たなタグを追加するだけです。例えば、[Emoji Rain element](https://beta.webcomponents.org/element/notwaldorf/emoji-rain)を使用するには、次のようにします。：


~~~html
<link rel="import" href="../emoji-rain/emoji-rain.html">
...
<emoji-rain active></emoji-rain>
~~~

カスタム要素をインストールするにはいくつかの方法があります。利用したい要素が見つかったら、そのREADMEをみてコマンドでインストールしてください。現在、ほとんどの要素はBowerを使ってインストールできます。 Bowerはコンポーネントの依存対象も併せてインストールします。Bowerの詳細については、[Bower.io](https://bower.io/)を参照してください。

例えば、[Emoji Rain README](https://beta.webcomponents.org/element/notwaldorf/emoji-rain)では、Bowerのインストールプロセスについて説明があります。：

~~~
mkdir emoji-rain-demo && cd emoji-rain-demo
bower install emoji-rain
~~~

## どのように新たなHTML要素を定義するか？

このセクションでは、Web components仕様の新しいクロスブラウザバージョン(v1)の構文について説明します。

JavaScriptを使用して、新しいHTML要素とそのタグを`customElements`グローバルを使って定義します。 customElements.define()を呼び出すには、作成するタグ名と基底となる`HTMLElement`を拡張したJavaScriptのクラスを指定します。

例えば、モバイル向けのドロワーパネル`<app-drawer>`を定義するには、：

~~~javascript
class AppDrawer extends HTMLElement {...}
window.customElements.define('app-drawer', AppDrawer);
~~~

Custom Elements v0仕様では、このためにdocument.registerElement()を使用していました。：

~~~javascript
var XFoo = document.registerElement('x-foo');
document.body.appendChild(new XFoo());
~~~

詳細については、[v0 Custom Elements specification](https://www.html5rocks.com/jp/tutorials/webcomponents/customelements/)に関する記事を参照してください。新しいタグを使用するには：

~~~html
<app-drawer></app-drawer>
~~~

カスタム要素を使うことは、`<div>`や他の要素を使用するのと変わりありません。インスタンスはページ上で宣言したり、JavaScriptで動的に作成したり、イベントリスナーを設定したりすることができます。

~~~html
<script>
// Create with javascript
var newDrawer = document.createElement(‘app-drawer’);
// Add it to the page
document.body.appendChild(newDrawer);
// Attach event listeners
document.querySelector(‘app-drawer’).addEventListener(‘open’, function() {...});
</script>
~~~

## Shadow Rootを作成、利用する

このセクションでは、Shadow DOM仕様の新しいクロスブラウザバージョン(v1)を元にShadow DOMを作成するための構文について解説します。Shadow DOMは、コンポーネントを構築するのに便利な新しいDOM機能です。Shadow DOMは、要素内におけるスコープ付サブツリーと考えることができます。

Shadow Rootは、ホスト要素にアタッチされるdocument fragmentです。Shadow Rootを追加するということは、その要素がShadow DOMを取得するということです。要素のSahdow DOMを作成するには、 `element.attachShadow()`を呼び出します。：

~~~javascript
const header = document.createElement('header');
const shadowRoot = header.attachShadow({mode: 'open'});
shadowRoot.innerHTML = '<h1>Hello Shadow DOM</h1>'; // Could also use appendChild().
// header.shadowRoot === shadowRoot
// shadowRoot.host === header
~~~

Shadow DOM v0仕様では、Shadow DOMを作成するために少々異なる方法が用意されていました。：

~~~javascript
var root = host.createShadowRoot();
~~~

詳細は、[shadow DOM v0](https://www.html5rocks.com/jp/tutorials/webcomponents/shadowdom/)を参照してください。 [Hayato Ito's comparison of v0 and v1 of the shadow DOM specification](http://hayato.io/2016/shadowdomv1/)も併せてご覧ください。

## Web componentsを構築するためのライブラリ

既に多くのライブラリが存在しており、Web componentsを手軽に作成できます。足を踏み入れ、独自のコンポーネントを作成するには、以下に紹介するライブラリを使って試してみて下さい。：

- [Bosonic](https://bosonic.github.io/)は、Web開発者の日々のニーズに応えるコンポーネントのコレクションです。
- [Polymer](https://www.polymer-project.org/)は、カスタム要素の作成するための機能セットを提供しています。
- [SkateJS](https://github.com/skatejs/skatejs)はWeb conponentsを記述するための軽量なJavascriptライブラリです。
- [X-Tag](https://x-tag.github.io/)は、コンポーネントの開発者にインターフェイスを提供するオープンソースのJavascriptライブラリです。
- [Slim.js](http://slimjs.com/)は、ES6のネイティブのクラス継承を利用して、コンポーネントにデータバインディングと拡張機能を提供する軽量なオープンソースのWeb componentライブラリです。

