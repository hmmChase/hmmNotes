# _GraphQL Frontend_

---

# _Apollo Client_

- https://github.com/apollographql/apollo-client
- A fully-featured, production ready caching GraphQL client for every UI framework and GraphQL server
- Used in the frontend to '`fetch`' (query) data from GraphQL server endpoint
- For data managment
- Performing mutations
- Fetching data from server
- Caching data
- Managing local state
- Error and loading UI states
- Replaces the need for Redux

## Setup

### CRA - FrontEnd

- `npm i apollo-boost react-apollo graphql`
- Create a client
  - The only thing you need to get started is the endpoint for your GraphQL server
  - Import `ApolloClient` from `apollo-boost`
  - Add the endpoint for our GraphQL server to the `uri` property of the client config object
    - If you don’t pass in `uri` directly, it defaults to the `/graphql` endpoint on the same host your app is served from
  - In `src/index.js`
  - Using Apollo Boost:

```
import ApolloClient from "apollo-boost";

const client = new ApolloClient({
  uri: "http://localhost:4000"
});
```

    * Using Apollo Client directly:

```
import { ApolloClient } from 'apollo-client';
import { createHttpLink } from 'apollo-link-http';
import { InMemoryCache } from 'apollo-cache-inmemory';

const httpLink = createHttpLink({
  uri: 'http://localhost:4000'
});

const client = new ApolloClient({
  link: httpLink,
  cache: new InMemoryCache()
});
```

- Now your client is ready to start fetching data
- Connect your client to React
  - Use the `ApolloProvider` component exported from `react-apollo`

```
import { ApolloProvider } from "react-apollo";

const app = (
  <ApolloProvider client={client}>
    <App />
  </ApolloProvider>
);

ReactDOM.render(app, document.getElementById('root'));
```

- You’re ready to start requesting data with `Query` components

### Next - Frontend

- `npm i graphql`
  - A query language and execution engine
  - Also parses your GraphQL queries
  - https://github.com/facebook/graphql
- `npm i react-apollo`
- `npm i apollo-boost`
  - A zero-config way to start using Apollo Client
  - Package containing everything you need to set up Apollo Client
  - https://github.com/apollographql/apollo-client/tree/master/packages/apollo-boost
- `npm i next-with-apollo`
  - Apollo HOC for Next.js
  - https://github.com/lfades/next-with-apollo

* Create Apollo client
  - create `withApollo.js`

```
import withApollo from 'next-with-apollo';
import ApolloClient, { InMemoryCache } from 'apollo-boost';
import { GRAPHQL_URL, GRAPHQL_PROD_URL } from '../config';

export default withApollo(
  ({ initialState }) => new ApolloClient({
    uri: process.env.NODE_ENV === 'development' ? GRAPHQL_URL : GRAPHQL_PROD_URL,
    cache: new InMemoryCache().restore(initialState || {}),
    getDataFromTree: 'ssr',
    clientState: {
      resolvers: {
        Query: {},
        Mutation: {}
      },
      defaults: {}
    }
  })
);
```

- Create `config.js`

```
export const GRAPHQL_URL = '';
export const GRAPHQL_PROD_URL = '';
```

- Hook Apollo client up to your app by passing it to the `ApolloProvider`
  - In `_app.js`

```
import App, { Container } from 'next/app';
import { ApolloProvider } from 'react-apollo';
import withApollo from '../lib/withApollo';
import Layout from '../components/Layout/Layout';

class MyApp extends App {
  static async getInitialProps({ Component, ctx }) {
    let pageProps = {};

    if (Component.getInitialProps) {
      pageProps = await Component.getInitialProps(ctx);
    }

    return { pageProps };
  }

  render() {
    const { Component, apollo, pageProps } = this.props;

    return (
      <Container>
        <ApolloProvider client={apollo}>
          <Layout>
            <Component {...pageProps} />
          </Layout>
        </ApolloProvider>
      </Container>
    );
  }
}

export default withApollo(MyApp);
```

- create `/lib/witApollo.js`

```
import withApollo from 'next-with-apollo';
import ApolloClient from 'apollo-boost';
import { endpoint } from '../config';

function createClient({ headers }) {
  return new ApolloClient({
    uri: process.env.NODE_ENV === 'development' ? endpoint : endpoint,
    request: operation => {
      operation.setContext({
        fetchOptions: {
          credentials: 'include'
        },
        headers
      });
    }
  });
}

export default withApollo(createClient);
```

- create `config.js`

```
export const endpoint = `http://localhost:4444`;
export const perPage = 4
```

## Queries

- You’ve got two ways of sending queries to the server
  - The first one is to directly use the `query` method on the `ApolloClient` directly
  - This is a very direct way of fetching data and will allow you to process the response as a promise

```
client.query({
  query: gql`
    {
      feed {
        links {
          id
        }
      }
    }
  `
}).then(response => console.log(response.data.allLinks))
```

- A more declarative way when using React however is to use new Apollo’s render prop API to manage your GraphQL data just using components
- Pass the GraphQL query as prop and `<Query />` component will fetch the data for you under the hood, then it’ll make it available in the component’s render prop function
- All of the logic for retrieving your data, tracking loading and error states, and updating your UI is encapsulated in a single `Query` component
  - `loading`: Is `true` as long as the request is still ongoing and the response hasn’t been received
  - `error`: In case the request fails, this field will contain information about what exactly went wrong
  - `data`: This is the actual data that was received from the server
- Process:
  - Write the query as a JavaScript constant using the `gql` parser function
  - Use the `<Query />` component passing the GraphQL query as prop
  - Access the query results that gets injected into the component’s render prop function
- Create a GraphQL query `gql` function which calls the API type, and what to return

```
import { Query } from 'react-apollo';
import { gql } from 'apollo-boost';

const ALL_ITEMS_QUERY = gql`
  query ALL_ITEMS_QUERY {
    items {
      id
      title
      description
    }
  }
`;
```

- Pass your GraphQL query to the `query` prop on the `Query` component
  - `Query` is a React component exported from `react-apollo`
  - Uses the render prop pattern to share GraphQL data with your UI
    - The child of the component can only be a function
    - Give a component in the `render()` a child function
    - The function gets passed a payload of methods to access in the function
      - Returns either loading state, error, or some code

```
<Query query={ALL_ITEMS_QUERY}>
  {({ data, error, loading }) => {
    if (loading) return <p>Loading...</p>;
    if (error) return <p>Error: {error.message}</p>;
    return (
      <ItemsList>
        {data.items.map(item => (
          <Item item={item} key={item.id} />
        ))}
      </ItemsList>
    );
  }}
