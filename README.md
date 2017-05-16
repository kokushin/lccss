# CSSコーディングルール

バージョン 1.0.0 / 最終更新: 2017/05/16

## 命名規則

クラスの命名規則は下記の通りとする

### 設計思想

SMACSS + MindBEMding

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

- 要素間は `_` で繋いでいく
- CSSは原則としてネストしない（詳細度をフラットにするため）

### コンポーネント

接頭辞に `c-` を付与

```html
<header class="c-header"> ... </header>
```

```css
.c-header { ... }
```

---

### ステート

接頭辞に `is-` を付与

```html
<div class="is-active"> ... </div>
```

```css
.is-active { ... }
```

※基本的に単体で使用せず、他のクラスと合わせて使用する
