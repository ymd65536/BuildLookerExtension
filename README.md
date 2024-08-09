# Looker 拡張機能のビルド

## はじめに

この記事ではLookerのアプリケーション拡張利用するため、React/JavaScript拡張機能のビルド方法について説明します。

## Looker 拡張機能のビルドの始め方

おおまかな手順は以下の通りです。

- マニュフェストファイルの作成
- プロジェクトにマニュフェストファイルを追加
- 実行環境の構築
- 拡張機能のビルド
- 拡張機能の実行

なお、今回はデプロイは行いません。

## マニュフェストファイルの作成

まずは拡張機能をLookerに登録するためのマニュフェストファイルを作成します。
以下のように定義して`manifest.lkml`というファイルを作成します。

```
project_name: "helloworld"
application: helloworld {
    label: "helloworld React/JavaScript extension"
    url: "https://localhost:8080/bundle.js"
    entitlements: {
        core_api_methods: ["me"]
    }
}
```

## プロジェクトにマニュフェストファイルを追加

拡張機能はLookerのプロジェクトに追加する必要がありますが、今回は検証環境でやっていることもあるため
既存のプロジェクトにマニュフェストファイルを追加します。

## 環境構築

## 拡張機能のビルド

```sh
yarn install
```

```sh
yarn build
```

## 拡張機能の実行

```sh
yarn develop
```

[https://localhost:8080](https://localhost:8080)にアクセスします。

## デプロイ

To allow other people to use the extension, build the JavaScript bundle file and directly include it in the project.

1. Build the extension with `yarn build` in the extension project directory on your development machine.
2. Drag and drop the generated `dist/bundle.js` file into the Looker project interface
3. Modify your `manifest.lkml` to use `file` instead of `url`:

```
project_name: "helloworld"
application: helloworld {
    label: "A Looker React/JavaScript extension"
    file: "bundle.js"
    entitlements: {
        core_api_methods: ["me"]
    }
}
```

## 参考

- [Looker 拡張機能の概要](https://cloud.google.com/looker/docs/extension-overview?hl=ja)
- [Looker データ ディクショナリの使用](https://cloud.google.com/looker/docs/using-looker-data-dictionary?hl=ja)
- [Looker 拡張機能のビルド](https://cloud.google.com/looker/docs/extension-intro-to-building?hl=ja)
- [app-data-dictionary](https://github.com/looker-open-source/app-data-dictionary/tree/master)
- [Looker UI Components](https://looker-open-source.github.io/components/latest/?path=/docs/home--docs)
