# LCCSS

バージョン 1.0.0 / 最終更新: 2017/05/17

## 命名規則

- 原則として `Layout` または `Component` に属さなければならない
- `Component` 内に属するコンポーネント要素（ボタン等）は、例えデザインが共通であってもコンポーネント内の要素としてクラスを指定する

クラスの命名規則は下記の通りとする

#### Layout

接頭辞に `l-` を付与

```html
<div class="l-inner"> ... </div>
```

```css
.l-inner { ... }
```

- 外枠や内枠など、枠組みを形成する要素に対して記述

#### Component

接頭辞に `c-` を付与

```html
<header class="c-header"> ... </header>
```

```css
.c-header { ... }
```

- どのページでも共通して流用できるような要素群に対して記述

#### ステート

接頭辞に `is-` を付与

```html
<div class="is-active"> ... </div>
```

```css
.is-active { ... }
```

- 要素の状態を変更する場合に記述
- 基本的に単体で使用せず、他のクラスと合わせての使用を推奨

#### JavaScript制御

接頭辞に `js-` を付与

```html
<div id="js-modal"> ... </div>
<div class="js-modalCloseButton"> ... </div>
```

- JavaScriptによる操作対象の要素にのみ記述
- このクラスに対してスタイルの適用は禁止とする
- 基本的に単体で使用せず、他のクラスと合わせての使用を推奨

---

## 設計思想

SMACSS + MindBEMding

#### 要素のネスト

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
- CSSは詳細度をフラットにするためにネストしない

#### Modifier

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

---

## サンプル

```html
<header class="c-header">
  <h1 class="c-header_title">Website</h1>
  <p class="c-header_read">Sint est sunt cillum Lorem irure irure laborum adipisicing officia consectetur elit aliquip.</p>
</header>

<main class="l-content">
  <div class="l-inner">

    <section class="l-entry">
      <article class="c-card _entry _1">
        <h2 class="c-card_title">Entry title</h2>
        <p class="c-card_read">Sint est sunt cillum Lorem irure irure laborum adipisicing officia consectetur elit aliquip.</p>
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
        <p class="c-card_read">Sint est sunt cillum Lorem irure irure laborum adipisicing officia consectetur elit aliquip.</p>
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

```css
/* Layout */
.l-inner { ... }
.l-content { ... }
.l-entry { ... }
.l-archive { ... }

/* Component: header */
.c-header { ... }
.c-header_title { ... }
.c-header_read { ... }

/* Component: footer */
.c-footer { ... }
.c-footer_copyright { ... }

/* Component: card */
.c-card { ... }
.c-card._1 { ... }
.c-card._2 { ... }
.c-card._3 { ... }
.c-card_title { ... }
.c-card_read { ... }
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


