# PostgreSQL

Date: 2016-08-01 14:23
Tags:[]
Categories:[]

---

## Commands

- 接続

        psql -h hostname -U username -d databasename

    - ポート指定

            psql -h hostname -U username -d databasename -p 32768

- テーブル一覧参照

        \d

- テーブル定義参照

        \d table_name

- SQL（スクリプト）ファイルの実行

        \i SQLファイル名

- psql切断

        \q

- エディタでSQL編集

        \e

- 拡張表示

        \x

- セッションを確認

        SELECT * FROM pg_stat_activity;

- セッションをすべて切断

        SELECT pg_terminate_backend(pid) FROM pg_stat_activity WHERE datname = 'DB名' AND pid <> pg_backend_pid();

- ダンプ取得

        pg_dump -U ${user} ${db} > ${output}

