# _GraphQL_

- https://graphql.org/
- https://facebook.github.io/graphql/
- https://devhints.io/graphql
- https://graphqleditor.com/
- https://apis.guru/graphql-voyager/
- GraphQL is a Query Language for APIs and a runtime for fulfilling those queries with your existing data
- GraphQL is a query language for your API, and a server-side runtime for executing queries by using a type system you define for your data

---

# _Overview_

- A GraphQL service is created by defining types and fields on those types, then providing functions for each field on each type
- For example, a GraphQL service that tells us who the logged in user is (`me`), as well as that user's name might look something like this:

```
type Query {
  me: User
}

type User {
  id: ID
  name: String
}
```

- Along with functions for each field on each type:

```
function Query_me(request) {
  return request.auth.user;
}

function User_name(user) {
  return user.getName();
}
```

- Once a GraphQL service is running (typically at a URL on a web service), it can be sent GraphQL queries to validate and execute
- A received query is first checked to ensure it only refers to the types and fields defined, then runs the provided functions to produce a result
- For example the query:

```
{
  me {
    name
  }
}
```

- Could produce the JSON result:

```
{
  "me": {
    "name": "Luke Skywalker"
  }
}
```

---

# _Queries and Mutations_

## Fields

- At its simplest, GraphQL is about asking for specific fields on objects. Let's start by looking at a very simple query and the result we get when we run it:

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

- The query has exactly the same shape as the result
- Queries can traverse related objects and their fields, letting clients fetch lots of related data in one request

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

## Arguments

- The ability to pass arguments to fields

```
{
  human(id: "1000") {
    name
    height
  }
}
```

```
{
  "data": {
    "human": {
      "name": "Luke Skywalker",
      "height": 1.72
    }
  }
}
```

- Every field and nested object can get its own set of arguments
- Can pass arguments into scalar fields, to implement data transformations once on the server, instead of on every client separately

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

- Arguments can be of many different types

## Aliases

- You may have noticed that, since the result object fields match the name of the field in the query but don't include arguments, you can't directly query for the same field with different arguments
- Aliases let you rename the result of a field to anything you want
- Allows you to include multiple fields in one request

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

- In the above example, the two `hero` fields would have conflicted, but since we can alias them to different names, we can get both results in one request

## Fragments

- Reusable units
- A a collection of fields on a specific type
- Let you construct sets of fields, and then include them in queries where you need to
- Let's say we had a relatively complicated page in our app, which let us look at two heroes side by side, along with their friends
- We would need to repeat the fields at least once - one for each side of the comparison
- Using fragments:

```
{
  leftComparison: hero(episode: EMPIRE) {
    ...comparisonFields
  }
  rightComparison: hero(episode: JEDI) {
    ...comparisonFields
  }
}

fragment comparisonFields on Character {
  name
  appearsIn
  friends {
    name
  }
}
```

