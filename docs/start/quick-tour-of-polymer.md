Polymer 2.0 チュートリアル（日本語）
Polymer 2.0 公式サイトの[クイックツアー](https://www.polymer-project.org/2.0/start/quick-tour)の邦訳です。

> 読みやすいように意訳したり、説明不足と思われる箇所に説明を補足しています。なお、Polymer 1.0以前のコードで利用経験がおありの方は、[About Polymer 2.0](https://www.polymer-project.org/2.0/docs/about_20)や[Polymer 2.0 upgrade guide](https://www.polymer-project.org/2.0/docs/upgrade)を併せて参照してください。主な変更点が簡潔に解説されています。また、Webコンポーネントの概要は、[Web Componentsとは何か？](http://qiita.com/jtakgiuchi/items/b1315f53b3726ff11b61)を参照してください。

Polymerを使えば、宣言的記述により[Webコンポーネント](http://qiita.com/jtakgiuchi/items/b1315f53b3726ff11b61)を簡単に作成することができます。

カスタム要素は、Polymerの提供する以下のような機能を利用でき、シンプルな記述によって複雑でインタラクティブな性質を持ったカスタム要素を容易に構築することができます。：

- カスタム要素の登録
- ライフサイクルコールバック
- プロパティの監視
- Shadow DOMテンプレート
- データバインディング

このチュートリアルでは、[Plunker](https://plnkr.co/)というブラウザベースのエディターを利用することで、何もインストールすることなくPolymerライブラリのクイックツアーを体験できるようにしています。チュートリアル内の[PLUNKERのサンプルコード](#)というリンクをクリックすれば、Plunker上のインタラクティブなサンドボックスの上でサンプルを試すことができます。

また、[LEARN MORE:xxx](#)をクリックすれば、各セクションで紹介した機能に関連するドキュメントの該当ページへ移動できます。(訳注：以下リンク先は拙訳の日本語版です。原文を参照したい方は[公式ドキュメント](https://www.polymer-project.org/2.0/docs/about_20)を参照してください。)

- [公式ドキュメント(邦訳)](http://qiita.com/jtakgiuchi/items/e5160ba7d039ca5b05a4)

## カスタム要素を登録

新しいカスタム要素を登録するには、ES6で導入されたclass構文を使い`Polymer.Element`クラスを拡張した上で、`customElements.define`メソッドを呼び出しカスタム要素をブラウザに登録します。この登録によってカスタム要素名とclass名が関連付けられます。なお、カスタム要素の名前にはASCII文字を使いダッシュ(-)を含める必要があります。

[PLUNKERのサンプルコード](http://plnkr.co/edit/PaCt2M?p=preview)

このサンプルでは、ライフサイクルコールバックをして`<custom-element>`の初期化時にコンテンツを追加しています。初期化が完了すると、`ready`というコールバックが呼び出されます。`ready`コールバックは、カスタム要素の生成後にワンタイムの初期化を行いたい場合に利用できます。
(訳注：`constructor`はPolymer 1.0の`created`に相当します。仕様の改定に併せて変更されました。)

[LEARN MORE:カスタム要素の登録](http://qiita.com/jtakgiuchi/items/8bcc2ef508709839985f)

[LEARN MORE:ライフサイクルコールバック](http://qiita.com/jtakgiuchi/items/8bcc2ef508709839985f#%E3%83%A9%E3%82%A4%E3%83%95%E3%82%B5%E3%82%A4%E3%82%AF%E3%83%AB%E3%82%B3%E3%83%BC%E3%83%AB%E3%83%90%E3%83%83%E3%82%AF)

## Shadow DOMの追加

多くの要素は、独自のUIや動作を実装するために内部にDOMノードを持っています。Polymerの*DOMテンプレート*を使うことで、カスタム要素にShadow DOMというDOMのサブツリーを作成できます。

[PLUNKERのサンプルコード](http://plnkr.co/edit/bVyU2T?p=preview)

Shadow DOMはカスタム要素の内部にカプセル化されています。

[LEARN MORE:DOMテンプレート](http://qiita.com/jtakgiuchi/items/f78b7e494a6e746040f6)

## Shadow DOMを使って要素を作成

Shadow DOMを使うことでカスタム要素を柔軟に構築できます。カスタム要素の子は割り当てられるので、Shadow DOMツリーに挿入されたかのようにレンダリングされます。

このサンプルでは、ロゴイメージをCSSでスタイリングされた`<div>`タグで囲うことで、シンプルなカスタムタグを作成しています。

[PLUNKERのサンプルコード](http://plnkr.co/edit/RJOuQf?p=preview)

> ヒント: `<dom-module>`の内部で定義されたCSSのスタイル情報は、カスタム要素のShadow DOM内にスコープされます。そのため、上記サンプルにおいて`<picture-frame>`内部の`div`に対して適用したスタイルルールは、内部の`<div>`タグに対してのみ適用されます。

[LEARN MORE:ShadowDOMとスロット](http://qiita.com/jtakgiuchi/items/0292178153d39f9cf464#shadow-dom%E3%81%A8%E6%A7%8B%E6%88%90)

## データバインディングを利用

もちろん予め静的にマークアップしたShadow DOMだけは十分でないと考えるでしょう。多くの場面において、Shadow DOMを動的にアップデートしたいと考えるはずです。そのような場合には、*データバインディング*というシステムを使いします。

データバインディングを使えば、簡潔なコードでカスタム要素内部で発生した変化をShadow DOMへ反映させることができます。`{{}}`という記号を使い、コンポーネント内のプロパティとバインドします。例えば`{{foo}}`は、カスタム要素内のプロパティ`foo`の値によって置き換えられます。

[PLUNKERのサンプルコード](http://plnkr.co/edit/l0zSDN?p=preview)

[LEARN MORE:データバインディング](http://qiita.com/jtakgiuchi/items/60f877d907e3d1fd51af)

## プロパティの宣言

プロパティは、カスタム要素が外部へ公開するAPIの重要な一部です。Polymerは、*宣言的なプロパティ*をサポートしており、以下のような一般的な機能を提供します。：

- プロパティにデフォルト値を設定
- マークアップからプロパティを設定
- プロパティの変更を監視して事前に指定した処理(observer)を実行

下記サンプルでは、一つ前に紹介したサンプルに`owner`プロパティの宣言を加えています。`index.html`内のマークアップから`owner`プロパティを設定しているのが分かると思います。

[PLUNKERのサンプルコード](http://plnkr.co/edit/huYt0l?p=preview)

[LEARN MORE:プロパティの宣言](http://qiita.com/jtakgiuchi/items/85d4e636bc490eac699c)

## プロパティへのデータバインディング

Shadow DOMのテキストコンテンツだけでなく、カスタム要素のプロパティに対してもバインドすることができます。(`property-name="[[binding]]"`という記法を使います。)Polymerの`properties`は、任意のオプションとして双方向バインディングもサポートしています。(`property-name="{{binding}}"`のように`{{}}`を使います。)

このサンプルでは、双方向バインディング(two-way binding)を使用しています。カスタム`input`要素(`iron-input`)の`value`と`owner`プロパティがバインドされており、ユーザーがタイプするとカスタム要素のコンテンツもアップデートされます。

[PLUNKERのサンプルコード](http://plnkr.co/edit/SEm7jd?p=preview)

> ヒント: [`<iron-input>`](https://www.webcomponents.org/element/PolymerElements/iron-input)要素は、ネイティブの`<input>`要素のラッパーとして双方向のデータバインディングや入力値のバリデーション機能を提供します。

> 注意: ネイティブの`input`要素(`<input type="number">"`を除く)の`value`との直接的なバインディングはサポートされていません。詳細は、[ドキュメント](http://qiita.com/jtakgiuchi/items/60f877d907e3d1fd51af#%E3%83%97%E3%83%AD%E3%83%91%E3%83%86%E3%82%A3%E3%83%90%E3%82%A4%E3%83%B3%E3%83%87%E3%82%A3%E3%83%B3%E3%82%B0%E3%82%92%E3%82%B5%E3%83%9D%E3%83%BC%E3%83%88%E3%81%97%E3%81%A6%E3%81%84%E3%81%AA%E3%81%84%E3%83%8D%E3%82%A4%E3%83%86%E3%82%A3%E3%83%96%E3%81%AE%E3%83%97%E3%83%AD%E3%83%91%E3%83%86%E3%82%A3)で確認してください。

## `<dom-repeat>`使いテンプレートを連続して描画

テンプレートリピーター(`dom-repeat`)は、配列とのバインドに特化したテンプレートです。配列内の各アイテムにつき一つずつテンプレート内のコンテンツをインスタンス化します。

[PLUNKERのサンプルコード](http://plnkr.co/edit/1KYc2z?p=preview)

[LEARN MORE:テンプレートリピーター(dom-repeat)](http://qiita.com/jtakgiuchi/items/105556142cfd6be278a7#%E3%83%86%E3%83%B3%E3%83%97%E3%83%AC%E3%83%BC%E3%83%88%E3%83%AA%E3%83%94%E3%83%BC%E3%82%BF%E3%83%BCdom-repeat)

## 次のステップ

これでPolymerの基本的なコンセプトは理解できたはずです。あとは、[Polymer App Toolbox](http://qiita.com/jtakgiuchi/items/01a9ae3e54b72645660e)というCLIツールを使って実際にアプリケーションを作成したり、[ドキュメント本文(邦訳)](http://qiita.com/jtakgiuchi/items/e5160ba7d039ca5b05a4)を参照してPolymerライブラリの機能の概要を理解していってください。