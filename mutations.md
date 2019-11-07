## Mutations

First, use a mutation to create a new repository:

```graphql
mutation {
  createRepository(input: {name: "AwesomeRepo", description: "This repository was created using a GraphQL request", visibility: PUBLIC}) {
    repository {
      id
    }
  }
}
```

The id that is returned here needs to be used in the following steps!

Now add an issue to that repository:

```graphql
mutation {
  createIssue(input: {repositoryId: "repository-id-string", title: "Generating things on GitHub via the API", body: "This issue was created using a GraphQL mutation"}) {
    issue {
      id
    }
  }
}
```

Again we are grabbing the id of the created item. An issue in this case. Because we need to use that in the next couple of mutations.

Add a reaction to that issue :rocket:

```graphql
mutation {
  addReaction(input: {subjectId: "issue-id-string", content: ROCKET}) {
    subject {
      id
      ... on Issue {
        url
      }
    }
    reaction {
      user {
        login
      }
      content
    }
  }
}
```

Finally, also add a comment

```graphql
mutation {
  addComment(input: {subjectId: "MDU6SXNzdWU1MTkxNjkzMjc=", body: "Commenting on the issue, also via the API. Because GraphQL is fun 😁"}) {
    commentEdge {
      node {
        author {
          login
          url
        }
        createdAt
        bodyHTML
        url
      }
    }
  }
}
```

Returning the URLs from the addition of an emoji reaction and a comment makes it very simple to then load that page in the browser and see for yourself what has been created in the GitHub UI :+1:
