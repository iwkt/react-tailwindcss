---
noteId: "709e1100f4e811ecb2df4bf22cdc5683"
tags: []

---

# TailCSS を利用してスタイルを当てる

今勢いのあるという TailCSS を使って使用感を確認した。
以下に作成した手順を示す。

## ３つのパッケージをインストール

```
npm install -D tailwindcss postcss-cli autoprefixer
```

## npx tailwindcss init -p で設定ファイルを作成

これで、tailwind.config.js と postcss.config.js ファイルが作られる。

```
npm tailwindcss init -p

```

## styles.css ファイルを作成

styles.css ファイルを作成して下記をペースト。
VSCode で書くと波下線がでて注意を促してくる。
これを回避するには VSCode 機能拡張[PostCSS Language]をインストールする

```
@tailwind base;
@tailwind components;
@tailwind utilities;

```

## index.html ファイルを作成

スタイルのリファレンス先を指定する。ここでは dist.css とした。
上記の styled.css がビルドされたものが dist.css に書き出される。

## dist.css ファイルを作成

root 直下に dist.css を作成。ここにビルドした後のコードが書き込まれる。
distribution の略。配布物の意味。

```
<link href="/dist.css" rel="stylesheet">

```

## Tailwind のクラスを当てる。

index.html に以下を記述

```
<h1 class="text-6xl text-cyan-600 p-10 bg-gray-200">Hello World</h1>

```

この時 VSCode 用の機能拡張『Tailwind CSS IntelliSense』をインストールしておくと便利。補完機能により候補や色などを表示してくれる。

## ビルドコマンドの作成

package.json にビルドコマンドを書きます。

postcss を使って styles.css から dist.css へ output （-o）するです。

```
/* package.json */
"scripts": {
    "build": "postcss styles.css -o dist.css"
  },

```

## tailwind.config に追記

content: []　の部分に path を追記

```
/* tailwind.config */
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ["./index.html"],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

# 使用方法

##コマンドの実行

```
npm run build
```
