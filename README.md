# Elastic Search キャッチアップ

## Kibana
http://localhost:5601/

### コンソール
http://localhost:5601/app/kibana#/dev_tools/console

## クラスタのヘルスチェック
クラスタ全体の状態をチェックできる。
`green` なら正常。

```
GET /_cat/health?v
```

## ノードリストの取得
```
GET /_cat/nodes?v
```

## 全インデックスのリスト取得
```
GET /_cat/indices?v
```

## インデックスの作成

```
PUT /customer?pretty    # 作成
GET /_cat/indices?v　　　# 確認
```
yellow でもおk
> customerインデックスにyellowステータスがタグ付けされていることにも気づくと思います。yellowは一部のレプリカが割り当てられていないことを示しているという前の説明を思い出してください。このインデックスでこのステータスが生じたのは、Elasticsearchがデフォルトでこのインデックスのレプリカを1つ作成したためです。今のところ1つのノードしか稼働していないため、別のノードがクラスタに参加するまで、その1つのレプリカは（高可用性用に）割り当てられません。そのレプリカが2番目のノードに割り当てられると、このインデックスのヘルスステータスはgreenに変わります。

## ドキュメントのインデキシング
ドキュメントをインデキシングするときは、インデックスを明示的に作成する必要はない。

```
# インデックスの作成とドキュメントのインデキシング
PUT /customer/_doc/1?pretty
{
  "name": "John Doe"
}

# ドキュメントの取得
GET /customer/_doc/1?pretty
```

## インデックスの削除

```
# 削除
DELETE /customer?pretty

# 確認
GET /_cat/indices?v
```

## まとめると
下記のように利用できる.

```
REST動詞 /index/type/id
```