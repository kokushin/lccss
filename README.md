# LCCSS

Layout or Component base CSS coding rule

## 概要

LCCSS（ルックス）は、各要素のカテゴライズを「レイアウト」と「コンポーネント」の2軸に絞ることでシンプルな構造にし、従来のCSS設計における思考時間を少しでも減らすことを目標としている。

- 各要素は `Layout` または `Component` のどちらかに属する。細かくカテゴライズしない
- `Layout` は「枠組み」となる要素に対して定義
- `Component` は「Layout内に含まれている、または単体で機能する」要素群に対して定義
- 接頭辞によって各要素の役割を明確に
- MindBEMdingを少し改変したものを採用することで、冗長な書き方を解決・命名に思考する時間の短縮に期待できる

## カテゴライズ

必須項目は `Layout` と `Component` の2つで、その他は状況に応じて使い分けることができる。

| 種類       | 接頭辞 | 補足                                                               |
|------------|--------|--------------------------------------------------------------------|
| Layout     |   l-   | 外枠や内枠など、枠組みを形成する要素に対して記述                   |
| Component  |   c-   | レイアウト内に含まれている、または単体で機能する要素群に対して記述 |
| State      |   is-  | 要素の状態を変更する場合に記述                                     |
| JavaScript |   js-  | JavaScriptによる操作対象の要素にのみ記述                           |
| Utility    |   u-   | 要素に対して固有のスタイルを適用させたいときに記述                 |
| Theme      |   t-   | ページごとにテーマとしてスタイルを適用させたいときに記述           |

### Layout

接頭辞に `l-` を付与

```html
<div class="l-inner"> ... </div>
```

```css
.l-inner { ... }
```

- 外枠や内枠など、枠組みを形成する要素に対して記述
- 横幅などベースとなるスタイルは、この要素に対して指定することを推奨

### Component

接頭辞に `c-` を付与

```html
<header class="c-header"> ... </header>
```

```css
.c-header { ... }
```

- Layout内に含まれている、または単体で機能する要素群に対して記述
- 共通で使いまわすことを想定して設計することを推奨
- `Component` 内に属するコンポーネント要素（ボタン等）は、たとえデザインが共通であってもコンポーネント内の要素として新規で命名しなければならない

### State

接頭辞に `is-` を付与

```html
<div class="is-active"> ... </div>
```

```css
.is-active { ... }
```

- 要素の状態を変更する場合に記述
- 基本的に単体で使用せず、他のクラスと合わせての使用を推奨

### JavaScript

接頭辞に `js-` を付与

```html
<div id="js-modal"> ... </div>
<div class="js-modalCloseButton"> ... </div>
```

- JavaScriptによる操作対象の要素にのみ記述
- このクラスに対してスタイルの適用は禁止とする
- 基本的に単体で使用せず、他のクラスと合わせての使用を推奨

### Utility

接頭辞に `u-` を付与

```html
<p class="u-textCenter">Qui ad culpa aute ad nulla officia sit aliquip excepteur.</p>
```

```css
.u-textCenter { text-align: center }
```

- 部分的な要素に対して固有のスタイルを適用させたいときに記述
- 共通して使いまわすことを前提にした設計にする

### Theme

接頭辞に `t-` を付与

```html
<body class="t-dark"> ... </body>
```

```css
.t-dark { background-color: #929292; }
```

- ページごとにテーマとしてスタイルを適用させたいときに記述
- `Utility` と `Theme` の使い分けとしては、前者は部分的にスタイルを適用させたいときに記述、後者は全体的にスタイルを適用させたい場合に記述する

## 設計思想

### 影響を受けたもの

> SMACSS、Enduring CSS（ECSS）、MindBEMding（BEM）

CSSカテゴライズはSMACSSを参考にしているが、LCCSSでは「ベース/エリアとなる枠組み（SMACSSではベース・レイアウトに該当）」をまとめて `Layout` として定義し、「レイアウト内に含まれている、または単体で機能する要素群（SMACSSではモジュールに該当）」を `Component` として定義する。また `Component` は、共通で使いまわすことも想定して設計することを推奨する。

コンポーネント内のパーツ（ボタン等）は、色・フォントサイズなど僅かなデザインが共通であっても新規でスタイルを適用する。コンポーネントは単体で機能すべきであり、余計なクラスを増やさなくても済む。

命名規則はMindBEMdingを参考にしているが、一部改変しており簡潔に記述することが可能。スタイルの打ち消しは状況に応じて可能だが、基本的に打ち消さない方が良い。また、セレクタのネストは極力行わず詳細度を一定に保つことを推奨する。（ただし、Stateを親要素に指定し、一括でスタイル操作する必要がある場合はネスト可能とする）

