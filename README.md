# Docker コンテナ環境をきれいにする

## 開発環境

- Windows 11 Home Ver. 21H2
- Docker Desktop for Windows

## 起動中のコンテナの確認

docker ps でプロセスの状態を確認

```console
docker ps
```
## 停止中のコンテナの削除

docker rm コンテナIDもしくはコンテナ名 ですべてのコンテナを削除できます。

次のコマンドは、docker ps -q で全コンテナのIDを取得し、それをdocker rm に渡しているコマンドです。

```console
docker rm $(docker ps -aq)
```

実行結果例：
```
330ddbe7aee0
8aef7f9046fa
a542eca70416
5225b7609af9
c495fdee1b2b
0fd1dd889b0a
0f68c8d2e932
c44cde856cf2
```

## イメージの削除

docker images でローカルに保存されている全てのイメージを表示できます。

```console 
docker images
```

```
REPOSITORY                                           TAG                 IMAGE ID            CREATED             SIZE
aspnetcorejwtvue_db                                  latest              951174b03a8c        3 months ago        1.35GB
disaster-stock-master-app_db                         latest              951174b03a8c        3 months ago        1.35GB
disasterstockmaster_db                               latest              951174b03a8c        3 months ago        1.35GB
mssqlserverlinux_db                                  latest              77415daff16b        3 months ago        1.35GB
explainhow_to_start_dotnet_apiwith_efwith_mssql_db   latest              ca683416b3b3        3 months ago        1.35GB
<none>                                               <none>              54846e230fdd        3 months ago        1.35GB
<none>                                               <none>              040216db7bb4        3 months ago        1.35GB
<none>                                               <none>              662778c57f37        3 months ago        1.35GB
<none>                                               <none>              5056808239a9        3 months ago        1.35GB
mssql-server-linux-sample_db                         latest              e10d64f06cd0        3 months ago        1.35GB
<none>                                               <none>              1e921655411b        3 months ago        1.35GB
<none>                                               <none>              2a74262944cf        3 months ago        1.35GB
<none>                                               <none>              e5c6fcdd8623        3 months ago        1.35GB
<none>                                               <none>              c3f398f5c824        3 months ago        1.35GB
<none>                                               <none>              0924d659d556        3 months ago        1.35GB
<none>                                               <none>              31ec89abbb29        3 months ago        1.35GB
docker-compose-laravel-lemp_backend                  latest              cd771e279fba        4 months ago        481MB
calender-app_api                                     latest              fa5ac8abaaf6        4 months ago        89.3MB
calender-app_nginx                                   latest              13dbc2293f61        4 months ago        133MB
php                                                  7.4-fpm             89cffc06d538        4 months ago        405MB
mac_app                                              latest              a80d1a1fe4b7        4 months ago        423MB
nginx-php-mysql-docker-compose_app                   latest              a80d1a1fe4b7        4 months ago        423MB
php-for-android-firebase-notification_app            latest              a80d1a1fe4b7        4 months ago        423MB
mysql                                                5.7                 ef08065b0a30        4 months ago        448MB
mysql                                                8.0                 e1d7dc9731da        4 months ago        544MB
mysql                                                latest              e1d7dc9731da        4 months ago        544MB
adminer                                              latest              b0101225da58        4 months ago        90.5MB
mariadb                                              latest              b28df07deb6c        5 months ago        407MB
nginx                                                alpine              6f715d38cfe0        5 months ago        22.1MB
nginx                                                latest              4bb46517cac3        5 months ago        133MB
node                                                 lts-alpine          18f4bc975732        6 months ago        89.3MB
php                                                  7.4.0-fpm           0203f6c79234        13 months ago       405MB
microsoft/mssql-server-linux                         2017-latest         314918ddaedf        2 years ago         1.35GB
microsoft/mssql-server-linux                         latest              314918ddaedf        2 years ago         1.35GB
```
次のコマンドは、docker images -q で全イメージのIDを取得し、それを docker rmi に渡しているコマンドになります。

```console
docker rmi $(docker images -q)
```

