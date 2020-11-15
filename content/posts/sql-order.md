---
title: "SQLの４大命令について"
description: "SQL, language to control DB"
date: 2020-03-27
aliases: ["/posts/sql-order/"]
---

SQLとはデータベース言語であり、データベースを管理するソフトウェアを操作・制御することが目的です。
<!--more-->
# SQLとは
データベースというのは、集めたデータをプログラムによって整理し、操作できるようにしたものです。データベース言語はデータを管理して、ユーザーが指定した条件に合致するものを見つけ出すためのものです。

# SQLの種類
SQLは、大きく分けて以下の3種類の言語から構成されています。

- データ定義言語(CREATE,DROP,ALTER等)
- データ操作言語(INSERT,UPDATE,DELETE,SELECT)
- データ制御言語(GRANT,REVOKE,SET TRANSACTION,BEGIN,COMMIT,ROLLBACK,SAVEPOINT,LOCK)

今回はデータ操作言語に該当するSQLの４大命令についてまとめてみました。

# SQLの４大命令とは

SQLの４大命令とは以下の４種類です。

| 命令       |      説明 |    文法    |
|:-----------------|------------------:|:------------------:|
| INSERT             |              データを追加する |        INSERT INTO テーブル名 (カラム名1, カラム名2, ...) VALUES (値1, 値2, ...);        |
| SELECT           |            データを取得する |       SELECT カラム名1, カラム名2, ... FROM テーブル名 [WHERE 絞込条件];
       |
| UPGRADE             |              データを更新する |        UPDATE テーブル名 SET カラム名1=値1 [, カラム名2=値2 ...] [WHERE 絞込条件];        |
| DELETE               |                データを削除する |         DELETE FROM テーブル名 [WHERE 絞込条件];
         |


# INSERT
テーブルにデータを追加する

```sql
INSERT INTO "テーブル名" ("列名1", "列名2", "列名3", ...) VALUES ("値1", "値2", )
```

# SELECT
テーブルからデータを取得する

```sql
SELECT "列名"... FROM "テーブル名" (WHERE "条件式")
```

# UPGRADE
テーブルにデータを追加する

```sql
UPDATE "テーブル名" SET "列名=値1", "列名2=値2", ... (WHERE "条件式")
```

※注:WHEREのないUPDATEは全レコードが更新される。

# DELETE
テーブルのデータを削除する

```sql
DELETE FROM "テーブル名" (WHERE "条件式")
```

※注:WHEREのないDELETEは全レコードが消去される。
