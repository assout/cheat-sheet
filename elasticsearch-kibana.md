# Elasticsearch Kibana

Date: 2016-10-27 00:21
Tags: []
Categories: []

---

## Using docker

[nshou/elasticsearch-kibana - Docker Hub](https://hub.docker.com/r/nshou/elasticsearch-kibana/)

- Elasticsearch by <http://localhost:9200>
- Kibana front-end by <http://localhost:5601>

## Elasticsearch

- インデックスの追加

        curl -XPOST http://localhost:9200/${indexName}

- インデックス一覧の取得

        curl -XGET localhost:9200/_aliases?pretty

- インデックスのマッピング一覧の取得

        curl -XGET localhost:9200/_mapping?pretty

- データのPUT例

        # format
        curl -XPUT http://localhost:9200/${indexName}/${typeName}/${documentId} -d '{"timestamp": "10/May/2016:09:00:00 +0000", "value":"hoge", "number": "123"}'
        # e.g.
        curl -XPUT http://localhost:9200/foo/bar/baz -d '{"timestamp": "10/May/2016:09:00:00 +0000", "value":"hoge", "number": "123"}'

- データのGET例

        curl -XGET http://localhost:9200/sample_index/sample_type/1

- データの一覧GET

        curl -XGET http://localhost:9200/sample_index/sample_type/_search?pretty

- データの全削除

        curl -XDELETE 'http://localhost:9200/*'

- クラスの状態確認

        curl -XGET http://localhost:9200/_cluster/state?pretty

