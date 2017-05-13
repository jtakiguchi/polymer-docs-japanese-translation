Polymer App Toolbox(日本語) What’s in the box 〜App Toolboxの概要〜

Polymer App Toolboxは、Polymerを使用して[Progressive Web Apps(PWA)](https://developers.google.com/web/progressive-web-apps/)を構築するためのコンポーネントやツール、テンプレートのコレクションです。App Toolboxの機能は以下の通りです。：

 - PolymerとWebコンポーネントを利用したコンポーネント指向のアーキテクチャ
 - [\<app-layout>](https://www.webcomponents.org/element/PolymerElements/app-layout)コンポーネントを利用したレスポンシブルデザイン
 - [\<app-route>](https://www.webcomponents.org/element/PolymerElements/app-route)要素を使用したモジュラールーティング
 - [\<app-localize-behavior>](https://www.webcomponents.org/element/PolymerElements/app-localize-behavior)によるローカリゼーション
 - [\<app-storage>](https://www.webcomponents.org/element/PolymerElements/app-storage)要素によるローカルストレージの簡易なサポート
 - [Service Worker](https://developers.google.com/web/fundamentals/getting-started/primers/service-workers?hl=ja)を使った、オフラインキャッシュによる[Progressive Enhancement](https://en.wikipedia.org/wiki/Progressive_enhancement)
 - ビルドツールは複数のアプリケーション配信手段をサポートしており、サーバープッシュを使うHTTP/2向けにはunbundledファイルを配信し、HTTP/1向けにはbundledファイルを配信します。

これらコンポーネントのいずれか一つを個別に使用することも、それらを併用してフル機能のProgressive Web Apps(PWA)を構築することもできます。最も重要なのは、各コンポーネントが付加的(additive)であることです。シンプルなアプリであれば、`app-layout`だけで十分かもしれません。アプリが複雑化するにつれ、必要に応じてルーティング、オフラインキャッシュ、ハイパフォーマンスな配信方法を追加することができます。

> **ハイブリッド互換** Toolboxの要素と機能には、Polymer 1とPolymer 2の両方で利用可能なハイブリッド版が用意されています。2.0リリース候補(RC)を使う場合は、要素の`2.0-preview`ブランチを使用してください。

これらのコンポーネントの実際の動作を体感したい場合は、次のいずれかのデモアプリケーションを試してみてください。：

- [Shop](https://shop.polymer-project.org/)：Shopは、ツールボックスを使用して構築された、フル機能を備えたECのPWAデモです。ビルド方法は、[Case study: the Shop app](https://www.polymer-project.org/2.0/toolbox/case-study)を読んでください。

- [News](https://news.polymer-project.org/list/top_stories)：NewsはShopのようなフル機能のPWAのデモですが、コンテンツの配信に焦点を当てています。ビルド方法は、[Case study: the News app](https://www.polymer-project.org/1.0/toolbox/news-case-study)を読んでください。

App Toolboxの利用を開始するには、[App Toolboxでアプリを構築](https://www.polymer-project.org/2.0/start/toolbox/set-up)を参照してください。

または、[レスポンシブアプリのレイアウト](https://www.polymer-project.org/2.0/toolbox/app-layout)を読んでみてください。

[BUILD AN APP](https://www.polymer-project.org/2.0/start/toolbox/set-up)

[RESPONSIVE APP LAYOUT](https://www.polymer-project.org/2.0/toolbox/app-layout)
