# よく使いそうなLinterの設定とPrettierの設定まとめ

## Stylelint

### scss含んだcssの書き方を怒ってくれるやつ

```sh
npm install -D stylelint-config-standard-scss
```

### cssの設定項目の順番に秩序を与えてくれるやつ

```sh
npm install -D stylelint-config-recess-order
```

### Vueファイルの中のstyleも見てくれるやつ

厳密にいうとtemplateタグやscriptタグで変に解析せず、styleタグの中を解析してくれるようになる。

```sh
npm install -D stylelint-config-recommended-vue
```

これにいたってはもしかすると↓これも必要かも

```sh
npm install -D postcss-html
```

## ESLint

Nuxt3でTypeScriptで開発する場合はそのまま使っていただいて

### 一部上書きしているルール

```json
"rules": {
    "comma-dangle": [
      "error",
      {
        "arrays": "always-multiline",
        "objects": "always-multiline",
        "imports": "never",
        "exports": "never",
        "functions": "never"
      }
    ],
    "vue/html-self-closing": "off"
  },
```

`"comma-dangle"`は、いわゆる末尾カンマ。

配列とオブジェクトに関しては複数行のときだけ末尾カンマ必須にしている。
これは、gitの差分が見やすくなるため。

`"vue/html-self-closing": "off"`これは閉じタグなし系の要素で怒られるのを回避するためのもの

この設定がないと`<img />`とか怒られます。

## Prettier
基本的には上のESLintの設定と噛み合うように設定しています。

## .vscode/ これなにげに一番大事かも
extensions.jsonにある拡張機能で、StylelintとESLintとPrettierはまず必須。

settings.jsonのセーブ時フォーマットの部分の設定があることで上の設定がすべて生きてくる。

本当はgitのpre-commitのフックで解析フォーマットする設定も入れるとなお良いんだけど、保存時フォーマットでも十分チームでのコーディング規約を固めれると思う。