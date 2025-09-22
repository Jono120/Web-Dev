<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "3f5e6821e0febccfc5d05e7c944d9e3d",
  "translation_date": "2025-08-23T23:54:07+00:00",
  "source_file": "5-browser-extension/solution/translation/README.ja.md",
  "language_code": "ja"
}
-->
# カーボントリガーブラウザ拡張機能：完成したコード

tmrow の CO2 シグナル API を使用して、地域の電力使用量を追跡し、ブラウザ上でリマインダーとして表示する拡張機能を構築します。この拡張機能を使うことで、電力使用量に基づいて日々の活動を調整することができます。

![extension screenshot](../../../../../5-browser-extension/extension-screenshot.png)

## はじめに

[npm](https://npmjs.com) がインストールされている必要があります。このコードをコンピュータ上のフォルダにダウンロードしてください。

必要なパッケージをすべてインストールします。

```
npm install
```

webpack を使用して拡張機能をビルドします。

```
npm run build
```

Edge にインストールするには、ブラウザの右上にある「3つのドット」メニューから「拡張機能」パネルを開きます。そこから「Load Unpacked」を選択し、新しい拡張機能をロードします。プロンプトが表示されたら「dist」フォルダを選択してください。これで拡張機能が読み込まれます。使用するには、CO2 シグナル API の API キー ([こちらでメールを通じて取得](https://www.co2signal.com/) - ページのボックスにメールアドレスを入力してください) と、[Electricity Map](https://www.electricitymap.org/map) に対応する [地域コード](http://api.electricitymap.org/v3/zones) が必要です（例えば、ボストンでは 'US-NEISO' を使用します）。

![installing](../../../../../5-browser-extension/install-on-edge.png)

API キーと地域コードを拡張機能のインターフェイスに入力すると、ブラウザの拡張バーに表示される色付きのドットが、地域のエネルギー使用量を反映して変化します。このドットは、どのようなエネルギーを必要とする活動を行うのが適切かを示してくれます。この「ドット」システムのアイデアは、カリフォルニア州の排出量を可視化する [Energy Lollipop extension](https://energylollipop.com/) にインスパイアされたものです。

**免責事項**:  
この文書は、AI翻訳サービス [Co-op Translator](https://github.com/Azure/co-op-translator) を使用して翻訳されています。正確性を追求しておりますが、自動翻訳には誤りや不正確な部分が含まれる可能性があることをご承知ください。元の言語で記載された文書が正式な情報源とみなされるべきです。重要な情報については、専門の人間による翻訳を推奨します。この翻訳の使用に起因する誤解や誤解釈について、当社は責任を負いません。