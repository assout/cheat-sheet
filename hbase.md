# HBase

Date: 2016-12-20 22:26
Tags: []
Categories: []

---

## REST API

- バージョン情報取得

        curl http://localhost:8080/version

- 利用可能なテーブル一覧取得

        curl http://localhost:8080

- テーブル作成例

        // format
        curl -v -X PUT 'http://localhost:8080/${format}/schema' -H "Accept: application/json" -H "Content-Type: application/json" -d '{"@name":"test","ColumnSchema":[{"name":"cf"}]}'
        // e.g.  (テーブル「test」 / カラムファミリ「cf」)
        curl -v -X PUT 'http://localhost:8080/test/schema' -H "Accept: application/json" -H "Content-Type: application/json" -d '{"@name":"test","ColumnSchema":[{"name":"cf"}]}'

- テーブル構造取得

        curl http://localhost:8080/test/schema

- データPUT例

        (テーブル「test」 / 行「row1」 / カラムファミリ：修飾子「cf：a」 / 値「value1」)
        ★Base64でエンコードして入れる
        ※行キーのエンコード例
        echo row1 | tr -d "\n" | base64
        cm93MQ==
        ※カラムキーのエンコード例
        echo cf:a | tr -d "\n" | base64
        Y2Y6YQ==
        ※値のエンコード例
        echo value1 | tr -d "\n" | base64
        dmFsdWUx

        curl -v -X PUT 'http://localhost:8080/test/row1/cf:a' -H "Accept: application/json" -H "Content-Type: application/json" -d "{\"Row\":[{\"key\":\"cm93MQ==\",\"Cell\":[{\"column\":\"Y2Y6YQ==\", \"$\":\"dmFsdWUx\"}]}]}"

- データ検索例

        (テーブル：test / 行：row1)
        curl -v -X GET 'http://localhost:8080/test/row1' -H "Accept: application/json"

- テーブル削除例

        (テーブル：test)
        curl -v -X DELETE 'http://localhost:8080/test/schema' -H "Accept: application/json"


