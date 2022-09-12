# Datadog Ariadne GraphQL Server

Includes the GraphQL operation name in the datadog APM resource name if one is present.

e.g.
```graphql
query FindProductByIdWithUsers {
  productById(id: 1) {
    name
    users {
      name
    }
  }
}
```

The APM resource name will be changed from`POST /graphql` to `POST /graphql?operationName=FindProductByIdWithUsers`.

## Usage

Use this server in place of `ariadne.asgi import GraphQL`

```python3
from datadog_ariadne_graphql_server.asgi import GraphQL

def configure_graphql(component: FastAPI) -> None:
    component.add_route(
        "/graphql", GraphQL(schema=schema, extensions=[OpenTracingExtension])
    )
```