実行結果例：
```
Untagged: mssqlserverlinux_db:latest
Deleted: sha256:77415daff16b1860b16d4a6583e89822f8078859d0c9a2e02d0de8dc6b08e904
Deleted: sha256:3e70244e7bb2b63c6b839636a84a5fe2703321489f3e2c324fd7ac23e361f8dc
Deleted: sha256:ef8c857952ffd2463653ca5f7c48a1bca133c0ff684aaf6d064e103a269a633a
Deleted: sha256:98e2c43fbdc68a74751e273e21ce0a638b358f9c14d9e7f55438fe651b33e7ae
Deleted: sha256:bfcba82d01c0c56f1f0028f3619bfc21c4e70d8b67689141935d679fd3509bf0
Deleted: sha256:a630c377052eda4cf24d3bcefe92f2c283a18d43b01c44468e46869e799c6691
Untagged: explainhow_to_start_dotnet_apiwith_efwith_mssql_db:latest
Deleted: sha256:ca683416b3b382f0fc4344f0afd0479bb453061f016fe6417cf978e8781c2fb8
Deleted: sha256:55d3d05bcdd6222a5252b9c55522afa545ab3c0e67e6394dfcc1a58f3f0c2b4c
Deleted: sha256:506e78957263b3c5d72bae262c6f330d6323315581c122fb5812a1ee3bb88f21
Deleted: sha256:9f2b362eb2b304d7e67ff76fb88861c02e92018f3877392721da4397b6487077
Deleted: sha256:1b273aca7e47ad148445b6ee1e075727c1d6e9b91249a35335eb50d41a34faea
Deleted: sha256:13aa4ff004fdb62d5e64eee693b975980553fe604b52e520dc96c213149ead76
Deleted: sha256:54846e230fdda2a7ae5510572ce8a40706c02b40287bc1b235a203cd72f8fb44
Deleted: sha256:c7999be93edc46d05977a0e60f38382d15a0780ce351c1d4cab5674d759753d2
Deleted: sha256:ce8c57ebfd44a3ae3c43a8422cb1c61e4e41d53398c03c4dea8be58852dd5376
Deleted: sha256:419d3e9011e61d259704fbdc37b920b81babf2e38ecf7334ff048fff4ac27785
Deleted: sha256:a469bacff36c77a5fc5d6f425050c3faa82892ac46fbc48a5213c57afbcb76a6
Deleted: sha256:d07c3c51f315bdae915981fc2de1c8f0d064fb91b63114df654a71d46b5a8b80
Deleted: sha256:040216db7bb49a0354e416dd4b92a4f94bdb327dd2aa6add52ba794d456f9a90
Deleted: sha256:aa6c843aef873fd2af417423e88498e614ae501b11280aaceb2922ef6a651fbc
Deleted: sha256:ef2004a8f8bf55668b6d867daf7b67acb21f9ba67a1d258a12f72c7a944102c1
Deleted: sha256:a9ebc330fe7e99d41dd048d273631df33556c6b45de98781cd5b70db35ecb514
Deleted: sha256:bba799067c6dcb0b2d9afbffe956287a2ad52442d488c552025206415ee53ca2
Deleted: sha256:9755960fe0f50ee822fd6f37d3125f15418cc2166b4f71e552eb17689afa5091
Deleted: sha256:662778c57f37d3ac25652a5ae6ec02d59391f0b7150055c170fc9e9b89e7b54c
Deleted: sha256:ca4c1a71c07b0c8ea551efd5248a13ead6b1d2fcf9d6908960bbd92b57bf75e6
Deleted: sha256:e5b55e8d6dd1dc4e8b05cd72f3b14c1dd79ba16e919f71ec16614c3654a00019
Deleted: sha256:ada934fbd26dc72e549b31f1e3f70ac5501571c279da5a8973eb63e88221cda0
Deleted: sha256:8f4bab88bde7fd3b3e5f154a421ead3fcad7f5390c1a19499f30af4be75cc325
Deleted: sha256:fd538833cde54f25db53beff09f3add06993ecb97e95e0d84951bbe3865162a5
Deleted: sha256:5056808239a9a5def38845bab82664d6f4bb7ec21a44792baac993c0e61d478c
Deleted: sha256:ad25cb356139e279f705a0bbe429f58bfeec59404a59890071371c02802b594b
Deleted: sha256:354d1922a01994c97e2feea3a69794c07174a6ac7e3f219059bdb3581b26270d
Deleted: sha256:68ee0e421e7174e884b9991ec40c1cf080bf36d0097ec6c97867064689360445
Deleted: sha256:a53c15642ad7d1010d26b8cb725161838b127ae988fd07c7d4fdcef6b2345c94
Deleted: sha256:ff5c84572cd51b11dd81af1154b1b0a516fd9c093381916d660ea134261e0e7d
```
