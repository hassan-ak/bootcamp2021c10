# bootcamp2021c10 - Integrate API Gateway and AppSync with Lambda and DynamoDB

## Integrate AppSync with Lambda as a Datasource

### Class Notes

SQL is query language for relational data bases. There are multiple data bases so in case if every data base uses its own language, it will be hard to use multiple data bases. So, SQL was made to work with multiple data bases. Sending get or post requests to API’s REST is the standard. Working with REST API’s we send get request to a URL and get the response which can be any thing such as JSON. Or we send a post request where we send some data along with the URL and get a response. GraphQL is becoming the new standard for working with API’s. The technology which AWS uses to implement GraphQL is AppSync.

[Start Learning - Introduction to GraphQL](https://graphql.org/learn/)

GraphQL is query language for the API’s and it is also runtime on the server side (in our case it is AppSync). It uses databases but not linked to a particular one. There are libraries for GraphQL on the client side such as apollo.
In GraphQL we define schema (like table definations) which is actually defining types and then fields on those types and then we provide functions for each field on each type. Types are defined as follows

```
type Query {
  me: User
}

type User {
  id: ID
  name: String
}
```

And functions for the types

```
function Query_me(request) {
  return request.auth.user;
}

function User_name(user) {
  return user.getName();
}
```

In SQL we define tables while in GraphQL we define types where Query is a special type which is root of all types. We start our query from the Query type.
When a GraphQL service is running it can get a query and validated the query based on types after validation it runs the function and gives the response. A GraphQL query can be of following type

```
{
  me {
    name
  }
}
```

Which can result in the following response

```
{
  "me": {
    "name": "Luke Skywalker"
  }
}
```

Working with GraphQL queries gives us an advantage that both the queries and response are of same structure.

[Start Learning - Queries and Mutations](https://graphql.org/learn/queries/)

Queries run in parallel and used to get data which mutations run in sequence and used to modify data. Have a look at a query and its response

```
{
  hero {
    name
  }
}
```

```
{
  "data": {
    "hero": {
      "name": "R2-D2"
    }
  }
}
```
