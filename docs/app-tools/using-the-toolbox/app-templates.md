Polymer App Toolbox(日本語) Using the Toolbox/App templates 〜アプリケーションのテンプレート〜

Polymer App Toolboxの利用は、Polymer CLIを使い、ここで紹介される要素やパターンが組み込まれたテンプレートから一つを選んで始めることができます。

## テンプレートからプロジェクトを初期化

テンプレートからプロジェクトを初期化するには、[Polymer CLI](https://www.polymer-project.org/2.0/docs/tools/polymer-cli)がインストールされていることを確認し、空のプロジェクトフォルダに`cd`で移動し、次のコマンドを実行するだけです。そうすると現在利用可能なテンプレートから一つ選択するよう促されます。

~~~
    $ polymer init
~~~

## テンプレート

### Application

`application`テンプレートは、Polymerで構築されるアプリケーションの最も基本的な出発点です。アプリケーションのルート(root)として配信可能な必要最小限の実装を備えたカスタム要素が一つ用意されています。非常に高い柔軟性を持っており、そこから思うままにアプリケーションを構築していけます。

### Starter Kit


<img src="https://www.polymer-project.org/images/1.0/toolbox/starter-kit.png" width="480" alt="Starter Kitのイメージ図">

`starter-kit`は[app-layout](https://github.com/jtakiguchi/polymer-docs-japanese-translation
/blob/master/docs/app-toolbox/responsive-app-layout.md)要素を取り入れ、汎用的なレフトドロワーパネルとツールバーを備えています。テンプレートは、メインコンテンツエリアへ読み込み描画される複数のビュー間にナビゲーションを提供します。

テンプレートは、アプリケーションの効率的かつ進歩的な(progressive)ローディングのため[PRPLパターン](https://github.com/jtakiguchi/polymer-docs-japanese-translation
/blob/master/docs/app-toolbox/serve-your-app.md)を用いてセットアップされます。PRPLパターンでは、ビューは必要に応じて読み込まれ、オフライン環境やその後の利用に備えてプリキャッシュされます。

### Shopアプリケーションデモ

<img src="https://www.polymer-project.org/images/1.0/toolbox/shop-template-desktop.png" width="480" alt="Shopデモのイメージ図">

`shop`テンプレートは、`starter-kit`上に構築された本格的なアプリケーションで、PWA仕様の完全なECアプリケーションを構成する要素一式を実装しています。このテンプレートは、「home - list - detail」型の典型的なアプリケーションフローの見本であり、出発点となるイメージや必要な機能一式を備えたアプリケーションの雛形を提供します。

詳細については、[Shop case study](https://www.polymer-project.org/2.0/toolbox/case-study)を参照してください。

### Newsアプケーションデモ

<img src="https://www.polymer-project.org/images/1.0/toolbox/news-template-desktop.png" width="480" alt="Shopデモのイメージ図">

`news `テンプレートは、`starter-kit`上に構築された本格的なアプリケーションで、PWA仕様の完全なNewsアプリケーションを構成する要素一式を実装しています。このテンプレートは、ニュース記事のロードをデモンストレートし、出発点となるイメージや必要な機能一式を備えたアプリケーションの雛形を提供します。

実装の詳細については、[News case study](https://www.polymer-project.org/1.0/toolbox/news-case-study)を参照してください。Newsのテンプレートの使用方法やカスタマイズ方法については、[News documentation site](https://news-docs.polymer-project.org/)を参照してください。

## 次に進むところ

テンプレートは出発点であり、アプリケーションのニーズに合わせて、Polymer App Toolboxのドキュメント内で紹介されるWebコンポーネントに限らず、[WebComponents.org](https://www.webcomponents.org/)のような外部のソースからも自由にコンポーネントを追加することができます。

App Toolboxのテンプレートの利用を開始するためのチュートリアルは、[Building your first Polymer application](https://www.polymer-project.org/2.0/start/toolbox/set-up)を参照してください。