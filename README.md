# vccw

https://capitalp.jp/2017/12/16/naoki-1/
だいたいここ参照させていただいてます。


## Homebrewのインストール

### Xcodeインストール
```
$ xcode-select --install
```
### Homebrewインストール
```
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
##### インストールされているかを確認
```
$ brew doctor
Your system is ready to brew.
```
上のように Your system is ready to brew と表示されれば大丈夫。そうじゃなければ表示されているメッセージをよく読んで問題を解決しましょう。
ここで適当にあきらめて次の処理に進んでも絶対にうまく行きません。
nodeとかパッケージ版でインストールしているとガンガンエラー出ますw


##### Homebrewは定期的にメンテナンスが必要です。以下のコマンドは手が空いたときにやっておきましょう。

アプデ
```
$ brew update && brew upgrade
```
キャッシュを掃除
```
$ brew cleanup
```
Homebrewの動作テスト
```
$ brew doctor
```

## 主要なコマンドのインストール

### gitインストール
```
$ brew install git curl
```
### PHPインストール
```
$ brew install php72
```
最新版をインストールしときます？

## MySQLのインストール
### gitインストール
```
$ brew install mysql
```
次にインストールした MySQL がパソコンの再起動後に自動的に起動するようにします。
```
$ brew services start mysql
```

## WP-CLIのインストール
```
$ cd
$ curl https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli-nightly.phar -o wp
$ chmod 755 wp
$ mv wp /usr/local/bin/
```
最後に wp --info で動作確認しましょう。以下のような出力に（だいたい）なっていればオッケーです。
```
$ wp --info
PHP binary:	/usr/local/Cellar/php72/7.2.0_11/bin/php
PHP version:	7.2.0
php.ini used:	/usr/local/etc/php/7.2/php.ini
WP-CLI root dir:	phar://wp-cli.phar
WP-CLI vendor dir:	phar://wp-cli.phar/vendor
WP_CLI phar path:	/Users/miya
WP-CLI packages dir:	/Users/miya/.wp-cli/packages/
WP-CLI global config:	
WP-CLI project config:	
WP-CLI version:	1.5.0-alpha-d71d228
```
この時点でうまく行っていなければ一番最初からやり直してください。


## Nodeのインストール
```
$ brew install node
```

## Rubyのインストール
```
$ brew install ruby
```

## Gitの設定
Gitにユーザー名とメールアドレスを設定します。今回は無難にGitHubのユーザー名とメールアドレスを設定しましょう。
GitHubにサインアップしていない場合はサインアップしてください。
サインアップしたらGitHubのユーザー名を以下のように設定します。 username の部分をみなさんのGitHubのユーザー名と置き換えてください。
```
$ git config user.name "username"
```
```
git config user.email "xxx@xxx.com"
```

## WP-CLIのコマンド補完を有効化する
以下のコマンドで必要なスクリプトをインストールします。
```
$ curl -L https://raw.githubusercontent.com/wp-cli/wp-cli/master/utils/wp-completion.bash -o ~/.wp-completion.bash
```
次に``` ~/.bash_profile ```に設定を記述します。
```
source ~/.wp-completion.bash
```
ターミナルを開き直すか```source ~/.bash_profile```コマンドを実行して設定を反映させてください


# 初心者がコマンドと付き合うときに最低限覚えておくべきこと
## sudo は安易に実行しない
```sudo```は root 権限と呼ばれるとても大きな権限でコマンドを実行するために使用します。
この記事で```sudo```を一度も実行していないことからも分かる通り、ローカル環境で```sudo```を使用することはめったにありません。
一度これで実行してしまうと次回以降つねに```sudo```をしてしまわないといけなくなりますし、権限が大きいためにシステムのトラブルを招きやすいだけでなく悪意があるコードをとても大きな権限で実行してしまうリスクもあります。
```sudo```は使用しないでください。また安易に```sudo```を書いてあるブログ等は見る価値がありません。

## 仮想環境のインストール

### Vagrantインストール
[Vagrant](https://www.vagrantup.com/downloads.html?utm_source=capitalp&utm_campaign=SponsorUs&utm_medium=voluntary_link)


### Virtualboxインストール
[Virtualbox](http://www.oracle.com/technetwork/server-storage/virtualbox/downloads/index.html?ssSourceSiteId=otnjp&utm_source=capitalp&utm_campaign=SponsorUs&utm_medium=voluntary_link)

#### Vagrantプラグインインストール
```
$ vagrant plugin install vagrant-hostsupdater
```
```
$ curl https://raw.github.com/brbsix/vagrant-bash-completion/master/vagrant-bash-completion/etc/bash_completion.d/vagrant -o vagrant
$ mv vagrant `brew --prefix`/etc/bash_completion.d/
```
最後に以下のコードを```~/.bash_profile```にコピペして```、source ~/.bash_profile```するかターミナルを再起動してください。
```
if [ -f `brew --prefix`/etc/bash_completion.d/vagrant ]; then
    source `brew --prefix`/etc/bash_completion.d/vagrant
fi
```

### Varantの使い方

```vagrant up``` – 起動 
```vagrant halt``` –  停止 
```vagrant destroy``` – 廃棄 
```vagrant provision``` – 再構築 
```vagrant global-status``` – 全マシンのステータスを確認 


```
cd [directory]
wp scaffold vccw [directory_name] --host=[host_name] --ip=192.168.33.10
ex) wp scaffold vccw vccw.test --host=vccw.test --ip=192.168.33.10
```


