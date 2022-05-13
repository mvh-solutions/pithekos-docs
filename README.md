# proskomma-docs
Documentation for the Proskomma Ecosystem

## To generate GraphQL documentation

- update diegesis-apollo-sandbox to latest Proskomma
- `node index.js`
- delete source/_static/schema
- In another session: `graphdoc -e http://localhost:2468/gql -o ./source/_static/schema/`

## To build documentation locally
`make html`
