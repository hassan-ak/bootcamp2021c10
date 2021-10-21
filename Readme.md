# bootcamp2021c10 - Integrate API Gateway and AppSync with Lambda and DynamoDB

## Integrate AppSync with Lambda as a Datasource 01

### Class Notes

SQL is query language for relational data bases. There are multiple data bases so in case if every data base uses its own language, it will be hard to use multiple data bases. So, SQL was made to work with multiple data bases. Sending get or post requests to API’s REST is the standard. Working with REST API’s we send get request to a URL and get the response which can be any thing such as JSON. Or we send a post request where we send some data along with the URL and get a response. GraphQL is becoming the new standard for working with API’s. The technology which AWS uses to implement GraphQL is AppSync.

[Introduction to GraphQL](https://graphql.org/learn/)

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

[Queries and Mutations](https://graphql.org/learn/queries/)

Queries run in parallel and used to get data which mutations run in sequence and used to modify data. In the most simple terms GraphQL is about asking specific fields on objects. Queries can have comments and as a response we can get strings or objects. A query where a string is returned as response is given in the above exapmle. See the follwoing example where string and object is returned as response (what a query will respond can be expected based on schema).

```
{
  hero {
    name
    # Queries can have comments!
    friends {
      name
    }
  }
}
```

```
{
  "data": {
    "hero": {
      "name": "R2-D2",
      "friends": [
        {
          "name": "Luke Skywalker"
        },
        {
          "name": "Han Solo"
        },
        {
          "name": "Leia Organa"
        }
      ]
    }
  }
}
```

In the queries we can have arguments on any field. In rest we can only pass a single set of arguments but in GraphQL every field can have its own argument. Arguments can be of any type (string, number, Boolean, enum).

```
{
  human(id: "1000") {
    name
    height(unit: FOOT)
  }
}
```

```
{
  "data": {
    "human": {
      "name": "Luke Skywalker",
      "height": 5.6430448
    }
  }
}
```

When working with the GraphQL queries if we need to use multiple arguments on a same field we can’t do it directly for this purpose aliases are used.

```
{
  empireHero: hero(episode: EMPIRE) {
    name
  }
  jediHero: hero(episode: JEDI) {
    name
  }
}
```

```
{
  "data": {
    "empireHero": {
      "name": "Luke Skywalker"
    },
    "jediHero": {
      "name": "R2-D2"
    }
  }
}
```

[Schemas and Types](https://graphql.org/learn/schema/)

QraphQL queries is about selecting fields on an object. In order to write these queries, we have typing system. Let have a look at a type definition here, "!" means that a filed cannot be null (will always get a response in return), while "[ ]" represents a list.

```
type Character {
  name: String!
  appearsIn: [Episode!]!
}
```

We can also specify arguments in the schema, let’s have a look at the following schema where arguments are provided for the length field with default value. Arguments can be required or optional and when these are optional, we need to define the default value.

```
type Starship {
  id: ID!
  name: String!
  length(unit: LengthUnit = METER): Float
}
```

We can define as many types as we want but two types are defined by GraphQL itself which defines the entry point of every query.

```
schema {
  query: Query
  mutation: Mutation
}
```

Every GraphQL service have a query (can only access data and run in parallel) and may or may not have a mutation (can update data so runs in sequence). Only the query type fields are of root type otherwise not. we can start our query with a root type but not with any other type.

An Interface is an abstract type that includes a certain set of fields that a type must include to implement the interface

```
interface Character {
  id: ID!
  name: String!
  friends: [Character]
  appearsIn: [Episode]!
}
```

### Reading Material

- [Start Learning - Introduction to GraphQL](https://graphql.org/learn/)
- [AppSync Lambda as data source](https://github.com/panacloud-modern-global-apps/full-stack-serverless-cdk/tree/main/step03_appsync_lambda_as_datasource)

### Class 10 Videos:

- [English YouTube](https://www.youtube.com/watch?v=m_lPimHUd4k&ab_channel=CertifiedUnicornDeveloper)
- [English Facebook](https://www.facebook.com/524892375/videos/1196774377471411/)
- [Urdu YouTube](https://www.youtube.com/watch?v=1-wOShkvThQ&ab_channel=CertifiedUnicornDeveloperinUrdu)
- [Urdu Facebook](https://www.facebook.com/100003743983275/videos/1009725069788588/)
