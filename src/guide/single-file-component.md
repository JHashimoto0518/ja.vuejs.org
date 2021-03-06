# 単一ファイルコンポーネント

## 前書き

多くの Vue プロジェクトでは、 グローバルコンポーネントは  `app.mount('#app')` の後に各ページの body においてコンテナ要素のターゲットすることに続いて、`app.component()` を使用して定義されています。

これはある view を拡張するためだけに JavaScript が利用された中小規模のプロジェクトにおいてはとても有効です。しかしながら、あなたのフロントエンドで JavaScript 全体を操作するようなもっと複雑なプロジェクトでは、これらの点において不利益になります。:

- **グローバル宣言**は全てのコンポーネントに一意な名前を強制すること
- シンタックスハイライトがない**文字列テンプレート**と複数行 HTML の時の醜いスラッシュが強要されること
- **CSS サポート無し**だと HTML と JavaScript がコンポーネントにモジュール化されている間、これ見よがしに無視されること
- **ビルド処理がない**と Pug(前 Jade)と Babel のようなプリプロセッサよりむしろ、 HTML や ES5 JavaScript を制限されること

これらは全ては Webpack や Browserify のビルドツールにより実現された `.vue`拡張子の**単一ファイルコンポーネント**によって解決されます。

こちらが `Hello.vue` と呼ばれたファイルの例です:

<a href="https://codepen.io/team/Vue/pen/3de13b5cd0133df4ecf307b6cf2c5f94" target="_blank" rel="noopener noreferrer"><img src="/images/sfc.png" width="403" alt="Single-file component example (click for code as text)" style="display: block; margin: 15px auto; max-width: 100%"></a>

さて次にこちらに入ります:

- [完全版シンタックスハイライト](https://github.com/vuejs/awesome-vue#source-code-editing)
- [CommonJS モジュール](https://webpack.js.org/concepts/modules/#what-is-a-webpack-module)
- [コンポーネントスコープ CSS](https://vue-loader.vuejs.org/en/features/scoped-css.html)

約束した通り、Pug、Babel (ES2015 モジュールと一緒に) や Stylus など 綺麗で機能が豊富なコンポーネントもプリプロセッサとして利用することができます。

<a href="https://codesandbox.io/s/vue-single-file-component-with-pre-processors-mr3ik?file=/src/App.vue" target="_blank" rel="noopener noreferrer"><img src="/images/sfc-with-preprocessors.png" width="563" alt="Single-file component with pre-processors example (click for code as text)" style="display: block; margin: 15px auto; max-width: 100%"></a>

これらの特定の言語は単なる一例です。TypeScript、SCSS、PostCSS などの生産的なプリプロセッサも簡単に使うことができます。もし `vue-loader` で Webpack を使用しているならば、CSS Modules 向けに素晴らしいサポートがあります。

### 関心の分離について

注意すべき重要な点の１つは、**関心の分離がファイルタイプの分離とは等しくないことです。** 現代の UI 開発では、私たちはコードベースを互いに織りなす3つの巨大なレイヤーに分割するのではなく、それらを疎結合なコンポーネントに分割して構成する方がはるかに理にかなっていることを発見しました。コンポーネントの内部では、そのテンプレート、ロジック、スタイルが本質的に結合しており、実際にそれらを配置することでコンポーネントの一貫性と保守性が高くなります。

単一ファイルコンポーネントのアイディアが好きではなくても、JavaScript と CSS を別々ファイルに分けることによってホットリロードとプリコンパイル機能を活用することができます:

``` html
<!-- my-component.vue -->
<template>
  <div>This will be pre-compiled</div>
</template>
<script src="./my-component.js"></script>
<style src="./my-component.css"></style>
```

## はじめる

### サンドボックスの例

すぐに触ってそして単一ファイルコンポーネントを試したい方は、CodeSandBox 上の [この単純な todo アプリケーション](https://codesandbox.io/s/vue-todo-list-app-with-single-file-component-vzkl3?file=/src/App.vue)
をチェックしてみてください。

### JavaScript でモジュールビルドシステムが初めてなユーザ向け

`.vue` コンポーネントにより、高度な JavaScript アプリケーションの分野へ入っていきます。 これはあなたがまだ使ったことのない、いくつかの追加のツールの使い方を学ぶことを意味します:

- **Node Package Manager (NPM)**: レジストリからパッケージを取得する方法については[Getting Started guide](https://docs.npmjs.com/packages-and-modules/getting-packages-from-the-registry) のセクションを読んでください。

- **ES2015/16 を使ったモダンな JavaScript**: Babel の [Learn ES2015 guide](https://babeljs.io/docs/en/learn)を読んでみてください。今すぐには全ての機能を暗記する必要はないですが、参考として戻れるようにしておいてください。

これらのリソースに没頭した後は、[Vue CLI](https://cli.vuejs.org/)を確認することをお勧めします。 指示に従うことであっという間に `.vue` コンポーネントと ES2015、 Webpack、ホットリローティングを備えた Vue プロジェクトを手に入れられるはずです！

### 上級ユーザ向け

CLI はツールの設定の大部分の面倒を見てくれますが、[設定オプション](https://cli.vuejs.org/config/)を通してよりきめ細かいカスタマイズをすることもできます。

あなたが独自のビルドセットアップをゼロから作ることを好む場合、webpack と [vue-loader](https://vue-loader.vuejs.org)を手動で設定する必要があるでしょう。webpack についてもっと学びたいときは、[公式ドキュメント](https://webpack.js.org/configuration/)や [webpack learning academy](https://webpack.academy/p/the-core-concepts)を参照してください。
