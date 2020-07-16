# gatsby-tutorial
Gatsby を GitHub Pages に表示させる

## Getting Started  

### Install the Gatsby CLI  
Gatsby CLI をシステムにインストールする。

```
npm i -g gatsby-cli
```

### Create a new site  
```
gatsby new プロジェクト名
```

テーマを指定する場合は以下のコマンド（以下の例は Code Bushi のテーマを使用）。
```
gatsby new プロジェクト名 https://github.com/codebushi/gatsby-theme-document-example
```


GitHub にリポジトリを作成しておく。

### Change directories into site folder
```
cd .\プロジェクト名
git init 
git config --local user.name fs5013-furi-sutao
git config --local user.email fs5013.furi.sutao@gmail.com
git add .
git commit -m "first commit"
git remote add origin https://ユーザ名:パスワード@github.com/fs5013-furi-sutao/プロジェクト名.git
git push -u origin master
```

### Start development server
```
gatsby develop
```

localhost:8000 のアドレスでブラウザを確認する。
http://localhost:8000

以下のファイルを編集して、ヘッダのロゴが変わることを確認する
`src/gatsby-theme-document/logo.mdx`

## コンテンツを追加する
ドキュメントはMDXで作成されている。コンテンツは、コンテンツフォルダーでMDXファイルを作成または編集することで追加できる。

`content/index.mdx`

MDX を使用すると、JSX または React コンポーネントをマークダウンファイルに追加できる。画像は任意の .mdx ファイルに追加することもでき、gatsby-remark-images を使用して自動的に最適化される。

## Installing the gh-pages package

Gatsby アプリを GitHub Pages にプッシュするには、gh-pages というパッケージを使う。

gh-pages
https://github.com/tschaub/gh-pages

```
npm install gh-pages --save-dev
```

## デプロイスクリプトの使用
package.json にカスタムスクリプトを記述することで、サイトの構築が容易になり、構築したファイルの内容を GitHub Pages 用の適切なブランチに移動させることができ、そのプロセスの自動化に役立つ。

## GitHub Pages のパスへのデプロイ
username.github.io/reponame/ のようなパスでデプロイされたサイトの場合、--prefix-paths フラグが使用される。gatsby-config.js のオプションとして/reponame パスのプレフィックスを追加する必要がある。

```gatsby-config.js
module.exports = {
  pathPrefix: "/reponame",
}
```

そして、リポジトリのコードベースにある package.json にデプロイスクリプトを追加する。

```package.json
{
  "scripts": {
    "deploy": "gatsby build --prefix-paths && gh-pages -d public"
  }
}
```

npm run deploy を実行すると、public フォルダのすべての内容がリポジトリの gh-pages ブランチに移動する。リポジトリの設定で、デプロイ元として gh-pages ブランチが設定されていることを確認する。

```
npm run deploy
```

NOTE: master や gh-pages を公開ソースとして選択するには、そのブランチがリポジトリに存在している必要がある。master や gh-pages のブランチがない場合は、ブランチを作成してからソースの設定に戻り、公開ソースを変更することができる。