</Query>
```

- Apollo Client automatically caches this data when it comes back from the server, so you won’t see a loading indicator if you run the same query twice

### Props

- https://www.apollographql.com/docs/react/essentials/queries.html#props
- `query` and `children` are required
- `query`: DocumentNode
  - A GraphQL query document parsed into an AST by `graphql-tag`
- `children`: (result: QueryResult) => React.ReactNode
  - A function returning the UI you want to render based on your query result
- `variables`: { [key: string]: any }
  - An object containing all of the variables your query needs to execute
- `pollInterval`: number
  - Specifies the interval in ms at which you want your component to poll for data
  - Defaults to 0 (no polling)
- `notifyOnNetworkStatusChange`: boolean
  - Whether updates to the network status or network error should re-render your component
  - Defaults to false
- `fetchPolicy`: FetchPolicy

  - How you want your component to interact with the Apollo cache
  - Sometimes, it’s useful to tell Apollo Client to bypass the cache altogether if you have some data that constantly needs to be refreshed
  - Default is `cache-first`
    - It checks the cache to see if the result is there before making a network request
  - Since we want this list to always reflect the newest data from our graph API, we set the `fetchPolicy` for this query to `network-only`
  - <Query query={GET_MY_TRIPS} fetchPolicy="network-only">
            {({ data, loading, error }) => {
              if (loading) return <Loading />;
              if (error) return <p>ERROR: {error.message}</p>;

              return (
                <>
                  ...
                </>
              );
            }}
          </Query>

- `errorPolicy`: ErrorPolicy
  - How you want your component to handle network and GraphQL errors
  - Defaults to “none”, which means we treat GraphQL errors as runtime errors
- `ssr`: boolean
  - Pass in false to skip your query during server-side rendering
- `displayName`: string
  - The name of your component to be displayed in React DevTools
  - Defaults to ‘Query’
- `skip`: boolean
  - If skip is true, the query will be skipped entirely
- `onCompleted`: (data: TData | {}) => void
  - A callback executed once your query successfully completes
- `onError`: (error: ApolloError) => void
  - A callback executed in the event of an error
- `context`: Record<string, any>
  - Shared context between your Query component and your network interface (Apollo Link)
  - Useful for setting headers from props or sending information to the `request` function of Apollo Boost
- `partialRefetch`: boolean
  - If `true`, perform a query `refetch` if the query result is marked as being partial, and the returned data is reset to an empty Object by the Apollo Client `QueryManager` (due to a cache miss)
  - The default value is `false` for backwards-compatibility’s sake, but should be changed to true for most use-cases

### Render Prop function

- https://www.apollographql.com/docs/react/essentials/queries.html#render-prop
- The render prop pattern provides the ability to add a function as a child to our `Query` component that will notify React about what you want to render
- `data`: TData
  - An object containing the result of your GraphQL query
  - Defaults to an empty object
- `loading`: boolean
  - A boolean that indicates whether the request is in flight
- `error`: ApolloError
  - A runtime error with `graphQLErrors` and `networkError` properties
- `variables`: { [key: string]: any }
  - An object containing the variables the query was called with
- `networkStatus`: NetworkStatus
  - A number from 1-8 corresponding to the detailed state of your network request
  - Includes information about refetching and polling status
  - Used in conjunction with the `notifyOnNetworkStatusChange` prop
- `refetch`: (variables?: TVariables) => Promise
  - A function that allows you to refetch the query and optionally pass in new variables
- `fetchMore`: ({ query?: DocumentNode, variables?: TVariables, updateQuery: Function}) => Promise
  - A function that enables pagination for your query
- `startPolling`: (interval: number) => void
  - This function sets up an interval in ms and fetches the query each time the specified interval passes
- `stopPolling`: () => void
  - This function stops the query from polling
- `subscribeToMore`: (options: { document: DocumentNode, variables?: TVariables, updateQuery?: Function, onError?: Function}) => () => void
  - A function that sets up a subscription
  - `subscribeToMore` returns a function that you can use to unsubscribe
- `updateQuery`: (previousResult: TData, options: { variables: TVariables }) => TData
  - A function that allows you to update the query’s result in the cache outside the context of a fetch, mutation, or subscription
- `client`: ApolloClient
  - Your `ApolloClient` instance
  - Useful for manually firing queries or writing data to the cache

### Manual Queries

- To load data every time the user hits a button instead upon the initial load of the component, use `withApollo`
- This function injects the `ApolloClient` instance that you created in `index.js` into a component as a new prop called `client`
- `client` has a method called `query` which you can use to send a query manually instead of using the `graphql` higher-order component

```
import { withApollo } from 'react-apollo';

class Search extends Component {
  state = {
    links: [],
    filter: ''
  };

  render() {
    return (
      <div>
        <div>
          Search
          <input
            type="text"
            onChange={e => this.setState({ filter: e.target.value })}
          />
          <button onClick={() => this._executeSearch()}>OK</button>
        </div>
        {this.state.links.map((link, index) => (
          <Link key={link.id} link={link} index={index} />
        ))}
      </div>
    );
  }

  _executeSearch = async () => {
    const { filter } = this.state;
    const result = await this.props.client.query({
      query: FEED_SEARCH_QUERY,
      variables: { filter }
    });
    const links = result.data.feed.links;
    this.setState({ links });
  };
}

export default withApollo(Search);
```

- Or use `ApolloConsumer`

## Mutations

- The main difference from `Query` is:
  - The first argument to the `Mutation` render prop function is a mutate function that actually triggers the mutation when it is called
  - The second argument to the `Mutation` render prop function is a result object that contains loading and error state, as well as the return value from the mutation
- Process:
  - Write the mutation as a JavaScript constant using the `gql` parser function
  - Use the `<Mutation />` component passing the GraphQL mutation and variables (if needed) as props
  - Use the mutation function that gets injected into the component’s render prop function
- Must define params and their types

```
import { Mutation } from 'react-apollo';
import { gql } from 'apollo-boost';

