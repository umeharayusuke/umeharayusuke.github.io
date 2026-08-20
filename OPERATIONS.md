# 公開・更新ガイド

## 1. 最初に差し替えるもの

```powershell
rg "umeharayusuke|example.com|0000-0000-0000-0000|20XX|Replace|replace" . -g "!docs/**"
```

`_quarto.yml` の `site-url`、`contact.qmd`、経歴・研究内容を修正します。顔写真を使う場合は `assets/profile.jpg` を置き、`index.qmd` の `portrait-placeholder` ブロックを以下に置換します。

```markdown
![](assets/profile.jpg){.profile-photo fig-alt="Portrait of Yusuke Umehara"}
```

## 2. ローカル確認

通常は `quarto preview` を実行します。このPCでは次のRStudio同梱版も使えます。

```powershell
& 'C:\Program Files\RStudio\resources\app\bin\quarto\bin\quarto.exe' preview
```

保存するとブラウザ表示が自動更新されます。公開用HTMLを作るだけなら `quarto render` です。

## 3. GitHubへ初回公開

GitHubで公開リポジトリを作ります。ユーザーサイトなら名前を `umeharayusuke.github.io` にします。プロジェクトサイトなら任意名（例: `academic-website`）で、URLは `https://umeharayusuke.github.io/academic-website/` です。

このフォルダで実行します（各値は置換）。

```powershell
git init
git branch -M main
git add .
git commit -m "Create academic website"
git remote add origin https://github.com/umeharayusuke/umeharayusuke.github.io.git
git push -u origin main
```

GitHubの **Settings → Pages** で以下を選びます。

- Source: `Deploy from a branch`
- Branch: `main`
- Folder: `/docs`

保存後、数分待って公開URLを確認します。

## 4. 普段の更新

1. `.qmd` または `styles.css` を編集する。
2. `quarto preview` で確認する。
3. `quarto render` で `docs/` を更新する。
4. 差分を確認し、GitHubへ送る。

```powershell
git status
git diff
git add .
git commit -m "Update research and publications"
git push
```

`docs/` もコミットするのが重要です。push後、GitHub Pagesが再公開します。

## 5. 独自ドメイン

まずGitHubの **Settings → Pages → Custom domain** に購入済みドメインを入力し、その後DNSを設定します。`www.example.com` のようなサブドメインは通常CNAMEを `umeharayusuke.github.io` に向けます。ルートドメインのA/AAAA値は設定時にGitHub公式資料で最新値を確認してください。DNS反映後に **Enforce HTTPS** を有効にし、`_quarto.yml` の `site-url` も変更します。

## 6. おすすめの運用

- 月1回、所属・CV・研究テーマを確認する。
- 論文採択、発表、プロジェクト公開のたびに更新する。
- 公開後はスマートフォン表示と全リンクを確認する。
- 主要情報はPDFだけでなくHTMLにも載せる。
- 公開してよいメールアドレスだけを掲載する。
- 図は圧縮し、意味のある代替テキストを付ける。
