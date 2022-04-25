# STAC FastAPI Elasticsearch

Elasticsearch backend for stac-fastapi. 

**WIP** This backend does not have any production deployments yet, so use the pgstac backend instead if that's what you need.

For changes, see the [Changelog](CHANGELOG.md).

## Development Environment Setup

To install the classes in your local Python env, run:

```shell
pip install -e 'stac_fastapi/elasticsearch[dev]'
```

### Pre-commit

Install [pre-commit](https://pre-commit.com/#install).

Prior to commit, run:

```shell
pre-commit run --all-files`
```


## Building

```shell
docker-compose build
```

## Running API on localhost:8080

```shell
docker-compose up
```

By default, docker-compose uses Elasticsearch 7.x. If you wish to use a different version, put the following in a 
file named `.env` in the same directory you run docker-compose from:

```shell
ELASTICSEARCH_VERSION=7.12.0
```

### Generate a keystore and cert

```shell
docker-compose -f docker-compose.setup.yml run --rm keystore
docker-compose -f docker-compose.setup.yml run --rm certs
```



To create a new Collection:

```shell
curl -X "POST" "http://localhost:8080/collections" \
     -H 'Content-Type: application/json; charset=utf-8' \
     -d $'{
  "id": "my_collection"
}'
```

Note: this "Collections Transaction" behavior is not part of the STAC API, but may be soon.

## Testing

```shell
make test
```

## Ingest sample data

```shell
make ingest
```

## Elasticsearch Mappings

Mappings apply to search index, not source. 
