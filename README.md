# This is a demo for [Moqui GraphQl](https://github.com/shendepu/moqui-graphql) 

This demo depends on:
- [Moqui Framework](https://github.com/moqui/moqui-framework)
- [Moqui Runtime](https://github.com/moqui/moqui-runtime)
- [Moqui GraphQL](https://github.com/shendepu/moqui-graphql)
 
## tl;dr

```sh
git clone https://github.com/moqui/moqui-framework

cd moqui-framework
./gradlew getRuntime

git clone https://github.com/shendepu/moqui-graphql ./runtime/component/moqui-graphql
git clone https://github.com/shendepu/moqui-graphql-demo ./runtime/component/mqoui-graphql-demo
 
./gradlew run 
```

First open http://localhost:8080 and login with john.deo test account

then open [http://localhost:8080/graphql/GraphiQL](http://localhost:8080/graphql/GraphiQL)

#### Note: It seems safari has issue to show variable panel of GraphiQL. Chrome and firefox are fine. 

input 
```graphql
query QueryType($showUsers: Boolean!) {
  moqui {
    artifacts {
      hitSummary (pagination:{ pageSize: 1 }) {
        edges {
          node {
            artifactType
            artifactSubType
          }
        }
      }
    }
    users (pagination: {pageSize: 2}) @include(if: $showUsers) {
      edges {
        node {
          userId 
          username
          emailAddress
        }
      }
    }
    user(userId: "EX_JOHN_DOE") {
      userId
      username
      userFullName
    }

    entity {
      syncs {
        edges {
          node {
          	entitySyncId
          }
        }
      }
    }
    basic {
      geos (pagination: {pageSize: 4 }) {
        edges {
          node {
            geoId
            geoName
          }
        }
        pageInfo {
          totalCount
        }
      }
    }
  }
}
```
also add query variables
```json
{
  "showUsers": true
}
```

You may try modifying the query to see different result  

## Snapshot

![GraphiQL](graphiql-snapshot.png)

