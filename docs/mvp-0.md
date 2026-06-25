# deckfolio.vue MVP-0

## Purpose

MVP-0 の目的は、deckfolio.vue の中核コンセプトである **「発表時は薄く、発表後は厚く」** を、最小の実装で検証することである。

deckfolio.vue は、発表用スライドと公開用詳細資料を分離せず、1つの Vue SFC として同時に作成するためのツールである。

MVP-0 では、1つの Vue SFC から以下を生成できることを到達点とする。

* 発表当日に使う PDF
* 発表後に公開する HTML

## Goal

MVP-0 のゴールは次の通り。

```txt
talks/example.vue
↓
deckfolio build talks/example.vue
↓
dist/example/deck.pdf
dist/example/index.html
```

この流れにより、以下を確認する。

1. Vue SFC を発表資料の入力形式として使える
2. `<template>` を発表用スライドとして扱える
3. custom block を公開用本文として扱える
4. 同一 SFC から PDF と HTML を生成できる
5. 発表用資料と公開用資料を別ファイルとして二重管理しなくてよい

## Non-Goals

MVP-0 では、以下は扱わない。

* テーマ機構
* プラグイン機構
* 複数発表資料の一括管理
* 公開サイト全体の生成
* ルーティング
* OGP 生成
* speaker note 機能
* 高度な PDF レイアウト制御
* Markdown ファイルの外部読み込み
* 独自コンポーネント配布
* create コマンド
* init コマンド
* watch / dev server
* deploy 機能

MVP-0 は、完成した発表資料作成環境ではなく、deckfolio.vue の成立可能性を確認するための最小プロトタイプである。

## Input

MVP-0 の入力は、単一の Vue SFC とする。

例:

```txt
talks/example.vue
```

SFC は以下の構造を持つ。

```vue
<template>
  <Deck>
    <Slide>
      <h1>deckfolio.vue</h1>
      <p>発表時は薄く、発表後は厚く。</p>
    </Slide>

    <Slide>
      <h2>なぜ必要か</h2>
      <p>スライドと公開資料を分離しない。</p>
    </Slide>
  </Deck>
</template>

<article lang="md">
# deckfolio.vue

deckfolio.vue は、発表用スライドと公開用詳細資料を同じ Vue SFC として記述するためのツールである。

## なぜ必要か

発表用スライドは、発表の場では薄い方がよい。
しかし、発表後に公開される資料まで薄いと、あとから資料を読む人に十分な情報が届かない。

deckfolio.vue は、発表用の薄いスライドと、公開用の厚い本文を、同じ SFC の中で同時に作成する。
</article>
```

## SFC Format

### `<template>`

`<template>` は発表用スライドを表す。

MVP-0 では、`<Deck>` と `<Slide>` を最小の構成要素とする。

```vue
<template>
  <Deck>
    <Slide>
      <h1>Title</h1>
    </Slide>
  </Deck>
</template>
```

MVP-0 では、`<Slide>` の内部は通常の Vue template として扱う。

ただし、複雑な状態管理、外部データ取得、非同期処理は MVP-0 の対象外とする。

### `<article lang="md">`

`<article lang="md">` は、発表後に公開する詳細本文を表す。

`article` という名前を使う理由は、この領域が単なる登壇者用メモではなく、公開用の第一級コンテンツだからである。

MVP-0 では、`<article lang="md">` の中身を Markdown として HTML に変換する。

```vue
<article lang="md">
# Title

Detailed article body.
</article>
```

## Output

MVP-0 の出力先は `dist/` とする。

```txt
dist/
  example/
    deck.html
    deck.pdf
    index.html
```

### `deck.html`

`deck.html` は、発表用スライドを HTML として表示するためのファイルである。

主に PDF 生成の中間成果物として使う。

### `deck.pdf`

`deck.pdf` は、発表当日に使う PDF である。

MVP-0 では、`deck.html` をブラウザでレンダリングし、PDF として出力する。

### `index.html`

`index.html` は、発表後に公開する HTML である。

MVP-0 では、`<article lang="md">` の内容を Markdown から HTML に変換し、単一ページとして出力する。

## CLI

MVP-0 で提供する CLI は `build` のみとする。

```bash
deckfolio build talks/example.vue
```

入力ファイル名から出力ディレクトリ名を決定する。

```txt
talks/example.vue
→ dist/example/
```

MVP-0 では、設定ファイルは必須にしない。

## Directory Structure

MVP-0 で想定する最小ディレクトリ構成は次の通り。

