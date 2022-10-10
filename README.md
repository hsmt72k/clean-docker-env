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
... 中略 ...
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
... 中略 ...
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
... 中略 ...
Deleted: sha256:a630c377052eda4cf24d3bcefe92f2c283a18d43b01c44468e46869e799c6691
Untagged: explainhow_to_start_dotnet_apiwith_efwith_mssql_db:latest
Deleted: sha256:ca683416b3b382f0fc4344f0afd0479bb453061f016fe6417cf978e8781c2fb8
... 中略 ...
Deleted: sha256:ff5c84572cd51b11dd81af1154b1b0a516fd9c093381916d660ea134261e0e7d
```

## Docker の容量利用状況を確認

現在の Docker の容量利用状況を確認するには `docker system df` コマンドを実行する。

`Docker の容量利用状況を確認`
``` console
docker system df
```

`実行結果例`
``` console
TYPE            TOTAL     ACTIVE    SIZE      RECLAIMABLE
Images          0         0         0B        0B
Containers      0         0         0B        0B
Local Volumes   0         0         0B        0B
Build Cache     42        0         85.81MB   85.81MB
```

Build Cache が残っていることが分かる。

### Build Cache を削除

この Build Cache は `docker builder prune` コマンドで削除できる。

`Build Cache を削除`
``` console
docker builder prune
```

「Build Cache が削除されます。本当に続けますか？」と聞かれるので、問題なければ `y` を入力する。

`実行結果例`
``` console
WARNING! This will remove all dangling build cache. Are you sure you want to continue? [y/N] y
Deleted build cache objects:
m165f4itt84bdf9iwedz5ogth
... 中略 ...
898w3j5nbbn0ev04l81ka3wmz

Total reclaimed space: 85.81MB
```
