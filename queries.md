## Queries


1. How long have you had your GitHub account?

```graphql
query { 
  viewer { 
    login
    name
    createdAt
    databaseId
  }
}
```

2. Which repositories have you starred?

```graphql
query { 
  viewer {
    login
    starredRepositories(first: 50) {
      nodes {
        nameWithOwner
      }
      pageInfo {
        hasNextPage
        endCursor
      }
      totalCount
    }
  }
}
```

You can then page using the `endCursor`

```graphql
query { 
  viewer {
    login
    starredRepositories(first: 50, after: "L9tyc29bOnYyOpHO3ltnnw==") {
      nodes {
        nameWithOwner
      }
      pageInfo {
        hasNextPage
        endCursor
      }
      totalCount
    }
  }
}
```

3. Which was your first (created) repository on GitHub?

```graphql
{
  viewer {
    repositories (
      isFork: false,
      first: 1,
      orderBy: { field: CREATED_AT, direction: ASC },
      ownerAffiliations: OWNER
    ) {
      nodes {
        nameWithOwner
        createdAt
      }
		}
  }
}
```

4. Does anyone follow you and do you follow anyone on GitHub?

```graphql
query {
  viewer {
    followers(first: 20) {
      totalCount
      nodes {
        login
      }
      pageInfo {
      	endCursor
        hasNextPage
      }
    }
    following(first: 20) {
      totalCount
      nodes {
        login
      }
      pageInfo {
        hasNextPage
      }
    }
  }
}
```

Again the `endCursor` can be used for paging:

```graphql
query {
  viewer {
    followers(first: 20, after: "Gp3WM29yOnYyOpkG8UAxNi0wMy0yNFQwNDowMDoyNiswMDowMM34M9G3") {
      totalCount
      nodes {
        login
      }
      pageInfo {
      	endCursor
        hasNextPage
      }
    }
  }
}
```

5. Which items have you pinned?

```graphql
query { 
  viewer {
    login
    pinnedItems(first: 10) {
      nodes {
        ... on Gist {
          name
          description
          owner {
            login
          }
          
        }
        ... on Repository {
          nameWithOwner
          description
        }
      }
      totalCount
    }
    pinnedItemsRemaining
  }
}
```

6. What repositories do you have? For each one is it a fork?

```graphql
query {
  viewer {
    repositories(first: 20) {
      totalCount
      nodes {
        nameWithOwner
        isFork
      }
      pageInfo {
        endCursor
      }
    }
  }
}
```

7. Who else has also contributed to those repositories?

```graphql
query {
  viewer {
    repositories(first: 20) {
      totalCount
      nodes {
        nameWithOwner
        isFork
        collaborators(first: 20, affiliation: ALL) {
          totalCount
          nodes {
            name
            login
          }
          pageInfo {
            endCursor
          }
        }
      }
      pageInfo {
        endCursor
      }
    }
  }
}
```

8. Which organisations do you belong to?

```graphql
query {
  viewer {
    organizations(first: 20) {
      totalCount
      nodes {
        name
      }
	  }
  }
}
```

9. Do you have any pull requests you need to review?

```graphql
query {
  viewer {
    pullRequests(first: 20 states: [OPEN]) {
      totalCount
      nodes {
        title
        reviewRequests(first: 10) {
          nodes {
            requestedReviewer {
              ... on User {
                login
              }
              ... on Team {
                name
              }
            }
          }
        }
      }      
    }
  }
}
```

10. Are you assigned any issues at the moment?

```graphql
query {
  viewer {
    issues(first: 20 states: [OPEN]) {
      totalCount
      nodes {
        title
        assignees(first: 10) {
          nodes {
            login
          }
        }
      }      
	    pageInfo {
  	    hasNextPage
    	  endCursor
    	}
    }
  }
}
```

But for both (9) and (1) there is a better way. Via the search object!

```graphql
query {
  # or "is:open archived:false assignee:username"
  search(first: 20, type: ISSUE, query: "is:open review-requested:username archived:false") {
    nodes {
      __typename
      ... on Issue {
        title
      }
      ... on PullRequest {
        title
      }
    }
    pageInfo {
      hasNextPage
      endCursor
    }
  }
}
```
