# 検証脆弱性一覧
本検証は、以下の脆弱性を検証することができます。
* nginxの設定ミスで起こるHTTP Splitting
* nginxの設定ミスで起こるパス トラバーサル
* nginxの設定ミスで起こるSSRF
* nginxの設定ミスで起こるレスポンスヘッダの出力不備
* nginxの設定ミスで起こるMultiline response headers
* nginxの設定ミスで起こるreferer/origin検証の問題
* nginxの設定ミスで起こるリファラの検証不備
* nginxの設定ミスで起こるHostヘッダフォージェリ

[原文](https://github.com/yandex/gixy/tree/master/docs/en/plugins)

[翻訳記事](https://qiita.com/no1zy_sec)

# Dockerの環境の構築
本検証を実施する場合には、以下の環境を用意してください。
* dockerが動くこと
* nginxイメージがインストールされていること(無くても自動的にインストールします)
* docker-composerコマンドが動作すること

また一部の検証で、リクエスト改ざんのためにローカルプロキシツールが必要になります。

# VMの設定
検証環境がVMにある場合、VMのネットワーク設定に以下の設定を入れてください。  
[host]127.0.0.1:80 <=>[guest]0.0.0.0:8080

# 検証環境の立ち上げ方
本リポジトリをクローンしてください。

クローンしたリポジトリのディレクトリに移動し、以下のコマンドを実行してください。
> docker-compose up

# hosts設定
hostsファイルに以下の設定を追加してください。

- 127.0.0.1 badnginx.com
- 127.0.0.1 www.badnginx.com
- 127.0.0.1 evilnginx.com
- 127.0.0.1 www.badnginx.com.evilnginx.com
- 127.0.0.1 banginx.local