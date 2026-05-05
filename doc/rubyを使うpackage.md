GoogleのAIモードでlualatexでルビをつけるパッケージについて聞いてみました。

------------------------------
## LuaLaTeXにおけるルビパッケージの選択：luatexja-ruby から pxrubrica へ
## 1. なぜ okumacro の \ruby を使わないのか
LuaLaTeX環境では、伝統的な okumacro（pLaTeX向け）ではなく、LuaTeXに最適化されたパッケージが推奨されます。

* 互換性の問題: okumacro は (u)pLaTeX 特有の命令を利用しており、LuaLaTeXではエラーや組版崩れの原因になります。
* LuaTeX-jaへの最適化: luatexja-ruby や pxrubrica は、LuaTeXの高度な文字制御機能を活用して高品質な日本語組版を実現します。

## 2. luatexja-ruby と pxrubrica の比較

| 特徴 | luatexja-ruby | pxrubrica |
|---|---|---|
| 主な開発思想 | LuaTeX-jaの機能を最大限活用 | 汎用性が高く、(u)pLaTeX/LuaLaTeX両対応 |
| 処理方式 | マルチパス方式（複数回のコンパイル） | シングルパス方式（1回のコンパイル） |
| 中間ファイル | .ltjruby ファイルが生成される | 生成されない（フォルダが綺麗） |
| 制御方法 | 高度な自動計算が中心 | オプションによる直感的な手動制御 |

## 3. pxrubrica の導入と設定
### 導入
luatexja-ruby との競合を避けるため、使用する際は pxrubrica のみを読み込みます。

\usepackage{pxrubrica}

### 基本的な使い方

\ruby[オプション]{親文字}{ルビ}


* [g]: グループルビ（全体に配置）
* [m]: モノルビ（一字ずつ配置）
* [j]: 熟語ルビ（バランス調整あり）
* [|]: ルビの突出禁止

### 全体設定 (\rubysetup)
文書全体のスタイルを統一したい場合にプリアンブル等に記述します。

* \rubysetup{g}: グループルビ（おすすめ）
* \rubysetup{J}: 自動判別・熟語ルビモード（おすすめ）
* \rubysetup{c}: 中付き（デフォルト）
* \rubysetup{h}: 肩付き

## 4. 結論
LuaLaTeXにおいて、余計な補助ファイル（.ltjruby）を作らず、かつ柔軟にルビを制御したい場合は pxrubrica を選択するのが非常に合理的です。
------------------------------

## 後日補足
okumacroからの乗り換えでは，

\usepackage{pxrubrica}

\rubysetup{g}

の2行を指定しておくのが，ルビの扱いも同様で，エラーも少ない。
(2026/5/5)