# Polymerドキュメント(日本語) Shadow DOM & styling/DOM templating 〜DOMテンプレート〜

多くの要素は、その機能の実装にDOM要素のサブツリーを利用しています。DOMテンプレートを利用することで、要素にDOMのサブツリーを簡単に作成することができます。

デフォルトでは、要素にDOMテンプレートを追加すると、Polymerは要素にShadow Rootを作成し、テンプレートをShadow Tree内部に複製(clone)します。

また、DOMテンプレートによってデータバインディングと宣言型イベントハンドラが利用できるようになります。

## DOMテンプレートの概要

要素のDOMテンプレートを記述するには：

1. 要素の名前と同名の`id`属性を持つ`<dom-module>`要素を作成します。
2. `<dom-module>`の内部に`<template>`要素を作成します。

Polymerは、このテンプレートの内容を要素のローカルDOM内部に複製(clone)します。

例：

~~~html
<dom-module id="x-foo">

  <template>I am x-foo!</template>

  <script>
    class XFoo extends Polymer.Element {
      static get is() { return  'x-foo' }
    }
    customElements.define(XFoo.is, XFoo);
  </script>

</dom-module>
~~~

この例では、DOMテンプレートとその要素を定義するJavaScriptが同じファイルにあります。これらを別々のファイルに分割して配置することもできますが、DOMテンプレートの解析は要素が定義される前に行われる必要があります。

> **注意**：テスト環境を除き、要素はメインドキュメントの外で定義すべきです。メインドキュメント内における要素の定義に関する注意事項は、[main document definitions](https://github.com/jtakiguchi/polymer-docs-japanese-translation
/blob/master/docs/polymer2/custom-elements/define-an-element.md#main-document-definitions)を参照してください。

## ノードの自動探索

Polymerは、要素がDOMテンプレートを初期化する際に、ノードIDの静的マップを作成し、頻繁に使用されるノードに手軽にアクセスできるようにします。手動でクエリを記述する必要はありません。要素のテンプレートに`id`付きで記述されたノードはそれぞれ、`id`によってハッシュ化され`this.$`として格納されます。

> 注意：データバインディングを使用して動的に作成されたノード(`dom-repeat`テンプレートや`dom-if`テンプレートによるものが含まれます)は、ハッシュ`this.$`には追加されません。ハッシュには、静的に作成されたローカルDOMノード(つまり要素の最も外側のテンプレートに定義されたノード)だけが含まれます。

例：

~~~html
<dom-module id="x-custom">

  <template>
    Hello World from <span id="name"></span>!
  </template>

  <script>
    class MyElement extends Polymer.Element {
      static get is() { return  'x-custom' }
      ready() {
        super.ready();
        this.$.name.textContent = this.tagName;
      }
    }
  </script>

</dom-module>
~~~

要素のShadow DOM内に動的に生成されたノードを配置する場合、標準DOMの`querySelector`メソッドを利用してください。

~~~javascript
this.shadowRoot.querySelector(selector)
~~~
