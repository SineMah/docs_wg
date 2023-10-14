- Elasticsearch ist keine traditionelle Datenbank
- [GitHub](https://github.com/orgs/elastic/repositories?type=all)
- Suche auf Basis von Lucene
- NoSQL (JSON)
- [Geschichte](https://www.elastic.co/de/about/history-of-elasticsearch)
- ELK Stack 
	- Elasticsearch
	- Kibana
	- Beats
	- Logstash
	- usw.
- [X-Pack](https://www.elastic.co/de/what-is/open-x-pack) Plugins 
- [Licence: Elastic License](https://www.elastic.co/de/licensing/elastic-license)
	- Änderung durch Amazon/AWS
- Derivate
	- OpenSearch
	- früher noch Opendistro von Amazon

## Generelle Grundeigenschaften
- Volltextsuche
- diverse andere Suchmechanismen
	- Geo
	- 2D (Geo Shape); Virtuelle Welten, CAD, usw.
	- more_like_this
	- wrapper
	- scripts (painless)
	- [boosting](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-boosting-query.html)
	- [NLP](https://www.elastic.co/guide/en/machine-learning/current/ml-nlp.html)
	- [ML](https://www.elastic.co/guide/en/machine-learning/current/ml-nlp-deploy-models.html)
- Echtzeit-Indexing
- Facettierte Suche
- Aggregationen
- RESTful API

## Überblick Search Engines
- Elasticsearch (Lucene)
- Manticore (C++)
- Zinc (Go)
- Apache Solr (Lucene)
- Meilisearch (Rust)

## Wieso Elasticsearch 
- einfache Konfiguration/Setup
- scalable
- Deep nested queries
- Rest API
- für Large Datasets geeigent
- für komplexe Daten geeigent
- Geo suche 
- Vektor DB
- Aggregations 
- easy to use #solrsucks
	- Eine Firma wirbt mit dem Slogan `Solr isn't for the weak` und bietet solr-Hosting an
	- Besser für statische Daten (Cache, uninverted index)
- usw. ...

## Kibana - DevTool
- Dashboards
- Monitoring
- Query Debugger 

## Queries
- Abfrage deklarativ (SQL ähnlich) oder programmatisch mit JSON nesting

### Deklarativ 
- X-Pack Feature
```sql
POST /_sql?format=txt
{
  "query": "SELECT * FROM library WHERE release_date < '2000-01-01'"
}
```

### Imperativer Ansatz
```json
POST _search
{
  "query": {
    "bool" : {
      "must" : {
        "term" : { "user.id" : "kimchy" }
      },
      "filter": {
        "term" : { "tags" : "production" }
      },
      "must_not" : {
        "range" : {
          "age" : { "gte" : 10, "lte" : 20 }
        }
      },
      "should" : [
        { "term" : { "tags" : "env1" } },
        { "term" : { "tags" : "deployed" } }
      ],
      "minimum_should_match" : 1,
      "boost" : 1.0
    }
  },
  "_source": false
}
```


- must
	- wie `and`
	- scoring
	- not cached
- should
	- wie `or`
- must_not
	- `and not`
	- no scoring
- filter
	- no scoring
	- cached
- boost
	- Multiplikator für Score
- score
	- umso höher der Score, umso relevanter ist das gefundene Dokument
	- https://www.elastic.co/guide/en/elasticsearch/guide/current/relevance-intro.html
	- [Berechnung](https://www.infoq.com/articles/similarity-scoring-elasticsearch/)

## Index
Ein Index enthält ein Datenschema und dazugehörige Daten. 
Er kann Replikas und Shards haben.
[Einstellungen](https://www.elastic.co/guide/en/elasticsearch/reference/current/indices-create-index.html#create-index-settings) können während des Erstellens angegeben werden
- verschiedene Status
	- grün
	- gelb
		- eine oder mehr replica shards im Cluster sind keiner Node zugehörig
	- rot 
		- Cluster-Probleme
		- keine primären Shards
[Node-Management](https://www.elastic.co/guide/en/elasticsearch/reference/current/modules-node.html)
Index-Daten werden lokal gesichert

## Mapping
Das Mapping repräsentiert Datenstruktur. Es beeinflusst die Suche direkt.
Das Mapping kann während der Indexerstellung als [Konfiguration](https://www.elastic.co/guide/en/elasticsearch/reference/current/indices-create-index.html#mappings) übergeben werden.
Elasticsearch erstellt während des Indexierens automatsich ein Mapping für bis dahin unbekannte Felder.

### Types
(Types)[https://www.elastic.co/guide/en/elasticsearch/reference/current/mapping-types.html]

### keyword vs text
(gängigste Fehler)

- keyword
	- strukturierter Inhalt
	- Aggregations möglich
	- Sortierung
	- term-Queries

- text
	- Volltextinhalte wie Mail-Inhalte oder Produktbeschreibungen
	- werden mit [analyzer](https://www.elastic.co/guide/en/elasticsearch/reference/current/analysis.html) in eine Liste aus Terms umgeformt bevor indexiert wird

### Beispiel
```
GET index_or_alias_name/_mapping
```

```json
{
  "index_or_alias_name": {
    "mappings": {
      "properties": {
        "Abilities": {
          "type": "nested",
          "properties": {
            "IsHidden": {
              "type": "boolean"
            },
            "Name": {
              "type": "keyword"
            },
            "Slot": {
              "type": "long"
            }
          }
        },
        "Attributes": {
          "properties": {
            "Attack": {
              "type": "integer"
            },
            "Defense": {
              "type": "integer"
            },
            "HP": {
              "type": "integer"
            },
            "SpecialAttack": {
              "type": "integer"
            },
            "SpecialDefense": {
              "type": "integer"
            },
            "Speed": {
              "type": "integer"
            }
          }
        },
        "Games": {
          "type": "keyword"
        },
        "Height": {
          "type": "long"
        },
        "ID": {
          "type": "integer"
        },
        "Images": {
          "type": "text",
          "fields": {
            "keyword": {
              "type": "keyword",
              "ignore_above": 256
            }
          }
        },
        "Moves": {
          "type": "text",
          "fields": {
            "keyword": {
              "type": "keyword",
              "ignore_above": 256
            }
          }
        },
        "Name": {
          "type": "keyword"
        },
        "Species": {
          "type": "text",
          "fields": {
            "keyword": {
              "type": "keyword",
              "ignore_above": 256
            }
          }
        },
        "Type": {
          "type": "keyword"
        },
        "Weight": {
          "type": "long"
        }
      }
    }
  }
}
```


## [Painless](https://www.elastic.co/guide/en/elasticsearch/reference/master/modules-scripting-painless.html) (Erweiterbarkeit)
Skriptsprache für und von Elasticsearch

Anwendungsbeispiele sind zum Beispiel  Entfernungsberechnungen zwischen zwei Geo-Punkten und Anreicherung der Payload (source) 

```json
GET my-index-000001/_search
{
  "script_fields": {
    "my_doubled_field": {
      "script": {
        "source": "doc['my_field'].value * params['multiplier']",
        "params": {
          "multiplier": 2
        }
      }
    }
  }
}
```


[[Places]]