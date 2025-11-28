# LaTeX論文テンプレート

日本語LaTeX論文執筆用のテンプレートリポジトリです。セクション分割、参考文献管理、自動ビルド機能を備えています。

## 特徴

- 📝 セクション分割による構造化された論文執筆
- 📚 BibTeXによる参考文献管理
- 🔄 自動ビルドとウォッチモード
- 📦 npmスクリプトによる簡単なビルド管理
- 🎯 日本語LaTeX環境に対応
- 🚀 GitHub Actionsによる自動PDF生成

## 必要な環境

- Node.js と npm
- TeX Live（日本語LaTeX環境）

## 環境構築手順

### 1. Node.js と npm のインストール確認

```bash
node --version
npm --version
```

### 2. TeX Live のインストール

#### 2.1 基本パッケージのインストール

```bash
sudo apt-get update
sudo apt-get install texlive
```

#### 2.2 日本語LaTeXパッケージのインストール

```bash
sudo apt-get install texlive-lang-japanese
```

これにより、以下のコマンドが利用可能になります：
- `platex` - 日本語LaTeXコンパイラ
- `pbibtex` - 日本語BibTeX
- `dvipdfmx` - DVIからPDFへの変換ツール

### 3. npm パッケージのインストール

```bash
npm install
```

これにより、以下の開発依存パッケージがインストールされます：
- `chokidar-cli` - ファイル監視ツール
- `npm-run-all` - 並列コマンド実行ツール

## 使い方

### 1. リポジトリのクローン

```bash
git clone https://github.com/takapi-s/latex-template.git
cd latex-template
```

### 2. プロジェクトのカスタマイズ

1. `main.tex` を開き、タイトル、著者名、日付を編集
2. `sections/` ディレクトリ内の各セクションファイルを編集
3. `main.bib` に参考文献を追加

### 3. ビルド方法

#### 完全ビルド（推奨）

参考文献を含む完全なPDFを生成します：

```bash
npm run build
```

このコマンドは以下の処理を順番に実行します：
1. 一時ファイルのクリーンアップ
2. LaTeXの第1回コンパイル
3. BibTeXによる参考文献の処理
4. LaTeXの第2回コンパイル（参考文献の反映）
5. LaTeXの第3回コンパイル（相互参照の解決）
6. DVIからPDFへの変換

#### 開発用ビルド（高速）

参考文献の処理をスキップした高速ビルド：

```bash
npm run build-dev
```

#### ウォッチモード（自動再ビルド）

ファイル変更を監視して自動的に再ビルドします：

```bash
npm run watch
```

個別の監視：
- `npm run watch:tex` - .texファイルのみ監視
- `npm run watch:bib` - .bibファイルのみ監視

#### クリーンアップ

一時ファイルを削除します：

```bash
npm run clean
```

#### GitHub Actionsによる自動ビルド

このリポジトリにはGitHub Actionsのワークフローが設定されており、以下のタイミングで自動的にPDFがビルドされます：

- `main`または`master`ブランチへのプッシュ時
- プルリクエスト作成時
- 手動実行（GitHubのActionsタブから実行可能）

**ビルドされたPDFの取得方法：**

1. GitHubリポジトリのページにアクセス
2. 上部の「Actions」タブをクリック
3. 左側のサイドバーから「Build PDF」ワークフローを選択
4. 実行履歴から最新の実行をクリック
5. ページ下部の「Artifacts」セクションから「pdf」をクリックしてダウンロード

生成されたPDFは30日間保持されます。ビルドが成功すると、PDFファイルがアーティファクトとして利用可能になります。

## プロジェクト構造

```
.
├── main.tex              # メインのLaTeXファイル
├── main.bib              # 参考文献データベース
├── sections/             # セクションファイル
│   ├── introduction.tex  # はじめに
│   ├── related_work.tex  # 関連研究
│   ├── methodology.tex   # 提案手法
│   ├── experiments.tex   # 実験
│   ├── results.tex       # 結果と考察
│   └── conclusion.tex    # 結論
├── output/               # ビルド出力ディレクトリ（自動生成）
│   ├── main.pdf          # 生成されたPDFファイル
│   ├── main.dvi          # 中間DVIファイル
│   └── *.aux, *.bbl, etc. # 一時ファイル
├── package.json          # npm設定ファイル
├── .gitignore           # Git除外設定
├── LICENSE              # ライセンス
└── README.md             # このファイル
```

**注意**: `output`フォルダはビルド時に自動的に作成され、すべてのビルド出力ファイル（PDF、DVI、一時ファイルなど）がここに保存されます。

## 使用可能なnpmスクリプト

| コマンド | 説明 |
|---------|------|
| `npm run build` | 完全ビルド（参考文献含む） |
| `npm run build-dev` | 開発用ビルド（高速） |
| `npm run build:tex` | LaTeXコンパイルのみ |
| `npm run build:bib` | BibTeX処理のみ |
| `npm run build:dvi` | DVIからPDFへの変換のみ |
| `npm run watch` | ファイル変更の監視と自動再ビルド |
| `npm run clean` | 一時ファイルの削除 |

## 参考文献の追加方法

`main.bib` ファイルにBibTeX形式で参考文献を追加してください。例：

```bibtex
@article{example2024,
  title={Example Paper Title},
  author={Author, Name},
  journal={Journal Name},
  year={2024}
}
```

本文中で引用する場合は：

```latex
\cite{example2024}
```

## トラブルシューティング

### `platex: Permission denied` エラー

日本語LaTeXパッケージがインストールされていません：

```bash
sudo apt-get install texlive-lang-japanese
```

### `File 'xxx.sty' not found` エラー

必要なLaTeXパッケージが不足しています。以下のいずれかを実行：

1. 使用していないパッケージを `main.tex` から削除
2. 必要なパッケージをインストール（通常は `texlive-latex-extra` などに含まれる）

### ビルドが途中で止まる

LaTeXのコンパイル中にエラーが発生した可能性があります。ログファイル（`output/main.log`）を確認してください。

## 注意事項

- 完全ビルドには、LaTeXのコンパイルを3回実行する必要があります（参考文献と相互参照の解決のため）
- **すべてのビルド出力ファイル（PDF、DVI、一時ファイル）は `output/` ディレクトリに保存されます**
- PDFファイル（`output/main.pdf`）は `npm run build` または `npm run build-dev` の後に生成されます
- 一時ファイルは `npm run clean` で削除できます（`output/` ディレクトリ内のファイルが削除されます）
- `output/` ディレクトリは `.gitignore` に含まれているため、Gitには追跡されません

## ライセンス

このテンプレートはMIT Licenseの下で公開されています。詳細は[LICENSE](LICENSE)ファイルを参照してください。

## 貢献

バグ報告や機能要望は、GitHubのIssuesでお知らせください。プルリクエストも歓迎します。