```txt
my-deckfolio/
  package.json
  talks/
    example.vue
  public/
  dist/
```

### `talks/`

発表資料の SFC を置く。

### `public/`

画像などの静的アセットを置く。

MVP-0 では、最低限の静的ファイル参照のみを扱う。

### `dist/`

生成物を出力する。

`dist/` は Git 管理対象外とする。

## Requirements

### R1. SFC を読み込める

指定された Vue SFC を読み込み、`<template>` と custom block を取得できる。

### R2. `<template>` から発表用 HTML を生成できる

`<template>` の内容から `deck.html` を生成できる。

### R3. `<article lang="md">` から公開用 HTML を生成できる

`<article lang="md">` の内容を Markdown として変換し、`index.html` を生成できる。

### R4. 発表用 PDF を生成できる

`deck.html` をもとに `deck.pdf` を生成できる。

### R5. 単一コマンドで生成できる

次のコマンドで、`deck.html`、`deck.pdf`、`index.html` が生成される。

```bash
deckfolio build talks/example.vue
```

## Acceptance Criteria

MVP-0 は、次の条件を満たしたら完了とする。

1. `talks/example.vue` を用意できる
2. `deckfolio build talks/example.vue` を実行できる
3. `dist/example/deck.html` が生成される
4. `dist/example/deck.pdf` が生成される
5. `dist/example/index.html` が生成される
6. `deck.pdf` を開くと、`<template>` に書いたスライドが表示される
7. `index.html` を開くと、`<article lang="md">` に書いた本文が表示される
8. スライドと本文が同じ SFC から生成されていることを確認できる

## Implementation Scope

MVP-0 の実装範囲は次の通り。

1. CLI entrypoint を作る
2. `build` コマンドを作る
3. Vue SFC を parse する
4. `<template>` を取り出す
5. `<article lang="md">` を取り出す
6. スライド用 HTML を生成する
7. Markdown を HTML に変換する
8. 公開用 HTML を生成する
9. ブラウザレンダリングにより PDF を生成する
10. `dist/` に成果物を書き出す

## Error Handling

MVP-0 では、最低限以下のエラーを扱う。

### Input file not found

指定された SFC が存在しない場合、エラーとして終了する。

### Missing `<template>`

`<template>` が存在しない場合、エラーとして終了する。

### Missing `<article lang="md">`

`<article lang="md">` が存在しない場合、エラーとして終了する。

### Build failed

HTML 生成または PDF 生成に失敗した場合、エラーとして終了する。

MVP-0 では、詳細なエラー分類や診断メッセージの整備は対象外とする。

ただし、どの段階で失敗したかは最低限わかるようにする。

## Design Notes

### Why Vue SFC?

deckfolio.vue は、発表資料を単なる Markdown や静的 HTML ではなく、Vue SFC として扱う。

これにより、発表資料をコンポーネントとして構造化できる。

また、スライドと公開用本文を同じファイルに置きながら、用途ごとに異なる出力を生成できる。

### Why custom block?

Vue SFC の custom block を使うことで、発表用スライドと公開用本文を同じ SFC 内に共存させられる。

`<template>` は発表用スライド、`<article lang="md">` は公開用本文、という役割分担を明確にできる。

### Why `<article>` instead of `<notes>`?

`notes` は登壇者用メモに見えやすい。

deckfolio.vue における詳細本文は、発表者を補助するためのメモではなく、発表後に公開するためのコンテンツである。

そのため、MVP-0 では `<article lang="md">` を採用する。

## Open Questions

MVP-0 では、以下は未決のままにする。


1. `<article>` 以外の custom block 名を許容するか
2. `deckfolio.config.ts` をいつ導入するか
3. `create deckfolio` をいつ提供するか
4. 複数発表資料をどのように管理するか
5. テーマ機構をどの粒度で提供するか
6. 公開用 HTML のデザインをどこまで標準化するか
7. PDF レイアウトの制御をどこまで許容するか
8. 開発用 preview server をいつ導入するか

## Summary

MVP-0 は、deckfolio.vue の完成形を作る段階ではない。

MVP-0 の目的は、次の仮説を最小実装で検証することである。

> 1つの Vue SFC から、発表用の薄い PDF と、公開用の厚い HTML を生成できれば、発表資料と公開資料の二重管理を避けられる。

この仮説が通ることを確認できれば、次の段階でディレクトリ構成、設定ファイル、テーマ、開発サーバー、複数資料管理を設計する。
