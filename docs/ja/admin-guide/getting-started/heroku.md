# Heroku

## アプリの起動

1. Go to [the latest release page on GitHub](https://github.com/weseek/growi/releases/latest)
1. Go to file tree URL like https://github.com/weseek/growi/tree/vX.X.x
1. Click "Deploy to Heroku" button at the top of README.md
      1. Your browser will jump to Heroku
      1. Login if you need
1. Deploy app


## アップグレード

### Heroku CLI のインストール

[公式ページ](https://devcenter.heroku.com/articles/heroku-cli#download-and-install)を参考にHeroku CLIをインストールしてください。


### Heroku CLI を使って App のリポジトリを更新する

まず以下のコマンドによりHerokuにログインします。
```
$ heroku login 
```

続いて, Herokuからリポジトリをクローンします。クローンするときの名前はHerokuでのApp Nameになります.
`warning: You appear to have cloned an empty repository.`のようなメッセージが出ることがありますが無視して構いません。
```
heroku git:clone -a [App Name]
```

git remoteで正しくremoteが登録されているか確認します。
```
$ git remote -v
heroku	https://git.heroku.com/[App Name].git (fetch)
heroku	https://git.heroku.com/[App Name].git (push)
```

続いて, GitHub上のGROWIのリポジトリをremoteに登録します。
```
$ git remote add origin https://github.com/weseek/growi.git
```

登録したGROWIリポジトリからtag一覧を取得します。
```
$ git pull origin --tags 
```

使用したいバージョンにブランチを作成してチェックアウトします。
```
$ git checkout -b growi-vX.X.X refs/tags/vX.X.X
```

作成したブランチをHerokuリポジトリのmasterにpushします。これにより、Heroku上でbuildとdeployが行われエラー等がでなければアップグレード完了となります。場合によっては`--force`オプションの付与が必要になります。
```
$ git push heroku growi-vX.X.X:master
```
