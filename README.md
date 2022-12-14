# Docker コンテナ環境をきれいにする

## 開発環境

- Windows 11 Home Ver. 21H2
- Docker Desktop for Windows

## コンテナの状況確認

## 起動中のコンテナを表示

docker ps コマンドで、起動しているコンテナの状態を確認できる。

`起動しているコンテナ一覧を表示するコマンド` 
```console
docker ps
```

## すべてのコンテナを表示

起動しているコンテナだけではなく、
停止しているコンテナも含めたい場合は、-a オプションをコマンドに含める。

`停止しているコンテナも含めてコンテナ一覧を表示するコマンド` 
```console
docker ps -a
```

## 停止中のコンテナの削除

停止中のコンテナを削除するには、`docker rm` コマンドを実行する。

`docker rm` コマンドの引数には、CONTAINER ID を指定する。

`コンテナを削除するコマンド（CONTAINER ID に 41595c20a1d7 を指定した場合）`
``` console
docker rm 41595c20a1d7
```

### ローカルにあるコンテナをすべて削除したい場合

次のコマンドは、docker ps -q で全コンテナの ID を取得し、
その結果を docker rm に渡しているコマンドとなる。

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

## Docker volume を確認する

コンテナを削除しても永続化した volume は残り続けるので、
コンテナを削除したら、不要になった volume も削除したい。

Docker volume を確認するには、`docker volume ls` コマンドを実行する。

`Docker volume 一覧を表示するコマンド`
``` console
docker volume ls
```

`実行結果例:`
``` console
DRIVER    VOLUME NAME
local     react-dev-container_devcontainer_node_modules
local     vscode
```

## Docker volume の削除

Docker volume を削除するには、`docker volume rm` コマンドを実行する。

`Docker volume を削除するコマンド（VOLUME NAME に react_devcontainer を指定した場合）`
``` console
docker volume rm react_devcontainer
```

### ローカルにある Volume をすべて削除したい場合

次のコマンドは、docker volume ls で全イメージの ID を取得し、
その結果を docker rm に渡しているコマンドとなる。

```console
docker volume rm $(docker volume ls -q)
```

## Docker Image の確認

docker images でローカルに保存されている全てのイメージを表示できる。

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

## イメージの削除

Docker Image を削除するには、`docker rmi` コマンドを実行する。

`Docker Image を削除するコマンド（IMAGE ID に 951174b03a8c を指定した場合）`
``` console
docker rmi 951174b03a8c
```

### ローカルにあるイメージをすべて削除したい場合

次のコマンドは、docker images -q で全イメージの ID を取得し、
その結果を docker rmi に渡しているコマンドとなる。

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
