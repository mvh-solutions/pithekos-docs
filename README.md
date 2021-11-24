# proskomma-docs
Documentation for the Proskomma Ecosystem

## To generate GraphQL documentation

- update proskomma-node-express to latest Proskomma
- `npm dev run`
- delete source/_static/schema
- In another session: `graphdoc -e http://localhost:2468/gql -o ./source/_static/schema/`

## To build the documentation

