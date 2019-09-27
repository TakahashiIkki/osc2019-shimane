# ハンズオン内容

以下のような事を予定しています。

- DockerでPostgreSQLを立ち上げてみよう。
- PostgreSQL に dump ファイルをリストアしてみよう。
- テーブルにインデックスを貼ってSQLの高速化をしてみよう。
- Explainを使って何がどう変わったのか、みてみよう。

## ０．前準備

### git, docker をインストール

### この git レポジトリのCloneをする。

- terminal を立ち上げましょう。

```
cd ~
git clone https://github.com/TakahashiIkki/osc2019-shimane.git
cd osc2019-shimane
```

これで前準備 は終了です！

## １． Dodkerで PostgreSQL を立ち上げてみよう

docker のコマンドを実行して PostgreSQLを起動してみましょう！！

```
docker-compose up --build -d
```

成功すると 以下のようなメッセージが表示されます。

**Successfully tagged osc2019-shimane_postgres:latest**
**Creating osc_pgsql ... done**

--- 

※ docker, docker-compose が Vagrant と何が違うの？ みたいな方はこちらをぜひともご参照ください！

https://speakerdeck.com/soudai/vagrant-to-docker

--- 

dockerのコンテナが動いてる事を確認してみましょう！

```
docker-compose ps -a
```

**実行結果**

正常に動いていれば 以下のような表示がされます。

```
  Name                 Command              State           Ports         
--------------------------------------------------------------------------
osc_pgsql   docker-entrypoint.sh postgres   Up      0.0.0.0:5434->5432/tcp
```

それでは、 Dockerで起動しているコンテナの中に入って確認してみましょう！

以下のコマンドを入力してみてください。

```
docker-compose exec postgres bash
```

**実行結果**

正常に動いていれば 以下のような表示がされます。

```
root@58da2a0c083e:/opt/postgres# 
```


### デフォルトのデータベースを確認する。

**Dockerコンテナ上で動かす**

```
root@58da2a0c083e:/opt/postgres# psql -h localhost -U osc_user osc_demo

psql (11.5 (Debian 11.5-1.pgdg90+1))
Type "help" for help.

osc_demo=# \l
                             List of databases
   Name    |  Owner   | Encoding | Collate | Ctype |   Access privileges   
-----------+----------+----------+---------+-------+-----------------------
 osc_demo  | osc_user | UTF8     | C       | C     | 
 postgres  | osc_user | UTF8     | C       | C     | 
 template0 | osc_user | UTF8     | C       | C     | =c/osc_user          +
           |          |          |         |       | osc_user=CTc/osc_user
 template1 | osc_user | UTF8     | C       | C     | =c/osc_user          +
           |          |          |         |       | osc_user=CTc/osc_user
(4 rows)
```