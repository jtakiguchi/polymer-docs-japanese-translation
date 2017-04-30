# Polymerドキュメント(日本語) Feature overview 〜Polymerの概要〜

> Polymer公式サイトの[ドキュメント](https://www.polymer-project.org/2.0/docs/devguide/feature-overview)本体と[ツールボックス](https://www.polymer-project.org/2.0/toolbox/)の解説部分を翻訳しました。訳出作業が大方片付いたので(ドキュメント全体の8割くらい)校正の済んだものから順に上げていきます。後ほど、翻訳プロジェクトとしてGithub上に公開する予定なので、誤訳の指摘や改善点等はそちらにお寄せ頂けますと幸いです。
(注)リンクについて飛べないものがありますが後で対処します。

Polymerライブラリはカスタム要素(Custom Elements)を作成するための機能一式を提供します。これらの機能は、標準のDOM要素のように動作するカスタム要素を迅速かつ容易に作成できるように設計されています。標準的なDOM要素と同様、Polymer要素では以下のようなことが可能です。：

- コンストラクタまたは`document.createElement`を使用してインスタンス化する。
- 属性またはプロパティを使用して構成する。
- 各インスタンスに内部DOMを追加する。
- プロパティや属性の変化に応じて処理を行う（例えば、DOMにデータを追加したり、イベントを発火させるなど）。
- 内部のデフォルトから、あるいは外部からスタイルを設定する。
- 内部の状態を操作するメソッドに応答して処理する。

基本的なPolymer要素の定義は以下のようになります。：

~~~html
    <dom-module id="x-custom">
      <!-- Optional shadow DOM template -->
      <template>
        <style>
          /* CSS rules for your element */
        </style>

        <!-- shadow DOM for your element -->

        <div>{{greeting}}</div> <!-- data bindings in local DOM -->
      </template>

      <script>
        // Define the element's API using an ES2015 class
        class XCustom extends Polymer.Element {

          static get is() { return 'x-custom'; }

          // Declare properties for the element's public API
          static get properties() {
            return {
              greeting: {
                type: String,
                value: "Hello!"
              }
            }
          }

          // Add methods to the element's public API
          greetMe() {
            console.log(this.greeting);
          }

        }

        // Register the x-custom element with the browser
        customElements.define(XCustom.is, XCustom);
      </script>

    </dom-module>
~~~

このドキュメントでは、機能を次のグループに分けて解説しています。：

- [カスタム要素](https://github.com/jtakiguchi/polymer-docs-japanese-translation
/blob/master/docs/custom-elements/custom-elements-concepts.md)：要素を登録すると、class名がカスタム要素名に関連付けられます。この要素は、ライフサイクルを管理するコールバックを提供します。また、Polymerでは、プロパティを宣言することで、要素のプロパティAPIをPolymerのデータシステムに統合することもできます。

- [Shadow DOM](https://github.com/jtakiguchi/polymer-docs-japanese-translation
/blob/master/docs/shadow-dom-and-styling/shadow-dom-concepts.md)：Shadow DOMは、カスタム要素内にカプセル化されたローカルのDOMツリーを提供します。PolymerはDOMテンプレートからShadow Treeを自動的に生成し、カスタム要素に挿入することができます。

- [イベント](https://github.com/jtakiguchi/polymer-docs-japanese-translation
/blob/master/docs/events/handle-and-fire-events.md)：Polymerは、Shadow DOMの子にイベントリスナーをアタッチするための宣言的構文を提供します。また、ジェスチャー関連イベントを処理するためのオプションのライブラリも用意しています。

- [データシステム](https://github.com/jtakiguchi/polymer-docs-japanese-translation
/blob/master/docs/data-system/data-system-concepts.md)：Polymerのデータシステムは、プロパティオブザーバー(Property Observer)や算出プロパティ(Computed Properties)といった機能によって、プロパティや属性へのデータバインディングを提供しています。

Polymer 1.xベースの既存の要素を新しいAPIにアップグレードする場合は、[Upgrade guide](https://www.polymer-project.org/2.0/docs/upgrade)を参照してください 。

リリースの最新の状況を確認したい場合は、[Release notes](https://www.polymer-project.org/2.0/docs/release-notes)を参照してください。