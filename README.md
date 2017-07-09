# Polymer2.0公式ドキュメント邦訳

このページは[Polymer2.0の公式ドキュメント](https://www.polymer-project.org/2.0/docs/devguide/feature-overview)の邦訳を目的とした、公開のボランティアプロジェクトです。また、ドキュメントの理解に役立つ情報も併せて提供します。

ページの管理方針は以下の通りです。
- 下記の進捗表で未着手のドキュメントについてはマークダウンで記述した翻訳をPull Requestでお送りください。
- 誤訳の指摘や翻訳の改善点があれば、Pull RequestやIssueでお知らせください。
- ドキュメント内で理解が困難な箇所はIssueを立ててみんなで議論し知識を共有しましょう。
- Wikiページを活用して、ドキュメントを読む上で役立つ追加の情報を公開できたらと考えています。(内部実装解説、本家の重要なissue、実用的なノウハウ、アンチパターン、仕様策定の動向など)

## 翻訳ポリシー

### 目的と想定読者
日本におけるWeb Components及びPolymerの普及を目的とし、Web ComponentsやPolymerについては聞いたことはないが、フロントエンド開発はある程度経験がある方以上に向けて情報を提供します。

### 方針
- 公式ドキュメントと極力スタイルを合わてマークダウンで記述する。
- リファレンスとしての利便性を考慮して厳密訳に固執せず適宜意訳する。
- 変数/プロパティ/属性/オブジェクト/メソッド等のコード内の識別子は英語のままにしバッククオートで括る。
- 英文の単数/複数の違いについては、原則区別しない。ただし意味上、その区別が重要な場合は適宜訳語を工夫する。
- 訳したが原語が理解の役に立つかもしれない箇所にはかっこ書で添える。
- 一部のパンクチュエーション(:や-)は日本語においてもそのまま利用する。
- 訳者がコメントを加える場合は、「訳注：〜や訳補：〜」と添えてコメント

### ライセンス
原文の[CC BY 3.0](https://creativecommons.org/licenses/by/3.0/deed.ja)を継承します。

### 免責
このページで提供されるドキュメントの利用によって生じたいかなる損害もその責任を負い兼ねます。必要に応じて原文を参照してください。

### 訳語
|原語|訳語|備考|
|:--|:--|:--|
|array item|配列のアイテム|カスタム要素やDOM要素の「要素(elements)」と区別するためアイテムで統一|
|array mutation|配列の変更||
|annotated|アノテーション付き||
|annotation|アノテーション||
|behavior|動作|Polymer 1.0のプロパティ名を指す場合は英語のまま|
|changed record|変更レコード||
|complex observer|複雑なオブザーバー||
|compound binding|複合バインディング||
|computed binding|算出バインディング||
|computed properties|算出プロパティ||
|computing function|算出関数|計算関数とすると一般的すぎるため|
|connect/connection|コネクトする/コネクション|データバインディングの説明で登場します。|
|custom css property|カスタムCSSプロパティ||
|custom element(s)|カスタム要素|WHATWGの仕様を指す言葉として使われた場合は、英語で表記|
|data binding|データバインディング||
|declarative|宣言的||
|dependency/dependent|依存部/依存関係にある||
|distributed node|原語まま||
|getter|getterメソッド||
|imperative|命令的||
|Light DOM|原語まま||
|listen|監視する||
|mixin|ミックスイン||
|multi-property observers|マルチプロパティオブザーバー||
|mutable/immutable|可変/不変||
|observable|監視可能||
|observer|オブザーバー||
|polymer elements|Polymer要素||
|propagation|伝播||
|property-change notifications|プロパティ変更通知||
|property effect|プロパティエフェクト||
|setter|setterメソッド||
|shadow DOM|Shadow DOM||
|Shadow tree|Shadow Tree||
|shady DOM|Shady DOM||
|simple observer|単純なオブザーバー||
|single property observers|シングルプロパティオブザーバー||
|slot|スロット||
|stamp|スタンプ|テンプレートの説明で動詞として頻繁に登場します。テンプレートからインスタンス化するようなイメージです。|
|type-extention|タイプ拡張||

## プロジェクト
### 進捗表
||||参照|着手|試訳|校正|備考|
|:--|:--|:--|:--|:--|:--|:--|:--|
|Start|Get started|||[ ]|[ ]|[ ]||
||Quick tour of Polymer||5/13/17|[x]|[x]|[x]||
||Install Polymer 2.x|||[ ]|[ ]|[ ]||
|Polymer|Feature overview||4/21/17|[x]|[x]|[x]||
||About this release|What's new in 2.0|4/21/17|[x]|[x]|[x]||
|||Upgrade guide||[ ]|[ ]|[ ]||
|||Heybrid elemnets||[ ]|[ ]|[ ]||
|||Release notes||[ ]|[ ]|[ ]||
||Custom elements|Custom element concepts|4/21/17|[x]|[x]|[x]||
|||Define an element|4/21/17|[x]|[x]|[x]||
|||Declare properties|4/21/17|[x]|[x]|[x]||
||Shadow DOM & styling|Shadow DOM concepts|4/21/17|[x]|[x]|[x]||
|||DOM templating|4/21/17|[x]|[x]|[x]||
|||Style shadow DOM|4/21/17|[x]|[x]|[x]||
|||Custom CSS properties|4/21/17|[x]|[x]|[x]||
||Events|Handle and fire events|4/21/17|[x]|[x]|[x]||
|||Gesture events|4/21/17|[x]|[x]|[x]||
||Data system|Data system concepts|4/21/17|[x]|[x]|[x]||
|||Work with object and array data|4/21/17|[x]|[x]|[x]||
|||Observers and computed properties|4/21/'17|[x]|[x]|[x]||
|||Data binding|4/21/17|[x]|[x]|[x]||
|||Helper elements|4/21/17|[x]|[x]|[x]||
||Resources|Overview|7/9/17|[x]|[x]|[ ]||
|||Polyfills||[ ]|[ ]|[ ]||
|||ES6||[ ]|[ ]|[ ]||
||Tools|Tools overview|4/21/17|[x]|[x]|[x]||
|||Polymer CLI||-|-|-|情報の鮮度が大事な箇所なので飛ばした|
|||Document your elements||-|-|-|2.0向けのアップデートが完了していないので飛ばした|
|||Test your elements||[ ]|[ ]|[ ]||
|||Oprimize for production|4/21/17|[x]|[x]|[x]||
|||Advance tools||[ ]|[ ]|[ ]||
|||Services||[ ]|[ ]|[ ]||
|||polymer.json specification||[ ]|[ ]|[ ]||
|||Node support||[ ]|[ ]|[ ]||
||Resources|Glossary||[ ]|[ ]|[ ]||
||API Reference|API Reference||[ ]|[ ]|[ ]||
|||Global settings|7/9/17|[x]|[x]|[ ]||
|App Toolbox|What's in the box?||4/21/17|[x]|[x]|[x]||
||Using the Toolbox|App templates|4/21/17|[x]|[x]|[x]||
|||Responsive app layout|4/21/17|[x]|[x]|[x]||
|||Routing|4/21/17|[x]|[x]|[x]||
|||Localization|4/21/17|[x]|[x]|[x]||
|||App storage|4/21/17|[x]|[x]|[x]||
|||Service worker|4/21/17|[x]|[x]|[x]||
||Deploy|Build for production||[ ]|[ ]|[ ]||
|||Serve your app||[ ]|[ ]|[ ]||
|||The PRPL pattern||[ ]|[ ]|[ ]||
||Case study|Shop||[ ]|[ ]|[ ]||
|||News||[ ]|[ ]|[ ]||
|Blog||||||||
|Others|WebComponenets.org|Introduction|4/21/17|[x]|[x]|[x]||