### 要素のネスト

```html
<div class="block">
  <div class="block_element">
    <div class="block_element_element"></div>
  </div>
</div>
```

```css
.block { ... }
.block_element { ... }
.block_element_element { ... }
```

- 要素は `_` で繋ぐ
- 階層は制限しない（余計な思考時間を省く）
- 単語の綴りにはキャメルケースを推奨（接頭辞に `-` 、要素のネスト・Modifierに `_` を使っているため。しかし状況に応じて変更してもよい）
- 詳細度を一定に保つためセレクタのネストは非推奨

> NG

```css
.parent { ... }
.parent .child { ... }
.is-active .parent .child { ... }
```

> OK

```css
.parent { ... }
.child { ... }
.is-active .child { ... }
```

### Modifier

```html
<div class="block _modifier">
  <div class="block_element _modifier">
    <div class="block_element_element _modifier"></div>
  </div>
</div>
```

```css
.block._modifier { ... }
.block_element._modifier { ... }
.block_element_element._modifier { ... }
```

- Modifierは先頭に `_` を記述
- 基本的に単体で使用せず、他のクラスと合わせての使用を推奨

## サンプル

CSSに関してはプリプロセッサーを利用した開発を前提としており、`@mixin` や `@extend` を利用し簡潔にコードを管理することを推奨する。

### HTML

```html
<header class="c-header">
  <h1 class="c-header_title">Website</h1>
  <p class="c-header_lead">Sint est sunt cillum Lorem irure irure laborum adipisicing officia consectetur elit aliquip.</p>
</header>

<main class="l-content">
  <div class="l-inner">

    <section class="l-entry">
      <article class="c-card _entry _1">
        <h2 class="c-card_title">Entry title</h2>
        <p class="c-card_lead">Sint est sunt cillum Lorem irure irure laborum adipisicing officia consectetur elit aliquip.</p>
        <div class="c-card_button"><a href="#">Button</a></div>
        <ul class="c-card_category">
          <li class="c-card_category_item _1"><a href="#">Sint est sunt cillum 1</a></li>
          <li class="c-card_category_item _2"><a href="#">Sint est sunt cillum 2</a></li>
          <li class="c-card_category_item _3"><a href="#">Sint est sunt cillum 3</a></li>
        </ul>
      </article>
    </section>

    <section class="l-archive">
      <article class="c-card _archive _1">
        <h2 class="c-card_title">Entry title</h2>
        <p class="c-card_lead">Sint est sunt cillum Lorem irure irure laborum adipisicing officia consectetur elit aliquip.</p>
        <div class="c-card_button"><a href="#">Button</a></div>
        <ul class="c-card_category">
          <li class="c-card_category_item _1"><a href="#">Sint est sunt cillum 1</a></li>
          <li class="c-card_category_item _2"><a href="#">Sint est sunt cillum 2</a></li>
          <li class="c-card_category_item _3"><a href="#">Sint est sunt cillum 3</a></li>
        </ul>
      </article>
    </section>

  </div>
</main>

<footer class="c-footer">
  <small class="c-footer_copyright">&copy; 2017 Website</small>
</footer>
```

### CSS

```css
/* Layout */
.l-inner { ... }
.l-content { ... }
.l-entry { ... }
.l-archive { ... }

/* Component: header */
.c-header { ... }
.c-header_title { ... }
.c-header_lead { ... }

/* Component: footer */
.c-footer { ... }
.c-footer_copyright { ... }

/* Component: card */
.c-card { ... }
.c-card._1 { ... }
.c-card._2 { ... }
.c-card._3 { ... }
.c-card_title { ... }
.c-card_lead { ... }
.c-card_button { ... }
.c-card_category { ... }
.c-card_category_item { ... }
.c-card_category_item._1 { ... }
.c-card_category_item._2 { ... }
.c-card_category_item._3 { ... }

/* Component: card - entry */
.c-card._entry { ... }
.c-card._entry._1 { ... }
.c-card._entry._2 { ... }
.c-card._entry._3 { ... }

/* Component: card - archive */
.c-card._archive { ... }
.c-card._archive._1 { ... }
.c-card._archive._2 { ... }
.c-card._archive._3 { ... }
```

LCCSSを適用したデモは [こちら](https://kokushin.github.io/lccss/)

## 更新履歴

Version 1.2.1 / Updated date: 2017/05/24

- [1.2.0] セレクタのネストは不可能→非推奨とする
- [1.1.0] Themeを追加

## ライセンス表記

MIT License

Copyright (c) 2017 kokushin
