---
'apollo-angular': minor
---

Improve the return type of client.watchFragment in regard of `errorPolicy`

Improves the return type of `client.query` to be smarter about the
applied `errorPolicy`. The `data` and `error` properties now better
reflect the expected runtime value for a given `errorPolicy`.

This allows the removal of `undefined` checks or optional chaining for
most uses of `client.query`.

> [!NOTE]
> The `ApolloClient.QueryResult` type is used in several places
throughout the code base, most of which do not know the underlying
`errorPolicy` applied (e.g. `refetchQueries`, which might have a mix of
`ObservableQuery` instances with different error policies). As such, I
left a fallback case that leaves the type as-is. You need to be explicit
about an error policy in order to get the smarter types.

See equivalent in Apollo Client: https://github.com/apollographql/apollo-client/pull/13130
