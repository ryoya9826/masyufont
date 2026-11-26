# masyufont パッケージ

Author: Ryoya Ando — [https://ryoya9826.github.io/](https://ryoya9826.github.io/)  
Version: 0.2 (2026-11-26)  
License: [MIT License](LICENSE)  

`masyufont.sty` は，本文フォントと数式フォントをプリセットの名前で選ぶための LaTeX パッケージです．
1つのプリセットに LuaLaTeX 用と (u)pLaTeX 用の設定をまとめて持つので，同じソースをどちらのエンジンで組版しても，同じフォントの組み合わせになります．

## 主な特徴

1. プリセットの名前で選ぶ:
  - `\masyufont{IPA}` のように名前を書くだけで，和文・欧文のフォントをまとめて切り替えます．
2. エンジンの違いを吸収:
  - LuaLaTeX では `luatexja-fontspec`，(u)pLaTeX では `pxchfon` の命令でフォントを設定します．
3. プリセットの追加:
  - `\masyuMainFontDefine` と `\masyuMathFontDefine` で，自分のプリセットを登録できます．
4. 既定の設定:
  - `\masyufont` を使わなければ，本文・数式とも newtx（Times 系）になります．

## 動作条件

| 項目 | 条件 |
| --- | --- |
| エンジン | LuaLaTeX，pLaTeX，upLaTeX（pdfLaTeX と XeLaTeX ではエラー） |
| 文書クラス | `bxjsarticle` などの BXJS 文書クラス（`ja=standard`）を想定 |
| DVI ウェア | (u)pLaTeX では dvipdfmx を想定 |
| 依存パッケージ | `iftex`，`xkeyval`，`etoolbox`．(u)pLaTeX では `pxchfon` |
| ドキュメントの組版 | LuaLaTeX |

## 使用方法

プリアンブルで `masyufont` パッケージを読み込み，`\masyufont` でプリセットを選びます．

```latex
\documentclass[autodetect-engine,dvi=dvipdfmx,ja=standard]{bxjsarticle}
\usepackage{masyufont}
\masyufont[xits]{IPA} % 本文は IPA フォント，数式は XITS Math（LuaLaTeX のみ）

\begin{document}
本文は IPA 明朝，\textsf{見出しは IPA ゴシック}，数式は $x^2+y^2$．
\end{document}
```

| コマンド | 説明 |
| --- | --- |
| `\masyufont[数式フォント]{本文フォント}` | プリセットを呼び出す．数式フォントを省くと `default` |
| `\masyuMainFontDefine{名前}{LuaLaTeX での設定}{(u)pLaTeX での設定}` | 本文フォントのプリセットを登録する |
| `\masyuMathFontDefine{名前}{LuaLaTeX での設定}{(u)pLaTeX での設定}` | 数式フォントのプリセットを登録する |

どのコマンドもプリアンブルでだけ使えます．
パッケージオプション `alphabet` を指定すると，(u)pLaTeX で `pxchfon` を `alphabet` オプションつきで読み込みます．

### プリセット

| 種類 | 名前 |
| --- | --- |
| 本文フォント | `default`，`timesnew`，`IPA`，`Kyokasyo`，`BIZUD`，`BIZUDo`，`oradano`，`yumin`，`mika` |
| 数式フォント | `default`，`timesnew`，`xits` |

> Note: IPA フォントと XITS Math は TeX Live に含まれます．
> そのほかのフォントは別に入手してください．
> フォントのファイル名や各プリセットの内容は，`masyufont-doc.pdf` の「プリセット一覧」を参照してください．

## ファイル構成

| ファイル | 説明 |
| --- | --- |
| `masyufont.sty` | パッケージ本体 |
| `masyufont-doc.tex`，`masyufont-doc.pdf` | ドキュメントとそのソース |
| `README.md` | このファイル |
| `LICENSE` | ライセンス |

ドキュメントを組版し直すには，次を実行します．

```
lualatex masyufont-doc
lualatex masyufont-doc
```

## ライセンス

MIT License の下で配布・改変が可能です．詳細は [LICENSE](LICENSE) を参照してください．

---

## 変更履歴

- Version 0.2 (2026-11-26): 読み込み時に未定義の `\@xp` でエラーになり，どのエンジンでも使えなかった問題を修正．`\masyuMathFontDefine` が本文フォント側に登録していた問題，`mika` プリセットの (u)pLaTeX 側で未定義の命令を呼んでいた問題を修正．内部の `\addoption`，`\optiondef` を廃止．ライセンスを MIT License にした．ドキュメント（`masyufont-doc.pdf`）を追加．別パッケージの内容になっていた `masyufont.dtx` と，書きかけの `masyufont.tex` を削除．
- Version 0.1 (2019-12-12): 初版．