const LOGIN_USER = gql`
  mutation login($email: String!) {
    login(email: $email)
  }
`;

export default function Login() {
  return (
    <Mutation mutation={LOGIN_USER}>
      {(login, { data }) => <LoginForm login={login} />}
    </Mutation>
  );
}
```

- Our `Mutation` component takes a render prop function as a child that exposes a mutate function (`login`) and the data object returned from the mutation
- Finally, we pass our login function to the `LoginForm` component

### Props

- https://www.apollographql.com/docs/react/essentials/mutations.html#props
- `mutation` and `children` are required
- `mutation`: DocumentNode
  - A GraphQL mutation document parsed into an AST by `graphql-tag`
- `children`: (mutate: Function, result: MutationResult) => React.ReactNode
  - A function that allows you to trigger a mutation from your UI
- `variables`: { [key: string]: any }
  - An object containing all of the variables your mutation needs to execute
  - Passes in the arguments to the mutation function
- `update`: (cache: DataProxy, mutationResult: FetchResult)
  - A function used to update the cache after a mutation occurs
  - Manually update the cache on the client, so it matches the server
  - See update the cache
- `ignoreResults`: boolean
  - If true, the `data` property on the render prop function will not update with the mutation result
- `optimisticResponse`: Object
  - Provide a mutation response before the result comes back from the server
  - Returns the types and fields in the prop immediately instead of waiting for the mutation to complete
  - Give it what you think the server will return
  - Allows for instant UI updating
  - Must use the `update` prop as well and manually update the cache

```
optimisticResponse={{
  __typename: 'Mutation',
  removeFromCart: {
    __typename: 'CartItem',
    id: this.props.id,
  },
}}
```

- `refetchQueries`: (mutationResult: FetchResult) => Array<{ query: DocumentNode, variables?: TVariables} | string>
  - A function that allows you to specify which queries you want to refetch after a mutation has occurred
  - Will perform a query every time a mutation is ran in order to update the page
  - Will refetch data after a mutation completes
  - `refetchQueries**=**{[{ query: CURRENT_USER_QUERY }]}`
- `awaitRefetchQueries`: boolean
  - Queries refetched as part of `refetchQueries` are handled asynchronously, and are not waited on before the mutation is completed (resolved)
  - Setting this to `true` will make sure refetched queries are completed before the mutation is considered done
  - `false` by default
- `onCompleted`: (data: TData) => void
  - A callback executed once your mutation successfully completes
- `onError`: (error: ApolloError) => void
  - A callback executed in the event of an error
- `context`: Record<string, any>
  - Shared context between your Mutation component and your network interface (Apollo Link)
  - Useful for setting headers from props or sending information to the `request` function of Apollo Boost

### Render prop function

- https://www.apollographql.com/docs/react/essentials/mutations.html#render-prop
- `data`: TData
  - The data returned from your mutation
  - It can be undefined if `ignoreResults` is true
- `loading`: boolean
  - A boolean indicating whether your mutation is in flight
- `error`: ApolloError
  - Any errors returned from the mutation
- `called`: boolean
  - A boolean indicating if the mutate function has been called
- `client`: ApolloClient
  - Your `ApolloClient` instance
  - Useful for invoking cache methods outside the context of the update function
    - such as `client.writeData` and `client.readQuery`

## Subscriptions

- https://www.apollographql.com/docs/react/advanced/subscriptions.html#subscriptions-client
- https://www.apollographql.com/docs/graphql-subscriptions/index.html
- Apollo Boost does not support them
- When using Apollo, you need to configure your `ApolloClient` with information about the subscriptions endpoint
- This is done by adding another `ApolloLink` to the Apollo middleware chain
- Import `WebSocketLink` from the `apollo-link-ws` package
- For `apollo-link-ws` to work you also need to install `subscriptions-transport-ws`
- Now create a new `WebSocketLink` that represents the WebSocket connection
- Use `split` for proper “routing” of the requests and update the constructor call of `ApolloClient`
- Update `src/index.js`

```
import { split } from 'apollo-link'
import { WebSocketLink } from 'apollo-link-ws'
import { getMainDefinition } from 'apollo-utilities'

const wsLink = new WebSocketLink({
  uri: `ws://localhost:4000`,
  options: {
    reconnect: true,
    connectionParams: {
      authToken: localStorage.getItem(AUTH_TOKEN),
    }
  }
})

const link = split(
  ({ query }) => {
    const { kind, operation } = getMainDefinition(query)
    return kind === 'OperationDefinition' && operation === 'subscription'
  },
  wsLink,
  authLink.concat(httpLink)
)

const client = new ApolloClient({
  link,
  cache: new InMemoryCache()
})
```

- You’re instantiating a `WebSocketLink` that knows the subscriptions endpoint
  - The subscriptions endpoint in this case is similar to the HTTP endpoint, except that it uses the `ws` instead of `http` protocol
  - You’re also authenticating the websocket connection with the user’s `token` that you retrieve from `localStorage`
- `split` is used to “route” a request to a specific middleware link
  - It takes three arguments:
    - The first one is a `test` function which returns a boolean
    - The remaining two arguments are again of type `ApolloLink`
  - If `test` returns `true`, the request will be forwarded to the link passed as the second argument
  - If `false`, to the third one
  - In this case, the `test` function is checking whether the requested operation is a subscription
  - If this is the case, it will be forwarded to the `wsLink`
  - Otherwise (if it’s a query or mutation), the `authLink.concat(httpLink)` will take care of it
- For the app to update in realtime when new links are created, you need to subscribe to events that are happening on the `Link` type
- There generally are three kinds of events you can subscribe to when using Prisma:
  - a new `Link` is created
  - an existing `Link` is updated
  - an existing `Link` is deleted

```
_subscribeToNewLinks = subscribeToMore => {
  subscribeToMore({
    document: NEW_LINKS_SUBSCRIPTION,
    updateQuery: (prev, { subscriptionData }) => {
      if (!subscriptionData.data) return prev;
      const newLink = subscriptionData.data.newLink;
      const exists = prev.feed.links.find(({ id }) => id === newLink.id);
      if (exists) return prev;

      return Object.assign({}, prev, {
        feed: {
          links: [newLink, ...prev.feed.links],
          count: prev.feed.links.length + 1,
          __typename: prev.feed.__typename
        }
      });
    }
  });
};

