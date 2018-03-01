# Docker on Jenkins Example

CIサーバーの構成管理

## 環境構築

### 事前準備

以下ののソフトウェアを事前に導入する必要があります。

* docker
* docker-compose

### 起動

```
# キーを作ります
ssh-keygen -t rsa -f ./jenkins/keys/id_rsa -N ""

# Dockerのコンテナに合わせて権限をrootに設定する
sudo chown -R ./jenkins/jenkins_home

# jenkinsを立てます
sudo docker-compose up -d
```

## FAQ

### Q. Jenkins で SSH したい

認証情報を追加します。  
/jenkins/key ディレクトリに鍵を作っておけば /root/keys の中に鍵が作られます。
その鍵をjenkinsに指定します

pipelineは以下の書き方で通ります

```
sshagent(credentials: ['crediential-id']) {
  sh "ssh -e o StrictHostKeyChecking=no xxx@xxx"
  sh "rsync -aze \"ssh -o StrictHostKeyChecking=no\" ./ xxx@xxx:~/xxxx"
}
```

`known_hosts` が毎回初期化されてしまって、確認求められて失敗する。
それを回避すると次はなりすましされる可能性があるのは現在対応考え中…。

### Q. ユーザー情報を追加したい

A. デフォルトユーザーの ID/PASS は今のところ `docker-compose.yaml` 内に記載されています。
そのほか、ユーザーを追加したい場合は `/jenkins/jenkins_home/init.groovy.d/` をカスタマイズします。

### Q. プラグインを管理したい

A. `/jenkins/jenkins_home/init.groovy.d/setup-plugins.groovy` をカスタマイズします。

ID は[こちら](https://plugins.jenkins.io/)を参照
