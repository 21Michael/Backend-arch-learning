# GraphQL

**GraphQL** is a query language and server-side runtime for application programming 
interfaces (APIs) that prioritizes giving clients exactly the data they request and no
more. It has a server-side runtime fulfilling those queries along with the data. In other words,
GraphQL follows WYAIWYG pattern What You Ask Is What You Get. GraphQL allows declarative data 
fetching where a client can specify what data it needs from an API.

GraphQL is designed to make APIs fast, flexible, and developer-friendly. It can even
be deployed within an integrated development environment (IDE) known as GraphiQL. As 
an alternative to REST, GraphQL lets developers construct requests that pull data from
multiple data sources in a single API call.

![link](https://content.altexsoft.com/media/2020/05/word-image-60.png)

GraphQL starts with building a schema, which is a description of all the queries you 
can possibly make in a GraphQL API and all the types that they return. Schema-building
is hard as it requires strong typing in the Schema Definition Language (SDL).

Having the schema before querying, a client can validate their query against making 
sure the server will be able to respond to it. On reaching the backend application, 
a GraphQL operation is interpreted against the entire schema, and resolved with data
for the frontend application. Sending one massive query to the server, the API returns
a JSON response with exactly the shape of the data we asked for.

![link](https://lighthouse-php.com/assets/img/flow.f9dcf86d.png)

## Components:

### Schema & Types: 
**Schema:** API developers use GraphQL to create a schema to describe all the possible data 
that clients can query through that service. A GraphQL schema is made up of object types, which define which kind of object you
can request and what fields it has. 

**Types:** Types are the most important concepts of GraphQL. It is a custom object and depicts 
how your API will look. Types have fields and these fields return a specific data type. In our 
example, Movie and Actor are two different types that contains fields for querying like name, 
age, genre and returns a type of data as Int, String, ID, List and a few more. The exclamation
mark denotes that the field is mandatory or non-nullable.

```graphql
  type Actor {
     id:String!
     name:String!
     age:Int
     movies:Movie
  }

  type Movie {
     id:String
     name:String!
     genre:String
     actor:Actor
  }
```

### Queries: 
**Query:** In simple terms, queries are ways to get data from the server. No more over or under
fetching, you get what exactly you ask. It is a read-only fetch operation. In the REST world, 
queries are equivalent to how you’d use Request with a payload to get a response from the server.
```graphql
  type Query {
     movie(id: ID): Movie
     actor(id: ID): Actor
     movies:[Movie]
     actors: [Actor]
  }
```

### Mutation: 
**Mutation:** The way you are going to modify data on the server. The mutations are equivalent
to how you’d use the CRUD operation along with Verbs such as GET, POST, PUT, PATCH and DELETE 
in the REST world. In GraphQL it will always be a POST call. It is a write followed by fetch 
operation.
```graphql
  type Mutation {
     addMovie(id: String!, name: String!, genre: String): Movie
     addActor(name: String!, age: Int!): Actor
  }
```

### Resolvers:
**Resolvers:** A collection of functions that generate a response for a GraphQL query. There is
a protocol to follow like, the function name will have the same name as the Query type. In a 
nutshell, the Resolvers act as a GraphQL query handler.
```js
   movie: {
     type: MovieType,
     args: { id: { type: GraphQLID } },
     resolve(parent, args) {
        return Movie.findById(args.id);
     },
   }
```

### Subscriptions:
Like queries, subscriptions enable you to fetch data. Unlike queries, subscriptions are 
long-lasting operations that can change their result over time. They can maintain an active 
connection to your GraphQL server (most commonly via WebSocket), enabling the server to push 
updates to the subscription's result.
```graphql
subscription {    
    movies {    
        id    
        name    
        genre    
        actor{
           name
        }    
    }
}
```

![link](https://miro.medium.com/max/628/1*DOjFWMhLFKYa7yEbYOAzFA.png)

## REST vs GraphQL:
  - **Data Fetching:** Data fetching is one of the most significant improvements in GraphQL when 
    compared to REST. GrpahQL is a query language, and your query (request) when triggered it
    precisely responds with the expected data, no extra information gets retrieved. Whereas, 
    with a REST API, you’d usually retrieve the necessary information by accessing multiple 
    endpoints. In other words, no more over and under fetching of data. GraphQL gives you 
    precise data.
    
    ![link](https://blog.testproject.io/wp-content/uploads/2020/05/Screenshot-2020-06-01-at-10.42.35-PM.png)
  
  - **Data Operation:** In REST API, each resource is represented with an endpoint, and it’s 
    apparent to end up having multiple endpoints. The data fetch done using the CRUD (Create, 
    Read, Update and Delete) operation via multiple endpoints. Whereas, In GraphQL, everything 
    perceived as a graph and it’s connected and represented as a single endpoint. It also has 
    unique features like Query, Mutation and Subscription.
    
    ![link](https://blog.testproject.io/wp-content/uploads/2020/05/RestVsGraphQL-pic-768x438.png)
    
  - **Versioning:** In REST API, it is prevalent to see APIs have a different version like v1, 
    v2 and so on. In GraphQL, there’s no need since it is based on Schema and users can quickly 
    mark those types as deprecation for the fields that are no longer needed. This also saves a
    huge time in back and forth testing on different versions of the same API.
    
![link](https://www.partech.nl/publication-image/%7B8405BF1E-4EE8-46F4-A80A-D2393D03CFBB%7D)

## Conclusion:

### GraphQL pros:
  - **Typed schema.** GraphQL publishes in advance what it can do, which improves its 
    discoverability. By pointing a client at the GraphQL API, we can find out what queries 
    are available.
  - **Graph-like data in one request by one endpoint.** Data that goes far into linked relations but not good 
    for flat data.
  - **No versioning.** The best practice with versioning is not to version the API at all.
  - **Detailed error messages.** In a similar fashion to SOAP, GraphQL provides details to 
    errors that occurred. Its error message includes all the resolvers and refers to the exact 
    query part at fault.
  - **Flexible permissions.** GraphQL allows for selectively exposing certain functions while 
    preserving private information. Meanwhile, REST architecture doesn’t reveal data in portions.
    It’s either all or nothing.    
    
### GraphQL cons:
  - **Performance issues.** GraphQL trades off complexity for its power. Having too many nested
    fields in one request can lead to system overload. So, REST remains a better option for 
    complex queries.
  - **HTTP Caching complexity.** As GraphQL isn’t reusing HTTP caching semantics, it requires a 
    custom caching effort.
  - **A lot of pre-development education.** Not having enough time to figure out GraphQL niche 
    operations and SDL, many projects decide to follow the well-known path of REST.
    