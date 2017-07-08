# Polymerのグローバル設定

ドキュメントに対してグローバルな設定をするには、Polymerのライブラリをインポートする前に`windows`へ`Polymer`オブジェクトをセットします。

~~~html
<html>
  <head>
  <meta charset="utf-8">
  <script src="components/webcomponentsjs/webcomponents-loader.js"></script>
  <script>
    /* this script must run before Polymer is imported */
    window.Polymer = {
      rootPath: '/your/application/root'
    };
  </script>
  <!-- a component that relies on Polymer -->
  <link rel="import" href="elements/my-app.html">
  </head>
  <body>
  ...
~~~

利用できる設定:

<table>
<thead>
<tr>
  <td>
    設定
  </td>
  <td>
    説明
  </td>
</tr>
</thead>
<tbody>
  <tr>
    <td>
      <code>rootPath</code>
    </td>
    <td>
     テンプレート等で使用されるグローバルな<code>rootPath</code>プロパティが設定されます(アプリケーションルートからの相対的なURLを生成する場合など)。
    </td>
  </tr>
  <tr>
    <td>
      <code>sanitizeDOMValue</code>
    </td>
    <td>
    任意の値をDOMに挿入する前に、その値をサニタイズするために使用されるグローバルなコールバックです。
    仕様は次のとおりです。
          
```js
Polymer = {
  sanitizeDOMValue: function(value, name, type, node) { ... }
}
```

内容:

-   `value` サニタイズする値
-   `name` 属性やプロパティの名前 (例: `href`)
-   `type` 値が挿入されるタイプ: `property` 、 `attribute` もしくは `text`
-   `node` 値が挿入されるノード
    </td>
  </tr>
</tbody>
</table>

ポリフィルにおける固有の設定もいくつかあります。詳細は [Polyfills](../polyfills#settings) を参照してください。