```
{
  "data": {
    "leftComparison": {
      "name": "Luke Skywalker",
      "appearsIn": [
        "NEWHOPE",
        "EMPIRE",
        "JEDI"
      ],
      "friends": [
        {
          "name": "Han Solo"
        },
        {
          "name": "Leia Organa"
        },
        {
          "name": "C-3PO"
        },
        {
          "name": "R2-D2"
        }
      ]
    },
    "rightComparison": {
      "name": "R2-D2",
      "appearsIn": [
        "NEWHOPE",
        "EMPIRE",
        "JEDI"
      ],
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

- Frequently used to split complicated application data requirements into smaller chunks
- Especially when you need to combine lots of UI components with different fragments into one initial data fetch

## Operation Name

- Up until now, we have been using a shorthand syntax where we omit both the `query` keyword and the query name, but in production apps it's useful to use these to make our code less ambiguous
- Here’s an example that includes the keyword `query` as operation type and `HeroNameAndFriends` as operation name:

```
query HeroNameAndFriends {
  hero {
    name
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

- The operation type is either `query`, `mutation`, or `subscription`
- It describes what type of operation you're intending to do
- The operation name is a meaningful and explicit name for your operation
- It is only required in multi-operation documents
- Its use is encouraged because it is very helpful for debugging and server-side logging

## Variables

- A first-class way to factor dynamic values out of the query, and pass them as a separate dictionary
- When we start working with variables, we need to do three things:

  1. Replace the static value in the query with `$variableName`
  2. Declare `$variableName` as one of the variables accepted by the query
  3. Pass `variableName: value` in the separate, transport-specific (usually JSON) variables dictionary

```
// variables
{
  "episode": "JEDI"
}
```

```
query HeroNameAndFriends($episode: Episode) {
  hero(episode: $episode) {
    name
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

- In our client code, we can simply pass a different variable rather than needing to construct an entirely new query
- The variable definitions are the part that looks like `($episode: Episode)` in the query above
  - It works just like the argument definitions for a function in a typed language
  - It lists all of the variables, prefixed by `$`, followed by their type, in this case `Episode`
  - Can be optional or required
    - Since there isn't an `!` next to the `Episode` type, it's optional
  - Must be either scalars, enums, or input object types
    - So, if you want to pass a complex object into a field, you need to know what input type that matches on the server
- Default values can also be assigned to the variables in the query by adding the default value after the type declaration

```
query HeroNameAndFriends($episode: Episode = JEDI) {
  hero(episode: $episode) {
    name
    friends {
      name
    }
  }
}
```

## Directives

- We might need a way to dynamically change the structure and shape of our queries using variables
- For example, we can imagine a UI component that has a summarized and detailed view, where one includes more fields than the other

```
query Hero($episode: Episode, $withFriends: Boolean!) {
  hero(episode: $episode) {
    name
    friends @include(if: $withFriends) {
      name
    }
  }
}
```

```
{
  "episode": "JEDI",
  "withFriends": false
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

- A directive can be attached to a field or fragment inclusion, and can affect execution of the query in any way the server desires
- The GraphQL spec includes two directives
  - `@include(if: Boolean)`
    - Only include this field in the result if the argument is `true`
  - `@skip(if: Boolean)`
    - Skip this field if the argument is `true`
  - `@skip` always has higher precedence than `@include`

```
query ExampleQuery ($isCat: Boolean) {
  pet {
    numberLitterBoxes @include(if: $isCat)
    numberDogHouses @skip(if: $isCat)
  }
}
```

## Mutations

- A way to modify server-side data
- A convention that any operations that cause writes should be sent explicitly via a mutation
- Just like in queries, if the mutation field returns an object type, you can ask for nested fields
  - This can be useful for fetching the new state of an object after an update

```
mutation CreateReviewForEpisode($ep: Episode!, $review: ReviewInput!) {
  createReview(episode: $ep, review: $review) {
    stars
    commentary
  }
}
```

```
{
  "ep": "JEDI",
  "review": {
    "stars": 5,
    "commentary": "This is a great movie!"
  }
}
```

```
{
  "data": {
    "createReview": {
      "stars": 5,
      "commentary": "This is a great movie!"
    }
  }
}
```

- `createReview` field returns the `stars` and `commentary` fields of the newly created review
- While query fields are executed in parallel, mutation fields run in series, one after the other
  - If we send two `incrementCredits` mutations in one request, the first is guaranteed to finish before the second begins

## Inline Fragments

- GraphQL schemas include the ability to define interfaces and union types
- If you are querying a field that returns an interface or a union type, you will need to use inline fragments to access data on the underlying concrete type

```
query HeroForEpisode($ep: Episode!) {
  hero(episode: $ep) {
    name
    ... on Droid {
      primaryFunction
    }
    ... on Human {
      height
    }
  }
}
```

```
{
  "ep": "JEDI"
}
```

```
{
  "data": {
    "hero": {
      "name": "R2-D2",
      "primaryFunction": "Astromech"
    }
  }
}
```

- The `hero` field returns the type `Character`, which might be either a `Human` or a `Droid` depending on the `episode` argument
- In the direct selection, you can only ask for fields that exist on the `Character` interface, such as `name`
- To ask for a field on the concrete type, you need to use an inline fragment with a type condition
- Because the first fragment is labeled as `... on Droid`, the `primaryFunction` field will only be executed if the `Character` returned from `hero` is of the `Droid` type
- Similarly for the `height` field for the `Human` type
- Named fragments can also be used in the same way, since a named fragment always has a type attached

## Meta fields

- Given that there are some situations where you don't know what type you'll get back from the GraphQL service, you need some way to determine how to handle that data on the client
- GraphQL allows you to request `__typename`, a meta field, at any point in a query to get the name of the object type at that point

```
{
  search(text: "an") {
    __typename
    ... on Human {
      name
    }
    ... on Droid {
      name
    }
    ... on Starship {
      name
    }
  }
}
```

```
{
  "data": {
    "search": [
      {
        "__typename": "Human",
        "name": "Han Solo"
      },
      {
        "__typename": "Human",
        "name": "Leia Organa"
      },
      {
        "__typename": "Starship",
        "name": "TIE Advanced x1"
      }
    ]
  }
}
```

- In the above query, `search` returns a union type that can be one of three options
- It would be impossible to tell apart the different types from the client without the `__typename` field

---

# _Subscriptions_

- In addition to fetching data using queries and modifying data using mutations, the GraphQL spec supports a third operation type, called `subscription`
- Subscriptions are a GraphQL operation allowing the server to send data to its clients when a specific event happens
- Subscriptions are usually implemented with WebSockets, where the server holds a steady connection to the client
- This means when working with subscriptions, you’re breaking the Request-Response-Cycle that was used for all previous interactions with the API
- The client now initiates a steady connection with the server by specifying which event it is interested in
- Every time this particular event then happens, the server uses the connection to push the expected data to the client
- Just as a client can tell the server what data to refetch after it performs a mutation with a GraphQL selection, the client can tell the server what data it wants to be pushed with the subscription with a GraphQL selection
- A way to push data from the server to the clients that choose to listen to real time messages from the server
- Similar to queries in that they specify a set of fields to be delivered to the client, but instead of immediately returning a single answer, a result is sent every time a particular event happens on the server
- A common use case for subscriptions is notifying the client side about particular events, for example the creation of a new object, updated fields and so on

```
subscription StoryLikeSubscription($input: StoryLikeSubscribeInput) {
  storyLikeSubscribe(input: $input) {
    story {
      likers { count }
      likeSentence { text }
    }
  }
}
```

---

# _Schemas and Types_

## Type system

- Describes what data can be queried
- The GraphQL query language is basically about selecting fields on objects

1. We start with a special "root" object
2. We select the `hero` field on that
3. For the object returned by `hero`, we select the `name` and `appearsIn` fields

```
{
  hero {
    name
    appearsIn
  }
}
```

```
{
  "data": {
    "hero": {
      "name": "R2-D2",
      "appearsIn": [
        "NEWHOPE",
        "EMPIRE",
        "JEDI"
      ]
    }
  }
}
```

- Because the shape of a GraphQL query closely matches the result, you can predict what the query will return without knowing that much about the server
- But it's useful to have an exact description of the data we can ask for
  - What fields can we select?
  - What kinds of objects might they return?
  - What fields are available on those sub-objects?
- That's where the schema comes in
- Every GraphQL service defines a set of types which completely describe the set of possible data you can query on that service
- Then, when queries come in, they are validated and executed against that schema

## Type language

- GraphQL services can be written in any language
- We'll use the "GraphQL schema language"
- It's similar to the query language, and allows us to talk about GraphQL schemas in a language-agnostic way

## Object types and fields

- The most basic components of a GraphQL schema are object types
  - Represents a kind of object you can fetch from your service
  - And what fields it has

```
type Character {
  name: String!
  appearsIn: [Episode!]!
}
```

- What's what:
  - `Character`
    - A GraphQL Object Type, meaning it's a type with some fields
    - Most of the types in your schema will be object types
  - `name` and `appearsIn`
    - Fields on the `Character` type
    - That means that `name` and `appearsIn` are the only fields that can appear in any part of a GraphQL query that operates on the `Character` type
  - `String`
    - One of the built-in scalar types
    - These are types that resolve to a single scalar object, and can't have sub-selections in the query
  - `String!`
    - Means that the field is non-nullable, meaning that the GraphQL service promises to always give you a value when you query this field
    - In the type language, we'll represent those with an exclamation mark
  - `[Episode!]!`
    - Represents an array of `Episode` objects
    - Since it is also non-nullable, you can always expect an array (with zero or more items) when you query the `appearsIn` field
    - And since `Episode!` is also non-nullable, you can always expect every item of the array to be an `Episode` object

## Arguments

- Every field on a GraphQL object type can have zero or more arguments

```
type Starship {
  id: ID!
  name: String!
  length(unit: LengthUnit = METER): Float
}
```

- All arguments are named
- All arguments in GraphQL are passed by name specifically
- In this case, the `length` field has one defined argument, `unit`
- Arguments can be either required or optional
  - When an argument is optional, we can define a default value
  - If the `unit` argument is not passed, it will be set to `METER` by default

## Query and Mutation types

- Most types in your schema will just be normal object types
- But there are two types that are special within a schema

```
schema {
  query: Query
  mutation: Mutation
}
```

- Every GraphQL service has a `query` type and may or may not have a `mutation` type
- These types are the same as a regular object type, but they are special because they define the entry point of every GraphQL query
- If you see a query that looks like:

```
query {
  hero {
    name
  }
  droid(id: "2000") {
    name
  }
}
```

```
{
  "data": {
    "hero": {
      "name": "R2-D2"
    },
    "droid": {
      "name": "C-3PO"
    }
  }
}
```

- That means that the GraphQL service needs to have a `Query` type with `hero` and `droid` fields:

```
type Query {
  hero(episode: Episode): Character
  droid(id: ID!): Droid
}
```

- When you write a GraphQL query, you always want to start with the operation keyword (either query or mutation) and its name (like `GetLaunches`)
  - It’s important to give your queries descriptive names so they’re discoverable in Apollo developer tooling
- Next, we use a pair of curly braces after the query name to indicate the body of our query
- Finally, we use another pair of curly braces to indicate a selection set
  - The selection set describes which fields we want our query response to contain
- Mutations work in a similar way
  - Define fields on the `Mutation` type, and those are available as the root mutation fields you can call in your query
  - The return type for your GraphQL mutation is completely up to you, but we recommend defining a special response type to ensure a proper response is returned back to the client
    - In a larger project, you might abstract this type into an interface

```
type Mutation {
  # if false, booking trips failed -- check errors
  bookTrips(launchIds: [ID]!): TripUpdateResponse!

  # if false, cancellation failed -- check errors
  cancelTrip(launchId: ID!): TripUpdateResponse!

  login(email: String): String # login token
}

type TripUpdateResponse {
  success: Boolean!
  message: String
  launches: [Launch]
}
```

## Scalar types

- A GraphQL object type has a name and fields, but at some point those fields have to resolve to some concrete data
- Scalar types represent the leaves of the query
- Concrete units of data

```
{
  hero {
    name
    appearsIn
  }
}
```

```
{
  "data": {
    "hero": {
      "name": "R2-D2",
      "appearsIn": [
        "NEWHOPE",
        "EMPIRE",
        "JEDI"
      ]
    }
  }
}
```

- We know this because those fields don't have any sub-fields
  - They are the leaves of the query
- Default scalar types

  - `Int`
    - A signed 32‐bit integer
  - `Float`
    - A signed double-precision floating-point value
  - `String`
    - A UTF‐8 character sequence
  - `Boolean`
    - `true` or `false`
  - `ID`
    - The ID scalar type represents a unique identifier
    - Often used to refetch an object or as the key for a cache
    - The ID type is serialized in the same way as a `String`
    - However, defining it as an `ID` signifies that it is not intended to be human‐readable

- There is also a way to specify custom scalar types
- For example, we could define a `Date` type:
- scalar Date

## Enumeration types

- Also called Enums
- A special kind of scalar that is restricted to a particular set of allowed values
- This allows you to:
  - Validate that any arguments of this type are one of the allowed values
  - Communicate through the type system that a field will always be one of a finite set of values

```
enum Episode {
  NEWHOPE
  EMPIRE
  JEDI
}
```

- This means that wherever we use the type `Episode` in our schema, we expect it to be exactly one of `NEWHOPE`, `EMPIRE`, or `JEDI`

## Lists and Non-Null

- Object types, scalars, and enums are the only kinds of types you can define in GraphQL
- But you can apply additional type modifiers that affect validation of those values

```
type Character {
  name: String!
  appearsIn: [Episode]!
}
```

- Here, we're using a `String` type and marking it as Non-Null by adding an exclamation mark, `!` after the type name
- This means that our server always expects to return a non-null value for this field
- If it ends up getting a null value it will trigger a GraphQL execution error
- The Non-Null type modifier can also be used when defining arguments for a field

```
query DroidById($id: ID!) {
  droid(id: $id) {
    name
  }
}
```

```
{
  "id": null
}
```

```
{
  "errors": [
    {
      "message": "Variable \"$id\" of required type \"ID!\" was not provided.",
      "locations": [
        {
          "line": 1,
          "column": 17
        }
      ]
    }
  ]
}
```

- We can also use a type modifier to mark a type as a `List`
- Indicates that this field will return an array of that type
- This is denoted by wrapping the type in square brackets, `[` and `]`
- It works the same for arguments

## Interfaces

- An Interface is an abstract type that includes a certain set of fields that a type must include to implement the interface
- It allows you to specify a set of fields that any concrete type, which implements this interface, needs to have
- In many GraphQL schemas, every type is required to have an `id` field
- Using interfaces, this requirement can be expressed by defining an interface with this field and then making sure that all custom types implement it:

```
interface Node {
  id: ID!
}

type User implements Node {
  id: ID!
  name: String!
  age: Int!
}
```

- Another example, you could have an interface `Character` that represents any character in the Star Wars trilogy:

```
interface Character {
  id: ID!
  name: String!
  friends: [Character]
  appearsIn: [Episode]!
}
```

- This means that any type that implements `Character` needs to have these exact fields, with these arguments and return types.

```
type Human implements Character {
  id: ID!
  name: String!
  friends: [Character]
  appearsIn: [Episode]!
  starships: [Starship]
  totalCredits: Int
}

type Droid implements Character {
  id: ID!
  name: String!
  friends: [Character]
  appearsIn: [Episode]!
  primaryFunction: String
}
```

- Interfaces are useful when you want to return an object or set of objects, but those might be of several different types

```
query HeroForEpisode($ep: Episode!) {
  hero(episode: $ep) {
    name
    primaryFunction
  }
}
```

```
{
  "ep": "JEDI"
}
```

```
{
  "errors": [
    {
      "message": "Cannot query field \"primaryFunction\" on type \"Character\". Did you mean to use an inline fragment on \"Droid\"?",
      "locations": [
        {
          "line": 4,
          "column": 5
        }
      ]
    }
  ]
}
```

- The `hero` field returns the type `Character`, which means it might be either a `Human` or a `Droid` depending on the `episode` argument
- In the query above, you can only ask for fields that exist on the `Character` interface, which doesn't include `primaryFunction`
- To ask for a field on a specific object type, you need to use an inline fragment

```
query HeroForEpisode($ep: Episode!) {
  hero(episode: $ep) {
    name
    ... on Droid {
      primaryFunction
    }
  }
}
```

## Union types

- Union types are very similar to interfaces, but they don't get to specify any common fields between the types
- Can be used to express that a type should be either of a collection of other types
- Let’s consider the following types:

```
type Adult {
  name: String!
  work: String!
}

type Child {
  name: String!
  school: String!
}
```

- Now, we could define a `Person` type to be the **union** of `Adult` and `Child`:

```
`union Person = Adult | Child`
```

- This brings up a different problem:
- In a GraphQL query where we ask to retrieve information about a `Child` but only have a `Person` type to work with, how do we know whether we can actually access this field?
- The answer to this is called conditional fragments:

```
{
  allPersons {
    name # works for `Adult` and `Child`
    ... on Child {
      school
    }
    ... on Adult {
       work
    }
  }
}
```

- Another example:

```
union SearchResult = Human | Droid | Starship
```

- Wherever we return a `SearchResult` type in our schema, we might get a `Human`, a `Droid`, or a `Starship`
- Note that members of a union type need to be concrete object types
  - You can't create a union type out of interfaces or other unions
- if you query a field that returns the `SearchResult` union type, you need to use a conditional fragment to be able to query any fields at all:

```
{
  search(text: "an") {
    __typename
    ... on Human {
      name
      height
    }
    ... on Droid {
      name
      primaryFunction
    }
    ... on Starship {
      name
      length
    }
  }
}
```

```
{
  "data": {
    "search": [
      {
        "__typename": "Human",
        "name": "Han Solo",
        "height": 1.8
      },
      {
        "__typename": "Human",
        "name": "Leia Organa",
        "height": 1.5
      },
      {
        "__typename": "Starship",
        "name": "TIE Advanced x1",
        "length": 9.2
      }
    ]
  }
}
```

## Input types

- You can also easily pass complex objects as arguments into a field
- This is particularly valuable in the case of mutations, where you might want to pass in a whole object to be created

```
input ReviewInput {
  stars: Int!
  commentary: String
}
```

- Here is how you could use the input object type in a mutation:

```
mutation CreateReviewForEpisode($ep: Episode!, $review: ReviewInput!) {
  createReview(episode: $ep, review: $review) {
    stars
    commentary
  }
}
```

```
{
  "ep": "JEDI",
  "review": {
    "stars": 5,
    "commentary": "This is a great movie!"
  }
}
```

```
{
  "data": {
    "createReview": {
      "stars": 5,
      "commentary": "This is a great movie!"
    }
  }
}
```

- The fields on an input object type can themselves refer to input object types
- But, you can't mix input and output types in your schema
- Input object types also can't have arguments on their fields

---

# _Validation_

- By using the type system, it can be predetermined whether a GraphQL query is valid or not
- This allows servers and clients to effectively inform developers when an invalid query has been created, without having to rely on runtime checks
- https://github.com/graphql/graphql-js/tree/master/src/validation

---

# _Schema Stitching_

- Makes it possible to create one schema out of multiple schemas

## Technical Separation

- A separation by technical concerns for the GraphQL schema and resolvers

```
* src/
  * models/
    * index.js
  * resolvers/
    * index.js
    * user.js
    * message.js
  * schema/
    * index.js
    * user.js
    * message.js
  * index.js
```

## Domain Separation

- Assume you have a GraphQL schema you want to modularize based on domains (e.g. user, message)
- You may end up with two schemas, where each schema matches one type (e.g. User type, Message type)
  - The operation requires merging both GraphQL schemas to make the entire GraphQL schema accessible with your GraphQL server’s API
- First, separate entities in their own schema definition file

```
import { gql } from 'apollo-server-express';

export default gql`
  extend type Query {
    users: [User!]
    user(id: ID!): User
    me: User
  }

  type User {
    id: ID!
    username: String!
    messages: [Message!]
  }
`;
```

```
import { gql } from 'apollo-server-express';

export default gql`
  extend type Query {
    messages: [Message!]!
    message(id: ID!): Message!
  }

  extend type Mutation {
    createMessage(text: String!): Message!
    deleteMessage(id: ID!): Boolean!
  }

  type Message {
    id: ID!
    text: String!
    user: User!
  }
`;
```

- Each file only describes its own entity, with a type and its relations
- A relation can be a type from a different file, such as a Message type that still has the relation to a User type even though the User type is defined somewhere else
- Note the `extend` statement on the Query and Mutation types
- Since you have more than one of those types now, you need to extend the types
- Next, define shared base types for them in the `src/schema/index.js`

```
import { gql } from 'apollo-server-express';

import userSchema from './user';
import messageSchema from './message';

const linkSchema = gql`
  type Query {
    _: Boolean
  }

  type Mutation {
    _: Boolean
  }

  type Subscription {
    _: Boolean
  }
`;

export default [linkSchema, userSchema, messageSchema];
```

- Both schemas are merged with the help of a utility called `linkSchema`
- The `linkSchema` defines all types shared within the schemas

---

# Models

- The models are your data access layer, which can be sample data, a database, or a third-party API
- As an improvement, models are passed to the resolver function’s as context
- It’s always good to pass those things from the outside to keep the resolver functions pure
- Then, you don’t need to import the models in each resolver file

```
const server = new ApolloServer({
  typeDefs,
  resolvers,
  context: {
    models,
  }
});
```

---

# _Execution_

- After being validated, a GraphQL query is executed by a GraphQL server
- All the GraphQL server has to do is invoke all resolver functions for the fields that are contained in the query and then package up the response according to the query’s shape
- It returns a result that mirrors the shape of the requested query, typically as JSON
- Setting up a schema:

```
type Query {
  human(id: ID!): Human
}

type Human {
  name: String
  appearsIn: [Episode]
  starships: [Starship]
}

enum Episode {
  NEWHOPE
  EMPIRE
  JEDI
}

type Starship {
  name: String
}
```

- In order to describe what happens when a query is executed, let's use an example to walk through

```
{
  human(id: 1002) {
    name
    appearsIn
    starships {
      name
    }
  }
}
```

```
{
  "data": {
    "human": {
      "name": "Han Solo",
      "appearsIn": [
        "NEWHOPE",
        "EMPIRE",
        "JEDI"
      ],
      "starships": [
        {
          "name": "Millenium Falcon"
        },
        {
          "name": "Imperial shuttle"
        }
      ]
    }
  }
}
```

- You can think of each field in a GraphQL query as a function or method of the previous type which returns the next type
  - In fact, this is exactly how GraphQL works
- Each field on each type is backed by a function called the resolver
  - It's provided by the GraphQL server developer
- When a field is executed, the corresponding resolver is called to produce the next value
- If a field produces a scalar value like a string or number, then the execution completes
- However if a field produces an object value then the query will contain another selection of fields which apply to that object
- This continues until scalar values are reached
- GraphQL queries always end at scalar values

## Root fields & resolvers

- At the top level of every GraphQL server is a type that represents all of the possible entry points into the GraphQL API
  - It's often called the Root type or the Query type
- In the ongoing example, our Query type provides a field called `human` which accepts the argument `id`
- The resolver function for this field likely accesses a database and then constructs and returns a `Human` object

```
Query: {
  human(parent, args, context, info) {
    return context.db.loadHumanByID(args.id).then(
      userData => new Human(userData)
    )
  }
}
```

- A resolver function receives four arguments:
  - `obj` / `parent` / `root`
    - The previous object
    - The result of the previous resolver execution level
      - Each level of nested curly braces corresponds to one resolver execution level
    - For a field on the root Query type is often not used
  - `arguments` / `args`
    - The arguments provided to the field in the GraphQL query
  - `context` / `ctx`
    - An object which is provided to every resolver and holds important contextual information like the currently logged in user, or access to a database
    - We use the context to contain per-request state such as authentication information and access our data sources
    - A plain JavaScript object that every resolver in the resolver chain can read from and write to
    - It thus basically is a means for resolvers to communicate
    - It’s also possible to already write to it at the moment when the GraphQL server itself is being initialized
    - So, it’s also a way for you to pass arbitrary data or functions to the resolvers
  - `info`
    - A value which holds field-specific information relevant to the current query as well as the schema details
    - Information about the execution state of the operation which should only be used in advanced cases
- We structure our resolvers into a map where the keys correspond to the types and fields in our schema
  - A resolver always has to be named after the corresponding field from the schema definition
- You can write resolvers for any types in your schema, not just queries and mutations
- GraphQL has default resolvers
  - We don’t have to write a resolver for a field if the parent object has a property with the same name
- For an example using parent, a schema of:

```
type Query {
  info: String!
  feed: [Link!]!
}

type Link {
  id: ID!
  description: String!
  url: String!
}
```

- With data of:

```
let links = [{
  id: 'link-0',
  url: 'www.howtographql.com',
  description: 'Fullstack tutorial for GraphQL'
}]
```

- The resolvers would be:

```
const resolvers = {
  Query: {
    info: () => `This is the API of a Hackernews Clone`,
    feed: () => links,
  },
  Link: {
    id: (parent) => parent.id,
    description: (parent) => parent.description,
    url: (parent) => parent.url,
  }
}
```

    * In each of the three ``Link`` resolvers, the incoming ``parent`` object is the element inside the ``links`` list
    * Because the ``Link`` resolvers are trivial, you can actually omit them

## Asynchronous resolvers

- In this resolver function:

```
human(obj, args, context, info) {
  return context.db.loadHumanByID(args.id).then(
    userData => new Human(userData)
  )
}
```

- The `context` is used to provide access to a database
  - Which is used to load the data for a user by the `id` provided as an argument in the GraphQL query
- Since loading from a database is an asynchronous operation, this returns a Promise
- When the database returns, we can construct and return a new `Human` object
  - The resolver function needs to be aware of Promises
  - The GraphQL query does not
- It simply expects the `human` field to return something which it can then ask the `name` of
- During execution, GraphQL will wait for Promises to complete before continuing and will do so with optimal concurrency

## Trivial resolvers

- Now that a `Human` object is available, GraphQL execution can continue with the fields requested on it

```
Human: {
  name(obj, args, context, info) {
    return obj.name
  }
}
```

- A GraphQL server is powered by a type system which is used to determine what to do next
- Even before the `human` field returns anything
- GraphQL knows that the next step will be to resolve fields on the `Human` type since the type system tells it that the `human` field will return a `Human`
- Resolving the name in this case is very straight-forward
- The name resolver function is called and the `obj` argument is the `new Human` object returned from the previous field
- In this case, we expect that Human object to have a `name` property which we can read and return directly
- In fact, many GraphQL libraries will let you omit resolvers this simple
  - They will just assume that if a resolver isn't provided for a field, that a property of the same name should be read and returned

## Scalar coercion

- While the `name` field is being resolved, the `appearsIn` and `starships` fields can be resolved concurrently
- The `appearsIn` field could also have a trivial resolver, but let's take a closer look

```
Human: {
  appearsIn(obj) {
    return obj.appearsIn // returns [ 4, 5, 6 ]
  }
}
```

- Our type system claims `appearsIn` will return Enum values with known values
- However this function is returning numbers
- The type system knows what to expect and will convert the values returned by a resolver function into something that upholds the API contract
- In this case, there may be an Enum defined on our server which uses numbers like `4`, `5`, and `6` internally, but represents them as Enum values in the GraphQL type system

## List resolvers

- We've already seen a bit of what happens when a field returns a list of things with the `appearsIn` field above
- It returned a list of enum values, and since that's what the type system expected, each item in the list was coerced to the appropriate enum value
- What happens when the `starships` field is resolved?

```
Human: {
  starships(obj, args, context, info) {
    return obj.starshipIDs.map(
      id => context.db.loadStarshipByID(id).then(
        shipData => new Starship(shipData)
      )
    )
  }
}
```

- The resolver for this field is not just returning a Promise, it's returning a list of Promises
- The `Human` object had a list of ids of the `Starships` they piloted, but we need to go load all of those ids to get real Starship objects
- GraphQL will wait for all of these Promises concurrently before continuing
- When left with a list of objects, it will concurrently continue yet again to load the `name` field on each of these items

## Producing the result

- As each field is resolved, the resulting value is placed into a key-value map
  - The field name (or alias) as the key and the resolved value as the value
- This continues from the bottom leaf fields of the query all the way back up to the original field on the root Query type
- Collectively these produce a structure that mirrors the original query which can then be sent (typically as JSON) to the client which requested it

---

# _Introspection_

- GraphQL allows us ask a schema for information about what queries it supports using the introspection system
- By querying the `__schema` field on the root type of a Query, we can see what types are available

```
{
  __schema {
    types {
      name
    }
  }
}
```

- It is often useful to examine one specific type
- Let's take a look at the `Droid` type:

```
{
  __type(name: "Droid") {
    name
  }
}
```

- What if we want to know more about Droid:
  - `kind`

```
{
  __type(name: "Droid") {
    name
    kind
  }
}
```

- It's useful for an object to know what fields are available:
  - `fields`

```
{
  __type(name: "Droid") {
    name
    fields {
      name
      type {
        name
        kind
      }
    }
  }
}
```

- `ofType`

```
{
  __type(name: "Droid") {
    name
    fields {
      name
      type {
        name
        kind
        ofType {
          name
          kind
        }
      }
    }
  }
}
```

- `description`

```
{
  __type(name: "Droid") {
    name
    description
  }
}
```

- https://github.com/graphql/graphql-js/blob/master/src/type/introspection.js

---

# _Best Practices_

## Introduction

### HTTP

- GraphQL is typically served over HTTP via a single endpoint which expresses the full set of capabilities of the service

### JSON (with GZIP)

- GraphQL services typically respond using JSON
  - Because it is mostly text, it compresses exceptionally well with GZIP
- It's encouraged that any production GraphQL services enable GZIP and encourage their clients to send the header:
- Accept-Encoding: gzip

### Versioning

- GraphQL takes a strong opinion on avoiding versioning by providing the tools for the continuous evolution of a GraphQL schema
- In contrast, GraphQL only returns the data that's explicitly requested, so new capabilities can be added via new types and new fields on those types without creating a breaking change

### Nullability

- In the GraphQL type system, every field is nullable by default
- This is because there are many things which can go awry in a networked service backed by databases and other services
- When designing a GraphQL schema, it's important to keep in mind all the problems that could go wrong and if "null" is an appropriate value for a failed field
- Typically it is, but occasionally, it's not
- In those cases, use non-null types to make that guarantee

### Pagination

- The GraphQL type system allows for some fields to return lists of values, but leaves the pagination of longer lists of values up to the API designer
- Typically fields that could return long lists accept arguments "first" and "after" to allow for specifying a specific region of a list, where "after" is a unique identifier of each of the values in the list
- Ultimately designing APIs with feature-rich pagination led to a best practice pattern called "Connections"

### Server-side Batching & Caching

- GraphQL is designed in a way that allows you to write clean code on the server
- Every field on every type has a focused single-purpose function for resolving that value
- However without additional consideration, a naive GraphQL service could be very "chatty" or repeatedly load data from your databases
- This is commonly solved by a batching technique, where multiple requests for data from a backend are collected over a short period of time and then dispatched in a single request to an underlying database or microservice by using a tool like Facebook's DataLoader
  - https://github.com/facebook/dataloader#using-with-graphql

## Thinking in Graphs

### It's Graphs All the Way Down

- With GraphQL, you model your business domain as a graph by defining a schema
- Within your schema, you define different types of nodes and how they connect/relate to one another
- On the client, this creates a pattern similar to Object-Oriented Programming:
  - Types that reference other types
- On the server, since GraphQL only defines the interface, you have the freedom to use it with any backend

### Shared Language

- Naming things is a hard but important part of building intuitive APIs
- To build a good schema, examine the everyday language you use to describe your business
- Let's try to describe an email app in plain english
  - A user can have multiple email accounts
  - Each email account has an address, inbox, drafts, deleted items, and sent items
  - Each email has a sender, receive date, subject, and body
  - Users cannot send an email without a recipient address
- Fetch the number of unread emails in my inbox for all my accounts

```
{
  accounts {
    inbox {
      unreadEmailCount
    }
  }
}
```

- Fetch the "preview info" for the first 20 drafts in the main account

```
{
  mainAccount {
    drafts(first: 20) {
      ...previewInfo
    }
  }
}

fragment previewInfo on Email {
  subject
  bodyPreviewSentence
}
```

### Business Logic Layer

- Your business logic layer should act as the single source of truth for enforcing business domain rules
- Where should you define the actual business logic?
- Where should you perform validation and authorization checks?
- The answer: inside a dedicated business logic layer
- Your business logic layer should act as the single source of truth for enforcing business domain rules

### Working with Legacy Data

- Prefer building a GraphQL schema that describes how clients use the data, rather than mirroring the legacy database schema.

### One Step at a time

- Get validation and feedback more frequently
- Build only the part of the schema that you need for one scenario at a time
- By gradually expanding the schema, you will get validation and feedback more frequently to steer you toward building the right solution

## Serving over HTTP

- Here are some guidelines for setting up a GraphQL server to operate over HTTP

### Web Request Pipeline

- GraphQL should be placed after all authentication middleware
- So that you have access to the same session and user information you would in your HTTP endpoint handlers

### URIs, Routes

- GraphQL server operates on a single URL/endpoint, usually `/graphql`
- All GraphQL requests for a given service should be directed at this endpoint

### HTTP Methods, Headers, and Body

- Your GraphQL HTTP server should handle the HTTP GET and POST methods

### GET request

- When receiving an HTTP GET request, the GraphQL query should be specified in the "query" query string
- If we wanted to execute the following GraphQL query:

```
{
  me {
    name
  }
}
```

- This request could be sent via an HTTP GET like so:

```
http://myapi/graphql?query={me{name}}
```

- Query variables can be sent as a JSON-encoded string in an additional query parameter called `variables`
- If the query contains several named operations, an `operationName` query parameter can be used to control which one should be executed

### POST request

- A standard GraphQL POST request should use the `application/json` content type
- And include a JSON-encoded body of the following form:

```
{
  "query": "...",
  "operationName": "...",
  "variables": { "myVariable": "someValue", ... }
}
```

- `operationName` and `variables` are optional fields
- `operationName` is only required if multiple operations are present in the query

### Response

- Regardless of the method by which the query and variables were sent, the response should be returned in the body of the request in JSON format
- As mentioned in the spec, a query might result in some data and some errors, and those should be returned in a JSON object of the form:

```
{
  "data": { ... },
  "errors": [ ... ]
}
```

- If there were no errors returned, the `"errors"` field should not be present on the response
- If no data is returned, the `"data"` field should only be included if the error occurred during execution

### GraphiQL

- GraphiQL is useful during testing and development but should be disabled in production by default
- If you are using express-graphql, you can toggle it based on the NODE_ENV environment variable:

```
app.use('/graphql', graphqlHTTP({
  schema: MySessionAwareGraphQLSchema,
  graphiql: process.env.NODE_ENV === 'development',
}));
```

### Node

- If you are using NodeJS, we recommend using either [express-graphql](https://github.com/graphql/express-graphql) or [graphql-server](https://github.com/apollostack/graphql-server)

## Authorization

- Authentication and authorization are often confused
  - Authentication describes the process of claiming an identity
    - That’s what you do when you log in to a service with a username and password, you authenticate yourself
  - Authorization on the other hand describes permission rules that specify the access rights of individual users and user groups to certain parts of the system
- Delegate authorization logic to the business logic layer
- Authorization is a type of business logic that describes whether a given user/session/context has permission to perform an action or see a piece of data
- For example, “Only authors can see their drafts”
- Enforcing this kind of behavior should happen in the [business logic layer](https://graphql.github.io/learn/thinking-in-graphs/#business-logic-layer)
- It is tempting to place authorization logic in the GraphQL layer like so:

```
var postType = new GraphQLObjectType({
  name: ‘Post’,
  fields: {
    body: {
      type: GraphQLString,
      resolve: (post, args, context, { rootValue }) => {
        // return the post body only if the user is the post's author
        if (context.user && (context.user.id === post.authorId)) {
          return post.body;
        }
        return null;
      }
    }
  }
});
```

- We would need to duplicate this auth code for each entry point into the service
- Then if the authorization logic is not kept perfectly in sync, users could see different data depending on which API they use
- We can avoid that by having a [single source of truth](https://graphql.github.io/learn/thinking-in-graphs/#business-logic-layer) for authorization
- Delegate authorization logic to the business logic layer

```
//Authorization logic lives inside postRepository
var postRepository = require('postRepository');

var postType = new GraphQLObjectType({
  name: ‘Post’,
  fields: {
    body: {
      type: GraphQLString,
      resolve: (post, args, context, { rootValue }) => {
        return postRepository.getBody(context.user, post);
      }
    }
  }
});
```

- We see that the business logic layer requires the caller to provide a user object
- If you are using GraphQL.js, the User object should be populated on the `context` argument or `rootValue` in the fourth argument of the resolver
- We recommend passing a fully-hydrated User object instead of an opaque token or API key to your business logic layer
- This way, we can handle the distinct concerns of authentication and authorization in different stages of the request processing pipeline

## Pagination

- Different pagination models enable different client capabilities
- A common use case in GraphQL is traversing the relationship between sets of objects
- There are a number of different ways that these relationships can be exposed in GraphQL, giving a varying set of capabilities to the client developer

### Plurals

- The most simple way to expose a connection between objects is with a field that returns a plural type

```
{
  hero {
    name
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

### Slicing

- A client might want to be able to specify how many friends they want to fetch

```
{
  hero {
    name
    friends(first:2) {
      name
    }
  }
}
```

### Pagination and Edges

- Once the client fetches the first two friends, they might want to send a second request to ask for the next two friends
- There are a number of ways we could do pagination:
  - We could do something like `friends(first:2 offset:2)` to ask for the next two in the list
  - We could do something like `friends(first:2 after:$friendId)`, to ask for the next two after the last friend we fetched
  - We could do something like `friends(first:2 after:$friendCursor)`, where we get a cursor from the last item and use that to paginate
- Cursor-based pagination is the most powerful of those designed
- How do we get the cursor from the object?
- Our `friends` field should give us a list of edges, and an edge has both a cursor and the underlying node:

```
{
  hero {
    name
    friends(first:2) {
      edges {
        node {
          name
        }
        cursor
      }
    }
  }
}
```

### End-of-list, counts, and Connections

- How do we know when we reach the end of the connection?
- We have to keep querying until we get an empty list back
- But we'd really like for the connection to tell us when we've reached the end so we don't need that additional request
- Similarly, what if we want to know additional information about the connection itself
- For example, how many total friends does R2-D2 have?
- To solve both of these problems, our `friends` field can return a connection object
- The connection object will then have a field for the edges
- As well as other information like total count and information about whether a next page exists

```
{
  hero {
    name
    friends(first:2) {
      totalCount
      edges {
        node {
          name
        }
        cursor
      }
      pageInfo {
        endCursor
        hasNextPage
      }
    }
  }
}
```

### Complete Connection Model

- Clearly, this is more complex than our original design of just having a plural
- But by adopting this design, we've unlocked a number of capabilities for the client:
  - The ability to paginate through the list
  - The ability to ask for information about the connection itself, like `totalCount` or `pageInfo`
  - The ability to ask for information about the edge itself, like `cursor` or `friendshipTime`
  - The ability to change how our backend does pagination, since the user just uses opaque cursors
- To see this in action, there's an additional field in the example schema, called `friendsConnection`, that exposes all of these concepts

```
{
  hero {
    name
    friendsConnection(first:2 after:"Y3Vyc29yMQ==") {
      totalCount
      edges {
        node {
          name
        }
        cursor
      }
      pageInfo {
        endCursor
        hasNextPage
      }
    }
  }
}
```

```
{
  "data": {
    "hero": {
      "name": "R2-D2",
      "friendsConnection": {
        "totalCount": 3,
        "edges": [
          {
            "node": {
              "name": "Han Solo"
            },
            "cursor": "Y3Vyc29yMg=="
          },
          {
            "node": {
              "name": "Leia Organa"
            },
            "cursor": "Y3Vyc29yMw=="
          }
        ],
        "pageInfo": {
          "endCursor": "Y3Vyc29yMw==",
          "hasNextPage": false
        }
      }
    }
  }
}
```

## Caching

- Providing Object Identifiers allows clients to build rich caches
- In an endpoint-based API, clients can use HTTP caching to easily avoid refetching resources
- And for identifying when two resources are the same
- The URL in these APIs is a globally unique identifier that the client can leverage to build a cache
- In GraphQL, though, there's no URL-like primitive that provides this globally unique identifier for a given object
- It's hence a best practice for the API to expose such an identifier for clients to use

### Globally Unique IDs

- One possible pattern for this is reserving a field, like `id`, to be a globally unique identifier

```
{
  starship(id:"3003") {
    id
    name
  }
  droid(id:"2001") {
    id
    name
    friends {
      id
      name
    }
  }
}
```

### Compatibility with existing APIs

- One concern with using the `id` field for this purpose is how a client using the GraphQL API would work with existing APIs
- if our existing API accepted a type-specific ID, but our GraphQL API uses globally unique IDs, then using both at once can be tricky
- In these cases, the GraphQL API can expose the previous API's IDs in a separate field
- This gives us the best of both worlds:
  - GraphQL clients can continue to rely on a consistent mechanism for getting a globally unique ID
  - Clients that need to work with our previous API can also fetch `previousApiId` from the object, and use that

### Alternatives

- While globally unique IDs have proven to be a powerful pattern in the past, they are not the only pattern that can be used, nor are they right for every situation
- The really critical functionality that the client needs is the ability to derive a globally unique identifier for their caching
- While having the server derive that ID simplifies the client, the client can also derive the identifier
- Oftentimes, this would be as simple as combining the type of the object (queried with `__typename`) with some type-unique identifier
- Additionally, if replacing an existing API with a GraphQL API, it may be confusing if all of the fields in GraphQL are the same except `id`, which changed to be globally unique
- This would be another reason why one might choose not to use `id` as the globally unique field.

---

# _Security_

## Timeout

- Using a timeout to defend against large queries
- For example, a server configured with a 5 seconds timeout would stop the execution of any query that is taking more than 5 seconds to execute
- Timeout Pros:
  - Simple to implement
  - Most strategies will still use a timeout as a final protection
- Timeout Cons
  - Damage can already be done even when the timeout kicks in
  - Sometimes hard to implement
  - Cutting connections after a certain time may result in strange behaviours

## Maximum Query Depth

- Clients using GraphQL may craft any complex query they want
- Since GraphQL schemas are often cyclic graphs, this means a client could craft a query that goes on indefinitely
- By analyzing the query document’s abstract syntax tree (AST), a GraphQL server is able to reject or accept a request based on its depth
- Maximum Query Depth Pros:
  - Since the AST of the document is analyzed statically, the query does not even execute, which adds no load on your GraphQL server
- Maximum Query Depth Cons:
  - Depth alone is often not enough to cover all abusive queries
  - For example, a query requesting an enormous amount of nodes on the root will be very expensive but unlikely to be blocked by a query depth analyzer

## Query Complexity

- In a lot of cases, certain fields in our schema are known to be more complex to compute than others.
- Query complexity allows you to define how complex these fields are, and to restrict queries with a maximum complexity
- The idea is to define how complex each field is by using a simple number
- A common default is to give each field a complexity of `1` to start
- Query Complexity Pros:
  - Covers more cases than a simple query depth
  - Reject queries before executing them by statically analyzing the complexity
- Query Complexity Cons:
  - Hard to implement perfectly
  - If complexity is estimated by developers, how do we keep it up to date?
  - How do we find the costs in the first place?
  - Mutations are hard to estimate
  - What if they have a side effect that is hard to measure, like queuing a background job?

## Throttling

- The solutions we’ve seen so far are great to stop abusive queries from taking your servers down
- The problem with using them alone like this is that they will stop large queries, but won’t stop clients that are making a lot of medium sized queries!
- In most APIs, a simple throttle is used to stop clients from requesting resources too often
- GraphQL is a bit special because throttling on the number of requests does not really help us
- Even a few queries might be too much if they are very large.
- In fact, we have no idea what amount of requests is acceptable since they are defined by the clients
- So what can we use to throttle clients?

### Throttling Based on Server Time

- A good estimate of how expensive a query is the server time it needs to complete
- We can use this heuristic to throttle queries
- With a good knowledge of your system, you can come up with a maximum server time aclient can use over a certain time frame
- We also decide on how much server time is added to a client over time
- This is a classic [leaky bucket algorithm](https://en.wikipedia.org/wiki/Leaky_bucket)
- There are other throttling algorithms out there, but they are out of scope for this chapter
- We will use a leaky bucket throttle in the next examples
- Let’s imagine our maximum server time (Bucket Size) allowed is set to `1000ms`
- That clients gain `100ms` of server time per second (Leak Rate)

```
mutation {
  createPost(input: { title: "GraphQL Security" }) {
    post {
      title
    }
  }
}
```

- This mutation takes on average `200ms` to complete
  - In reality, the time may vary but we’ll assume it always takes `200ms` to complete for the sake of this example
- It means that a client calling this operation more than 5 times within 1 second would be blocked until more available server time is added to the client
- After two seconds (`100ms` is added by second), our client could call the `createPost` a single time
- As you can see, throttling based on time is a great way to throttle GraphQL queries since complex queries will end up consuming more time meaning you can call them less often, and smaller queries may be called more often since they will be very fast to compute
- It can be good to express these throttling constraints to clients if your GraphQL API is public
- In that case, server time is not always the easiest thing to express to clients, and clients cannot really estimate what time their queries will take without trying them first

### Throttling Based on Query Complexity

- Throttling based on Query Complexity is a great way to work with clients and help them respect the limits of your schema
- Let’s use the same complexity example we used in the Query Complexity section:

```
query {
  author(id: "abc") {    # complexity: 1
    posts {              # complexity: 1
      title              # complexity: 1
    }
  }
}
```

- We know that this query has a cost `3` based on complexity
- Just like a time throttle, we can come up with a maximum cost (Bucket Size) per time a client can use
- With a maximum cost of `9`, our clients could run this query only three times, before the leak rate forbids them to query more
- The principles are the same as our time throttle, but now communicating these limits to clients is much nicer
- Clients can even calculate the costs of their queries themselves without needing to estimate server time
- The GitHub public API actually uses this approach to throttle their clients
  - Take a look at how they express these limits to users
    - https://developer.github.com/v4/guides/resource-limitations/

---

# _PostgreSQL with Sequelize_

- `npm install pg sequelize --save`

---

# _Old_

## Queries

- Queries look like the data you request
- Will return only the data you have requested

```
query {
  users {
    id
    name
    email
  }
}
```

- Add params to filter a query

```
query {
  users(where: { name_contains: "Chase" }) {
    id
    name
    email
  }
}
```

- Connections
  - A connection to a list of items

```
query {
  usersConnection {
    pageInfo {
      hasNextPage
      hasPreviousPage
    }
    aggregate {
      count
    }
  }
}
```

## Mutations

- Updating the database
- Must specify what data to return
  - `name`, `email`

```
mutation {
  createUser(data: { name: "Chase", email: "hmm@ql.com" }) {
    name
    email
  }
}
```

## Schema

- Types
  - Queries
    - Reading data
  - Mutations
    - Creating data
    - Updating data
    - Deleting data
- Emum list fields
  - A custom type that ensures only values in this list can be used

```
enum Permission {
  ADMIN
  USER
  ITEMCREATE
  ITEMUPDATE
  ITEMDELETE
  PERMISSIONUPDATE
}
```

- Fields
  - The value is the data type of the field
    - Int
    - Float
    - String
    - Boolean
    - ID
    - `DateTime`
      - Provided by Prisma but not accessible unless defined
  - `!` = required
    - [Dog!]!
      - An array of Dogs is required, and no element can be null
- Directives
  - A way to provide additional info in your data model
  - `@unique`
    - Ensures that each entry is unique

## Resolvers

- Methods that perform the queries (pull data) and mutations (push data) defined in our schema, and resolves them according to the schema
- Answers the questions:
  - Where does this data come from?
  - How do I get it to the user?
- Database calls go here
- 2 resolver types
  - Query resolvers
    - pulls data
  - Mutation resolvers
    - pushes data
- Custom types
  - Types that are not tied to the Prisma API
  - Use when you want to return a custom object
  - Define in your `schema.graphql`

```
type SuccessMessage {
  message: String
}

type Mutation {
  signout: SuccessMessage
}
```

## _Security_

- Since anyone can submit queries on the client, you should never expose fields that return sensitive user information or reset tokens
  - Use backend-only fields by creating a custom type in the Yoga schema

## _Relationships_

- Create relationships between types
- In your Prisma datamodel, add a property to a type, of the type to want to be linked to it

```
type User {
  id: ID! @unique
  name: String!
}

type Item {
  id: ID! @unique
  title: String!
  user: User!
}
```

- In Yoga mutation resolver

```
const Mutations = {
  async createItem(parent, args, ctx, info) {
    const item = await ctx.db.mutation.createItem(
      {
        data: {
          // This is how to create a relationship
          //   between the Item and the User
          user: {
            connect: { id: ctx.request.userId }
          },
          ...args
        }
      },
      info
    );
    return item;
  }
};
```

---