<Query query={FEED_QUERY}>
  {({ loading, error, data, subscribeToMore }) => {
    if (loading) return <div>Fetching</div>
    if (error) return <div>Error</div>

    this._subscribeToNewLinks(subscribeToMore)
```

- Use `subscribeToMore` received as prop into the component’s render prop function
- Calling `_subscribeToNewLinks` with the respective `subscribeToMore` function makes sure that the component actually subscribes to the events
  - This call opens up a websocket connection to the subscription server
- You’re passing two arguments to `subscribeToMore`:
  - `document`
    - This represents the subscription query itself
    - In this case, the subscription will fire every time a new link is created
  - `updateQuery`
    - Similar to cache `update` prop
    - This function allows you to determine how the store should be updated with the information that was sent by the server after the event occurred
    - It follows exactly the same principle as a Redux reducer
    - It takes as arguments the previous state (of the query that `subscribeToMore` was called on) and the subscription data that’s sent by the server
    - You can then determine how to merge the subscription data into the existing state and return the updated data
    - All you’re doing inside `updateQuery` is retrieve the new link from the received `subscriptionData`, merge it into the existing list of links and return the result of this operation

## Cache

- https://www.apollographql.com/docs/react/advanced/caching.html
- https://www.apollographql.com/docs/react/essentials/mutations.html#update
- Includes zero-config caching
- Since you can have multiple paths leading to the same data, normalization is essential for keeping your data consistent across multiple components
- When performing a mutation, Apollo Client splits out each object in a GraphQL result with a `__typename` and an `id` property into its own entry in the Apollo cache
- This guarantees that returning a value from a mutation with an `id` will automatically update any queries that fetch the object with the same `id`
- It also ensures that two queries which return the same data will always be in sync

### Redirects

- If we want to transition to a detail page for a specific item we’ve already fetched information on, we don’t want to refetch the same information from our server
- cache redirects, the Apollo cache lets us connect the dots between two queries so we don’t have to fetch information that we know is already available
- Specify a map on the `cacheRedirects` property of the `apollo-boost` client
  - Returns a key that the query can use to look up the data in the cache

```
// Query
const GET_DOG = gql`
  query {
    dog(id: "abc") {
      id
      breed
      displayImage
    }
  }
`;
```

```
import ApolloClient from 'apollo-boost';

const client = new ApolloClient({
  cacheRedirects: {
    Query: {
      dog: (_, { id }, { getCacheKey }) => getCacheKey({ id, __typename: 'Dog' })
    }
  }
})
```

### Updating

- Sometimes when you perform a mutation, your GraphQL server and your Apollo cache become out of sync
- This happens when the update you’re performing depends on data that is already in the cache
  - For example, deleting and adding items to a list
- Not every mutation requires an update function
  - If you’re updating a single item, you usually don’t need an update function as long as you return the item’s `id` and the property you updated
- There are two ways to perform mutations in `apollo-link-state`
  - Direct writes
    - Directly writing to the cache by calling `cache.writeData` within an `ApolloConsumer` or `Query` component
    - Great for one-off mutations that don’t depend on the data that’s currently in the cache
      - such as writing a single value

```
import { ApolloConsumer } from 'react-apollo';

import Link from './Link';

const FilterLink = ({ filter, children }) => (
  <ApolloConsumer>
    {client => (
      <Link
        onClick={() => client.writeData({ data: { visibilityFilter: filter } })}
      >
        {children}
      </Link>
    )}
  </ApolloConsumer>
);
```

    * Resolvers
        * Creating a `Mutation` component with a GraphQL mutation that calls a client-side resolver
        * Use resolvers if your mutation depends on existing values in the cache
            * such as adding an item to a list or toggling a boolean
    * You can think of direct writes like calling `setState`, whereas resolvers offer a bit more structure like Redux

- The `<Mutation>` component has an optional `update` prop
  - A way to tell Apollo Client to update the query for the list of items
- You have to use a query to read and write to cache

```
import { ALL_ITEMS_QUERY } from './PathToQuery';

update = (cache, payload) => {
  // manually update the cache on the client, so it matches the server
  // 1. Read the cache for the items we want
  //    just export the all items query where it lives, and import it here
  const data = cache.readQuery({ query: ALL_ITEMS_QUERY });
  // 2. Filter the deleted item out of the page
  data.items = data.items.filter(
    item => item.id !== payload.data.deleteItem.id
  );
  // 3. Put the items back!
  cache.writeQuery({ query: ALL_ITEMS_QUERY, data });
};

<Mutation
  mutation={DELETE_ITEM_MUTATION}
  variables={{ id: this.props.id }}
  update={this.update}>
  {...function}
</Mutation>
```

### Manual

- You can manually control the contents of the cache
- Useful after a mutation is performed
- It allows to precisely determine how you want the cache to be updated

```
// Links.js
<Mutation
  mutation={VOTE_MUTATION}
  variables={{ linkId: this.props.link.id }}
  update={(store, { data: { vote } }) =>
    this.props.updateStoreAfterVote(store, vote, this.props.link.id)
  }
>
  {voteMutation => (
    <div className="ml1 gray f11" onClick={voteMutation}>
      ▲
    </div>
  )}
</Mutation>
```

- The `update` function will be called directly after the server returned the response
- It receives the payload of the mutation (`data`) and the current cache (`store`) as arguments
- You can then use this input to determine a new state for the cache

```
// LinkList.js
_updateCacheAfterVote = (store, createVote, linkId) => {
  const data = store.readQuery({ query: FEED_QUERY })

  const votedLink = data.feed.links.find(link => link.id === linkId)
  votedLink.votes = createVote.link.votes

  store.writeQuery({ query: FEED_QUERY, data })
}
```

- You start by reading the current state of the cached data for the `FEED_QUERY` from the `store`
- Now you’re retrieving the link that the user just voted for from that list
- You’re also manipulating that link by resetting its `votes` to the `votes` that were just returned by the server
- Finally, you take the modified data and write it back into the store
- The store update will trigger a rerender of the component and thus update the UI with the correct information

## Local State

- https://www.apollographql.com/docs/react/essentials/local-state.html
- Manage local state with `apollo-link-state`
- Allows you to use your Apollo cache as the single source of truth for data in your application
- Enables you to inspect both your local and remote schemas in Apollo DevTools
- You can add client-side only fields to your remote data seamlessly and query them from your components
  - by specifying the `@client` directive
- Managing local data with Apollo Client is very similar to how you manage remote data
  - You write a client schema and resolvers for your local data

### Write a local schema

- Writing a local schema is the first step we take on the client
- To build a client schema, we extend the types of our server schema and wrap it with the `gql` function
  - Using the `extend` keyword allows us to combine both schemas inside developer tooling
    - Apollo VSCode and Apollo DevTools
- Create `src/resolvers.js`

```
import gql from 'graphql-tag';

export const typeDefs = gql`
  extend type Query {
    isLoggedIn: Boolean!
    cartItems: [Launch]!
  }

  extend type Launch {
    isInCart: Boolean!
  }

  extend type Mutation {
    addOrRemoveFromCart(id: ID!): [Launch]
  }
`;
```

- We can also add local fields to server data by extending types from our server
- Here, we’re adding the `isInCart` local field to the `Launch` type we receive back from our graph API

### Initialize the store

- Since queries execute as soon as the component mounts, it’s important for us to warm the Apollo cache with some default state so those queries don’t error out
- In `src/index.js`, add a `cache.writeData` call to prepare the cache

```
const client = new ApolloClient({
  cache,
  link: new HttpLink({
    uri: 'http://localhost:4000/graphql',
    headers: {
      authorization: localStorage.getItem('token'),
    },
  }),
});

cache.writeData({
  data: {
    isLoggedIn: !!localStorage.getItem('token'),
    cartItems: [],
  },
});
```

- Now we’ve added default state to the Apollo cache

### Query local data

- The only difference from querying remote data is that you add a `@client` directive to a local field to tell Apollo Client to pull it from the cache

```
import { Query, ApolloProvider } from 'react-apollo';
import gql from 'graphql-tag';

import Pages from './pages';
import Login from './pages/login';

const IS_LOGGED_IN = gql`
  query IsUserLoggedIn {
    isLoggedIn @client
  }
`;

injectStyles();
ReactDOM.render(
  <ApolloProvider client={client}>
    <Query query={IS_LOGGED_IN}>
      {({ data }) => (data.isLoggedIn ? <Pages /> : <Login />)}
    </Query>
  </ApolloProvider>,
  document.getElementById('root'),
);
```

- First, we create our `IsUserLoggedIn` local query by adding the `@client` directive to the `isLoggedIn` field
- Then, we render a `Query` component, pass our local query in, and specify a render prop function
  - Renders either a login screen or the homepage depending if the user is logged in
- Since cache reads are synchronous, we don’t have to account for any loading state

### Adding virtual fields to server data

- One of the unique advantages of managing your local data with Apollo Client is that you can add virtual fields to data you receive back from your graph API
- These fields only exist on the client
- Useful for decorating server data with local state
- To add a virtual field:
- First extend the type of the data you’re adding the field to in your client schema
- In `src/resolvers.js`

```
import gql from 'graphql-tag';

export const typeDefs = gql`
  extend type Launch {
    isInCart: Boolean!
  }
`;
```

- Next, specify a client resolver on the `Launch` type to tell Apollo Client how to resolve your virtual field

```
export const resolvers = {
  Launch: {
    isInCart: (launch, _, { cache }) => {
      const { cartItems } = cache.readQuery({ query: GET_CART_ITEMS });
      return cartItems.includes(launch.id);
    },
  }
};
```

- The resolver API on the client must be the same as the resolver API on the server

### Update local data

- Apollo Client also lets you update local data in the cache with either direct cache writes or client resolvers
  - Direct cache writes are convenient when you want to write a simple field, like a boolean or a string, to the Apollo cache
  - Client resolvers are for more complicated writes such as adding or removing data from a list

### Direct cache writes

- We perform a direct write by calling `client.writeData()`
- Pass in an object with a data property that corresponds to the data we want to write to the cache

```
import React from 'react';
import styled from 'react-emotion';
import { ApolloConsumer } from 'react-apollo';

import { menuItemClassName } from '../components/menu-item';
import { ReactComponent as ExitIcon } from '../assets/icons/exit.svg';

export default function LogoutButton() {
  return (
    <ApolloConsumer>
      {client => (
        <StyledButton
          onClick={() => {
            client.writeData({ data: { isLoggedIn: false } });
            localStorage.clear();
          }}
        >
          <ExitIcon />
          Logout
        </StyledButton>
      )}
    </ApolloConsumer>
  );
}
```

- We can also perform direct writes within the `update` function of a `Mutation` component
- The `update` function allows us to manually update the cache after a mutation occurs without refetching data

```
import React from 'react';
import { Mutation } from 'react-apollo';
import gql from 'graphql-tag';

import Button from '../components/button';
import { GET_LAUNCH } from './cart-item';

const BOOK_TRIPS = gql`
  mutation BookTrips($launchIds: [ID]!) {
    bookTrips(launchIds: $launchIds) {
      success
      message
      launches {
        id
        isBooked
      }
    }
  }
`;

export default function BookTrips({ cartItems }) {
  return (
    <Mutation
      mutation={BOOK_TRIPS}
      variables={{ launchIds: cartItems }}
      refetchQueries={cartItems.map(launchId => ({
        query: GET_LAUNCH,
        variables: { launchId },
      }))}
      update={cache => {
        cache.writeData({ data: { cartItems: [] } });
      }}
    >
      {(bookTrips, { data, loading, error }) =>
        data && data.bookTrips && !data.bookTrips.success ? (
          <p data-testid="message">{data.bookTrips.message}</p>
        ) : (
          <Button onClick={bookTrips} data-testid="book-button">
            Book All
          </Button>
        )
      }
    </Mutation>
  );
}
```

- We’re directly calling `cache.writeData` to reset the state of the `cartItems` after the `BookTrips` mutation is sent to the server
- This direct write is performed inside of the update function, which is passed our Apollo Client instance

### Local resolvers

- What if we wanted to perform a more complicated local data update such as adding or removing items from a list?
- Local resolvers have the same function signature as remote resolvers
  - (`(parent, args, context, info) => data`)
- The only difference is that the Apollo cache is already added to the context for you
- Inside your resolver, you’ll use the cache to read and write data

```
export const resolvers = {
  Mutation: {
    addOrRemoveFromCart: (_, { id }, { cache }) => {
      const { cartItems } = cache.readQuery({ query: GET_CART_ITEMS });
      const data = {
        cartItems: cartItems.includes(id)
          ? cartItems.filter(i => i !== id)
          : [...cartItems, id],
      };
      cache.writeQuery({ query: GET_CART_ITEMS, data });
      return data.cartItems;
    },
  },
};
```

- In this resolver, we destructure the Apollo `cache` from the context in order to read the query that fetches cart items
- Once we have our cart data, we either remove or add the cart item’s `id` passed into the mutation to the list
- Finally, we return the updated list from the mutation
- We call the `addOrRemoveFromCart` mutation in a component like so

```
import gql from 'graphql-tag';

const TOGGLE_CART = gql`
  mutation addOrRemoveFromCart($launchId: ID!) {
    addOrRemoveFromCart(id: $launchId) @client
  }
`;
```

```
export default function ActionButton({ isBooked, id, isInCart }) {
  return (
    <Mutation
      mutation={isBooked ? CANCEL_TRIP : TOGGLE_CART}
      variables={{ launchId: id }}
      refetchQueries={[
        {
          query: GET_LAUNCH_DETAILS,
          variables: { launchId: id },
        },
      ]}
    >
      {(mutate, { loading, error }) => {
        if (loading) return <p>Loading...</p>;
        if (error) return <p>An error occurred</p>;

        return (
          <div>
            <Button
              onClick={mutate}
              isBooked={isBooked}
              data-testid={'action-button'}
            >
              {isBooked
                ? 'Cancel This Trip'
                : isInCart
                  ? 'Remove from Cart'
                  : 'Add to Cart'}
            </Button>
          </div>
        );
      }}
    </Mutation>
  );
}
```

## Connections

- Special queries created for every type in the schema
- Returns aggregate data about the data

## Link

- https://www.apollographql.com/docs/link/overview
- A link is a function that takes an operation and returns an observable
- Apollo Link is a standard interface for modifying control flow of GraphQL requests and fetching GraphQL results
- Allow you to create `middlewares` that let you modify requests before they are sent to the server
- The middleware will be invoked every time `ApolloClient` sends a request to the server
- An operation is an object with the following information:
  - `query`: A `DocumentNode` (parsed GraphQL Operation) describing the operation taking place
  - `variables`: A map of variables being sent with the operation
  - `operationName`: A string name of the query if it is named, otherwise it is null
  - `extensions`: A map to store extensions data to be sent to the server
  - `getContext`: A function to return the context of the request
    - This context can be used by links to determine which actions to perform.
  - `setContext`: A function that takes either a new context object, or a function which receives the previous context and returns a new one
    - It behaves similarly to `setState` from React.
  - `toKey`: A function to convert the current operation into a string to be used as a unique identifier

### Request

- At the core of a link is the `request` method
- It takes the following arguments:
  - `operation`: The operation being passed through the link
  - `forward`: (optional) Specifies the next link in the chain of links

### Context

- Since links are meant to be composed, they need an easy way to send metadata about the request down the chain of links
- They also need a way for the operation to send specific information to a link no matter where it was added to the chain
- Each `Operation` has a `context` object which can be set from the operation while being written and read by each link
- The `context` is not sent to the server, but is used for link to link communication

## Authentication

### Client side

- https://www.apollographql.com/docs/react/recipes/authentication.html
- Since all the API requests are actually created and sent by the `ApolloClient` instance in your app, you need to make sure it knows about the user’s token
- Using `apollo-link-context`:
- In `index.js`, put between the creation of the `httpLink` and the instantiation of `ApolloClient`
  - Don't actually use LocalStorage for auth tokens

```
import { setContext } from 'apollo-link-context'
import { AUTH_TOKEN } from './constants'

const authLink = setContext((_, { headers }) => {
  const token = localStorage.getItem(AUTH_TOKEN)
  return {
    headers: {
      ...headers,
      authorization: token ? `Bearer ${token}` : ''
    }
  }
})
```

- Make sure `ApolloClient` gets instantiated with the correct link

```
const client = new ApolloClient({
  link: authLink.concat(httpLink),
  cache: new InMemoryCache()
})
```

- Now all your API requests will be authenticated if a `token` is available
- --- or ---
- Attach authorization headers to the request:
- We need to attach our token to the GraphQL request’s headers so our server can authorize the user
- To do this, navigate to `src/index.js` where we create our `ApolloClient`

```
const client = new ApolloClient({
  cache,
  link: new HttpLink({
    uri: 'http://localhost:4000/graphql',
    headers: {
      authorization: localStorage.getItem('token'),
    },
  }),
  resolvers,
  typeDefs,
});
```

- Specifying the `headers` option on `HttpLink` allows us to read the token from `localStorage` and attach it to the request’s headers each time a GraphQL operation is made

### Server side

- Represent user data in the database by adding a `User` type
- Ensure only authenticated users are able to `post` new links
- Plus, every `Link` that’s created by a `post` mutation should automatically set the `User` who sent the request for its `postedBy` field
- in `resolvers/Mutation.js`

```
function post(parent, { url, description }, ctx, info) {
  const userId = getUserId(ctx)
  return ctx.db.mutation.createLink(
    { data: { url, description, postedBy: { connect: { id: userId } } } },
    info,
  )
}
```

- With this, you’re extracting the `userId` from the `Authorization` header of the request and use it to directly `connect` it with the `Link` that’s created
- Note that `getUserId` will throw an error if the field is not provided or not valid token could be extracted.

## Pagination

- https://www.apollographql.com/docs/react/features/pagination.html

```
export const FEED_QUERY = gql`
  query FeedQuery($first: Int, $skip: Int, $orderBy: LinkOrderByInput) {
    feed(first: $first, skip: $skip, orderBy: $orderBy) {
      links {
        id
        createdAt
        url
        description
        postedBy {
          id
          name
        }
        votes {
          id
          user {
            id
          }
        }
      }
      count
    }
  }
`
```

- The query accepts arguments that we’ll use to implement pagination and ordering:
  - `skip` defines the offset where the query will start
    - If you passed a value of e.g. `10` for this argument, it means that the first 10 items of the list will not be included in the response
  - `first` then defines the limit, or how many elements, you want to load from that list
    - Say, you’re passing the `10` for `skip` and `5` for `first`, you’ll receive items 10 to 15 from the list
  - `orderBy` defines how the returned list should be sorted

```
const LINKS_PER_PAGE = 5

_getQueryVariables = () => {
  const isNewPage = this.props.location.pathname.includes('new')
  const page = parseInt(this.props.match.params.page, 10)

  const skip = isNewPage ? (page - 1) * LINKS_PER_PAGE : 0
  const first = isNewPage ? LINKS_PER_PAGE : 100
  const orderBy = isNewPage ? 'createdAt_DESC' : null
  return { first, skip, orderBy }
}
```

```
`<Query query={FEED_QUERY} variables={this._getQueryVariables()}>`
```

- You’re now passing `first, skip, orderBy` values as `variables` based on the current page (`this.props.match.params.page`) which it’s used to calculate the chunk of links that you retrieve

### fetchMore

- Apollo Client has built-in helpers to make adding pagination to our app much easier than it would be if we were writing the logic ourselves
- To build a paginated list with Apollo, we first need to destructure the `fetchMore` function from the `Query` render prop function

```
export default function Launches() {
  return (
    <Query query={GET_LAUNCHES}>
      {({ data, loading, error, fetchMore }) => {
        // same as above
      }}
    </Query>
  );
};
```

- Connect `fetchMore` to a “Load More” button to fetch more items when it’s clicked
- We will need to specify an `updateQuery` function on the return object from `fetchMore` that tells the Apollo cache how to update our query with the new items we’re fetching

```
{data.launches &&
  data.launches.hasMore && (
    <Button
      onClick={() =>
        fetchMore({
          variables: {
            after: data.launches.cursor,
          },
          updateQuery: (prev, { fetchMoreResult, ...rest }) => {
            if (!fetchMoreResult) return prev;
            return {
              ...fetchMoreResult,
              launches: {
                ...fetchMoreResult.launches,
                launches: [
                  ...prev.launches.launches,
                  ...fetchMoreResult.launches.launches,
                ],
              },
            };
          },
        })
      }
    >
      Load More
    </Button>
  )
}
```

- First, we check to see if we have more launches available in our query
  - If we do, we render a button with a click handler that calls the `fetchMore` function from Apollo
  - The `fetchMore` function receives new variables for the list of launches query, which is represented by our cursor
- We also define the `updateQuery` function to tell Apollo how to update the list of launches in the cache
  - To do this, we take the previous query result and combine it with the new query result from `fetchMore`

## Fragments

- When we have two GraphQL operations that contain the same fields, we can use a **fragment** to share fields between the two
- We define a GraphQL fragment by giving it a name (`LaunchTile`) and defining it on a type on our schema (`Launch`)
- The name we give our fragment can be anything, but the type must correspond to a type in our schema

```
export const LAUNCH_TILE_DATA = gql`
  fragment LaunchTile on Launch {
    id
    isBooked
    rocket {
      id
      name
    }
    mission {
      name
      missionPatch
    }
  }
`;
```

- To use our fragment in our query, we import it into the GraphQL document and use the spread operator to spread the fields into our query

```
const GET_LAUNCHES = gql`
  query launchList($after: String) {
    launches(after: $after) {
      cursor
      hasMore
      launches {
        ...LaunchTile
      }
    }
  }
  ${LAUNCH_TILE_DATA}
`;
```

---

# _Apollo Boost_

- `npm i apollo-boost graphql react-apollo -S`
- A zero-config way to start using Apollo Client
- Includes some packages that we think are essential to developing with Apollo Client:
  - `apollo-client`
    - Options you can pass to the `ApolloClient` exported from `apollo-boost`:
      - `uri`
      - `fetchOptions`
      - `request`
      - `onError`
      - `clientState`
      - `cacheRedirects`
      - `credentials`
      - `headers`
      - `fetch`
      - `cache`
  - `apollo-cache-inmemory`
  - `apollo-link-http`
  - `apollo-link-error`
  - `apollo-link-state`
  - `graphql-tag`

---

# _Official packages_

## apollo-client

- https://github.com/apollographql/apollo-client
- Where all the magic happens
- Options you can pass to the `ApolloClient`
  - `uri`: string
    - A string representing your GraphQL server endpoint.
    - Defaults to `/graphql`
  - `fetchOptions`: Object
    - Any options you would like to pass to fetch (credentials, headers, etc).
    - These options are static, so they don’t change on each request.
  - `request`: (operation: Operation) => Promise
    - This function is called on each request.
    - It takes a GraphQL operation and can return a promise.
    - To dynamically set `fetchOptions`, you can add them to the context of the operation with `operation.setContext({ headers })`.
    - Any options set here will take precedence over `fetchOptions`.
    - Useful for authentication.
  - `onError`: (errorObj: { graphQLErrors: GraphQLError[], networkError: Error, response?: ExecutionResult, operation: Operation }) => void
    - We include a default error handler to log out your errors to the console.
    - If you would like to handle your errors differently, specify this function.
  - `clientState`: { resolvers?: Object, defaults?: Object, typeDefs?: string | Array }
    - An object representing your configuration for `apollo-link-state`.
    - This is useful if you would like to use the Apollo cache for local state management.
    - Learn more in our [quick start](https://www.apollographql.com/docs/link/links/state.html#start).
  - `cacheRedirects`: Object
    - A map of functions to redirect a query to another entry in the cache before a request takes place.
    - This is useful if you have a list of items and want to use the data from the list query on a detail page where you’re querying an individual item.
    - More on that [here](https://www.apollographql.com/docs/react/features/performance.html#cache-redirects).
  - `credentials`: string
    - Is set to `same-origin` by default.
    - This option can be used to indicate whether the user agent should send cookies with requests.
    - See [Request.credentials](https://developer.mozilla.org/en-US/docs/Web/API/Request/credentials) for more details.
  - `headers`: Object
    - Header key/value pairs to pass along with the request.
  - `fetch`: GlobalFetch[‘fetch’]
    - A [`fetch`](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) compatible API for making a request.
  - `cache`: ApolloCache
    - A custom instance of `ApolloCache` to be used.
    - The default value is `InMemoryCache` from `apollo-cache-inmemory`.
    - This option is quite useful for using a custom cache with `apollo-cache-persist`.

## graphql-tag

- https://github.com/apollographql/graphql-tag
- Exports the `gql` function for your queries & mutations

## apollo-cache-inmemory

- https://github.com/apollographql/apollo-client/tree/master/packages/apollo-cache-inmemory
- `npm install apollo-cache-inmemory --save`
- The recommended cache implementation for Apollo Client 2.0
- Normalizes your data before saving it to the store by splitting the result into individual objects, creating a unique identifier for each object, and storing those objects in a flattened data structure
- To interact directly with your cache, you can use the Apollo Client class methods:
  - `readQuery`
  - `readFragment`
  - `writeQuery`
  - `writeFragment`

## apollo-link-http

- https://www.apollographql.com/docs/link/links/http.html
- Get GraphQL results over a network using HTTP fetch
- An Apollo Link for remote data fetching

## apollo-link-error

- https://www.apollographql.com/docs/link/links/error.html
- Handle and inspect errors in your GraphQL network stack
- An Apollo Link for error handling

## apollo-link-state

- https://www.apollographql.com/docs/link/links/state.html
- Manage your local data with Apollo Client
- An Apollo Link for local state management

## apollo-link-rest

- https://www.apollographql.com/docs/link/links/rest.html
- Call your REST APIs inside your GraphQL queries

## apollo-link-context

- https://www.apollographql.com/docs/link/links/context.html
- Easily set a context on your operation, which is used by other links further down the chain
- It receives two arguments:
  - The GraphQL request being executed
  - The previous context
- This link makes it easy to perform async look up of things like authentication tokens and more

## apollo-link-retry

- https://www.apollographql.com/docs/link/links/retry.html
- Attempt an operation multiple times if it fails due to network or server errors

## apollo-link-ws

- https://www.apollographql.com/docs/link/links/ws.html
- Send GraphQL operations over a WebSocket
- Works with GraphQL Subscriptions
- For `apollo-link-ws` to work you also need to install `subscriptions-transport-ws`

## apollo-link-batch-http

- https://www.apollographql.com/docs/link/links/batch-http.html
- Batch multiple operations into a single HTTP request

## apollo-link-dedup

- https://www.apollographql.com/docs/link/links/dedup.html
- Deduplicate matching requests before making a request

## apollo-link-schema

- https://www.apollographql.com/docs/link/links/schema.html
- Assists with mocking and server-side rendering

---

# _React Apollo_

- https://github.com/apollographql/react-apollo
- Apollo Client integration for React
- React Apollo allows you to fetch data from your GraphQL server and use it in building complex and reactive UIs using the React framework
- One of the main functions of `react-apollo` is that it puts your `ApolloClient` instance on React’s context

## ApolloProvider

- To connect Apollo Client to React, you will need to use the `ApolloProvider` component
- Put it somewhere high in your app, above any places where you need to access GraphQL data
  - Outside of your root route component if you’re using React Router
- It wraps your React app and places the client on the context

## ApolloConsumer

- Exposes the client so when can call queries/mutations at will
  - Instead of being automatically called on render
- This is just like the `withApollo` HOC, just in a normal React component
- Similar to the `Consumer` component from the new React context API
- Expects a child function which receives the instance of Apollo Client in your tree
- Allows you to access it from anywhere in your component tree
- From the client instance, you can directly call `client.writeData` and pass in the data you’d like to write to the cache

```
const MyClient = () => (
  <ApolloConsumer>
    {(client) => (
      <div>
        <h1>The current cache is:</h1>
        <pre>{client.extract()}</pre>
      </div>
    )}
  </ApolloConsumer>
)
```

```
import { ApolloConsumer } from 'react-apollo';

onChange = debounce(async (e, client) => {
  this.setState({ loading: true });
  const res = await client.query({
    query: SEARCH_ITEMS_QUERY,
    variables: { searchTerm: e.target.value },
  });
  this.setState({
    items: res.data.items,
    loading: false,
  });
}, 350);

<ApolloConsumer>
  {client => (
    <input
      type="search"
      onChange={e => {
        e.persist();
        this.onChange(e, client);
      }}
    />
  )}
</ApolloConsumer>
```

## Components

- To connect Apollo Client to React, you will need to use the `ApolloProvider` component exported from `react-apollo`
  - The `ApolloProvider` is similar to React’s context provider
  - It wraps your React app and places the client on the context, which allows you to access it from anywhere in your component tree
- Use the React render prop API to request data

```
const Feed = () => (
  <Query query={GET_DOGS}>
    {({ loading, error, data }) => {
      if (error) return <Error />
      if (loading || !data) return <Fetching />;

      return <DogList dogs={data.dogs} />
    }}
  </Query>
)
```

- Create a `<Mutation>` component
  - Pass in your mutation as a prop
- Same as `<Query>`, the child can only be a function
- Wrap in the function, the part of the component that needs access to the mutation, and loading and error states

```
<Mutation mutation={CREATE_ITEM_MUTATION} variables={this.state}>
  {(createItem, { loading, error }) => (
    <Form
      onSubmit={async e => {
        e.preventDefault();
        const res = await createItem();
        Router.push({
          pathname: '/item',
          query: { id: res.data.createItem.id }
        });
      }}>
      <Error error={error} />
      <fieldset disabled={loading} aria-busy={loading}>
        <label htmlFor="title">
          Title
          <input
            type="text"
            id="title"
            name="title"
            placeholder="Title"
            required
            value={this.state.title}
            onChange={this.handleChange}
          />
        </label>
        <label htmlFor="description">
          Description
          <textarea
            id="description"
            name="description"
            placeholder="Enter A Description"
            required
            value={this.state.description}
            onChange={this.handleChange}
          />
        </label>
        <button type="submit">Submit</button>
      </fieldset>
    </Form>
  )}
</Mutation>
```

---

# _Libraries_

## Community Links

- https://www.apollographql.com/docs/link/links/community.html

## apollo-cache-persist

- Simple persistence for all Apollo Cache implementations
- https://github.com/apollographql/apollo-cache-persist

## _Testing_

### jest-transform-graphql

- `graphql-tag` loader for Webpack lets you keep GraphQL queries in separate files
- This lib makes those work in Jest
- https://github.com/remind101/jest-transform-graphql

---
