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

# jenkinsを立てます
sudo docker-compose up -d
```

## FAQ

### Q. Jenkins で SSH したい

A. `/jenkins/.ssh/` の情報を使ってsshします。

### Q. ユーザー情報を追加したい

A. デフォルトユーザーの ID/PASS は今のところ `docker-compose.yaml` 内に記載されています。
そのほか、ユーザーを追加したい場合は `/jenkins/jenkins_home/init.groovy.d/` をカスタマイズします。

### Q. プラグインを管理したい

A. `/jenkins/jenkins_home/init.groovy.d/setup-plugins.groovy` をカスタマイズします。
