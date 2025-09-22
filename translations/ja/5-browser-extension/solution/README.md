<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "fab4e6b4f0efcd587a9029d82991f597",
  "translation_date": "2025-08-23T23:48:47+00:00",
  "source_file": "5-browser-extension/solution/README.md",
  "language_code": "ja"
}
-->
# カーボントリガー ブラウザー拡張機能: 完成コード

tmrowのC02 Signal APIを使用して電力使用量を追跡し、地域の電力使用状況がどれだけ負荷がかかっているかをブラウザーで通知する拡張機能を作成します。この拡張機能を使うことで、得られた情報に基づいて活動を判断する助けになります。

![拡張機能のスクリーンショット](../../../../5-browser-extension/extension-screenshot.png)

## はじめに

[npm](https://npmjs.com) をインストールする必要があります。このコードをコンピューターのフォルダーにダウンロードしてください。

必要なパッケージをすべてインストールします:

```
npm install
```

webpackを使って拡張機能をビルドします:

```
npm run build
```

Edgeにインストールするには、ブラウザー右上の「三点メニュー」から拡張機能パネルを開きます。そこから「パッケージされていない拡張機能を読み込む」を選択し、新しい拡張機能を読み込みます。プロンプトで「dist」フォルダーを開くと、拡張機能が読み込まれます。使用するには、CO2 SignalのAPIキーが必要です（[こちらからメールで取得](https://www.co2signal.com/) - ページのボックスにメールアドレスを入力してください）と、[Electricity Map](https://www.electricitymap.org/map) に対応する地域コード（例: ボストンの場合は「US-NEISO」を使用）を取得してください ([地域コードはこちら](http://api.electricitymap.org/v3/zones))。

![インストール手順](../../../../5-browser-extension/install-on-edge.png)

拡張機能のインターフェースにAPIキーと地域コードを入力すると、ブラウザー拡張機能バーのカラードットが地域のエネルギー使用状況を反映するように変わります。また、エネルギー消費の多い活動を行うべきかどうかの指針を示してくれます。この「ドット」システムのコンセプトは、カリフォルニアの排出量を対象とした [Energy Lollipop拡張機能](https://energylollipop.com/) から着想を得ています。

**免責事項**:  
この文書は、AI翻訳サービス [Co-op Translator](https://github.com/Azure/co-op-translator) を使用して翻訳されています。正確性を追求しておりますが、自動翻訳には誤りや不正確な部分が含まれる可能性があることをご承知ください。元の言語で記載された文書が正式な情報源とみなされるべきです。重要な情報については、専門の人間による翻訳を推奨します。この翻訳の使用に起因する誤解や誤解釈について、当方は一切の責任を負いません。