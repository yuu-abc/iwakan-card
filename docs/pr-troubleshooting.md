# Pull Requestで緑のMergeボタンが出ないとき

GitHubのPull Request画面で緑の「Merge pull request」ボタンが出ない場合は、アプリの不具合ではなく、GitHub上でマージできない状態になっている可能性が高いです。

## よくある原因

- **競合があります**: `This branch has conflicts that must be resolved` と表示されている場合、同じファイルを別々の内容で変更しています。
- **ベースブランチが進んでいます**: Pull Requestを作ったあとに、取り込み先のブランチへ別の変更が入っています。
- **GitHubの確認中です**: 画面に `Checking for ability to merge automatically` と出ている場合は、少し待ってから再読み込みしてください。

## まず試すこと

1. Pull Request画面を再読み込みします。
2. `Update branch` ボタンが出ていれば押します。
3. `Resolve conflicts` ボタンが出ていれば押し、競合しているファイルを確認します。
4. 競合の解消が難しい場合は、このブランチの `index.html` を採用する形で競合を解消します。

## 今回のリポジトリで見るポイント

このアプリは基本的に `index.html` だけで動く静的HTMLアプリです。競合が出ている場合は、まず `index.html` が競合していないか確認してください。

`README.md` はアプリの動作には必須ではありません。`README.md` だけが競合している場合は、GitHub上で取り込み先ブランチの内容を残すか、Pull Request側からREADME変更を外してもアプリ本体には影響しません。

## GitHub上で解決できない場合

GitHubの競合解消画面で直せない場合は、ローカルでベースブランチを取り込んでから競合を解消し、再度pushします。

```bash
git fetch origin
git checkout <作業ブランチ名>
git merge origin/<取り込み先ブランチ名>
# 競合を直す
git add index.html
git commit
git push
```

作業ブランチ名や取り込み先ブランチ名が分からない場合は、Pull Request画面の上部に表示されている `base` と `compare` を確認してください。
