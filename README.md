# 目的
ESLint、StyleLintとWebpack5を連携。なお、ESLintはTypeScript、StyleLintはSCSSにも対応させる。
# ポイント
## package.json
以下のパッケージをそれぞれインストールする。
#### ESLint
インストール後は `npx eslint --init` で `.eslintrc.json` ファイルを作成する。
```
{
  "eslint": "7.32.0",
  "eslint-webpack-plugin": "^3.1.1",
}
```
#### StyleLint
StyleLintを拡張するパッケージも一緒にインストール(任意)
- stylelint-config-standard-scss<br/>
一般的なSCSSのコーディング規約集
- stylelint-order<br/>
CSSプロパティをABC順に並べる
```
{
  "stylelint": "^14.1.0",
  "stylelint-config-standard-scss": "^2.0.1",
  "stylelint-order": "^3.1.1",
  "stylelint-scss": "^4.0.0",
  "stylelint-webpack-plugin": "^3.1.0",
  ...
}
```
`.stylelintrc.json` ファイルは新規作成して追加する。
```
{
  "plugins": [
    "stylelint-scss",
    "stylelint-order"
  ],
  "extends": [
    "stylelint-config-standard-scss"
  ],
  "rules": {
    "order/properties-alphabetical-order": true,
    "indentation": 2
  }
}
```

## webpack.config.js
ESLint、StyleLintのプラグインを設定する。<br/>
`fix: true` でファイル保存時に自動整形する(任意)。
```
const ESLintPlugin = require('eslint-webpack-plugin')
const StylelintPlugin = require('stylelint-webpack-plugin')
...
plugins: [
  new ESLintPlugin({
    fix: true,
    extensions: ['ts', 'tsx', 'js', 'jsx']
  }),
  new StylelintPlugin({
    fix: true
  }),
]
