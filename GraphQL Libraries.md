# _GraphQL Libraries_

- https://graphql.github.io/code/
- https://github.com/chentsulin/awesome-graphql

---

# _Boilerplates_

- https://github.com/graphql-boilerplates
- https://github.com/alan345/naperg
  - Prisma, Nodemailer, Yoga, Auth, Subs, Upload, Chat, Apollo
- https://github.com/kriasoft/react-starter-kit/tree/feature/apollo-pure
- https://github.com/vulcanjs/vulcan
- https://github.com/leebenson/reactql
- https://github.com/m-nathani/graphql-elasticsearch-client
  - Apollo Server, Eleasticsearch, KOA, TypeScript, Docker, Helmet
- https://github.com/the-road-to-graphql/fullstack-apollo-express-postgresql-boilerplate

## Lambda

- https://github.com/hasura/graphql-engine/tree/master/community/boilerplates/remote-schemas/aws-lambda/nodejs

---

# _Examples_

- https://github.com/maticzav/gimb-events
  - Husky, SendGrid, Yoga, graphqlgen, Prisma, TypeScript, graphql-shield
- https://github.com/alex996/graphql-chat
  - apollo-server-express, express-session, connect-redis, joi, mongoose
- https://github.com/thekogmo/node-ts-graphql-boilerplate
  - apollo-server-express, express-session, codegen, pg
- https://github.com/up4life/backend
  - ALOT

---

# _Apollo VSCode_

- https://www.apollographql.com/docs/references/apollo-config.html
- There are a few different ways you can link your client to a schema:
  - Use the Apollo Engine [schema registry](https://www.apollographql.com/docs/platform/schema-registry.html)
  - With a remote endpoint (from a running server)
  - With a local schema file
- Add your Engine API key to `.env` on both the frontend and backend
  - `ENGINE_API_KEY=service:<your-service-name>:<hash-from-apollo-engine>`
  - Apollo VSCode uses this API key to pull down your schema from the registry
- On the frontend, create `apollo.config.js`
  - This config file is how you configure both the Apollo VSCode extension and CLI

```
module.exports = {
  client: {
    name: "My Client Project",
    service: "my-service-name"
  }
};
```

---

# _Security_

## GraphQL Shield

- A GraphQL tool to ease the creation of permission layer
- https://github.com/maticzav/graphql-shield
- https://medium.com/@maticzav/graphql-shield-9d1e02520e35

---

```
const db = new Prisma({
  typeDefs: "src/generated/prisma.graphql", // the auto-generated GraphQL schema of the Prisma API
  endpoint: "https://url.to.endpoint", // the endpoint of the Prisma API (value set in `.env`)
  debug: true // log all GraphQL queries & mutations sent to the Prisma API
  // secret: process.env.PRISMA_SECRET, // only needed if specified in `database/prisma.yml` (value set in `.env`)
});

const params = {
  typeDefs: importSchema(path.resolve("./src/schema.graphql")), // Your custom schema
  resolvers, // Your resolvers
  introspection: true, // automatic in DEV but needed in PROD too
  //playground: true, automatic in DEV
  context: req => ({
    ...req,
    db
  })
};

const server = new ApolloServer(params);
```

---

# Database

## PostGraphile

- Instantly spin-up a GraphQL API server by pointing PostGraphile at your existing PostgreSQL database
- https://github.com/graphile/postgraphile

---
