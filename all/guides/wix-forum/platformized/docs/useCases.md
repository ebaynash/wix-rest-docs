SortOrder: 2
# Use cases

This articles shares some possible uses of the Forum API endpoints and their respective responses.

## Post API
### Get a Post by ID or by Slug

To get a specific post, use [Get Post](https://dev.wix.com/api/rest/community/wix-forum/post/get-post) to retrieve a post by its ID:

```
curl 'https://www.wixapis.com/forum/v1/posts/5cacd5fe04976c0015f35363' -H 'Content-Type: application/json' -H 'Authorization: <AUTH>'
```


Another option for retrieving a specific post is by using [Get Post by Slug](https://dev.wix.com/api/rest/community/wix-forum/post/get-post-by-slug-by-slug):

```
curl 'https://www.wixapis.com/forum/v1/posts/slugs/welcome-to-the-forum' -H 'Content-Type: application/json' -H 'Authorization: <AUTH>'
```

An example response to both [Get Post](https://dev.wix.com/api/rest/community/wix-forum/post/get-post) and [Get Post by Slug](https://dev.wix.com/api/rest/community/wix-forum/post/get-post-by-slug-by-slug) will look something like this:

```
{
  "post": {
      "id": "5cacd5fe04976c0015f35363",
      "categoryId": "5cacd5fe04976c0015f35362",
      "ownerId": "a27d2491-90b0-4a3a-87d9-7a9de00bf17a",
      "title": "Welcome to the Forum!",
      "contentText": "It’s good to have you here! Feel free to share anything - stories, ideas, pictures or whatever is on your mind.",
      "best_answer_comment_id": "5ce7bb354f055300a4b7f945",
      "pinned": false,
      "commentingEnabled": true,
      "commentCount": 3,
      "likeCount": 0,
      "viewCount": 11,
      "createdDate": "2019-04-09T17:27:26.171Z",
      "editedDate": "2019-04-09T17:27:26.171Z",
      "lastActivityDate": "2019-05-24T11:55:29.339Z",
      "slug": "welcome-to-the-forum",
      "postType": "QUESTION",
    }
}
```

### Query Posts
If a more detailed query is needed, use [Query Posts](https://dev.wix.com/api/rest/community/wix-forum/post/query-posts).
In the example below we're going to request only posts that have a title starting with "Welcome".
Note that we're also requesting to include the `"URL"` fields in the response:

```
curl 'https://www.wixapis.com/forum/v1/posts/query' --data-binary '{"fieldsToInclude": ["URL"], "filter":{"title":{"$startsWith": "Welcome"}}}' -H 'Content-Type: application/json' -H 'Authorization: <AUTH>'
```

The response we got looked like this:

```
{
  "posts": [
    {
      "id": "5cacd5fe04976c0015f35363",
      "categoryId": "5cacd5fe04976c0015f35362",
      "ownerId": "a27d2491-90b0-4a3a-87d9-7a9de00bf17a",
      "title": "Welcome to the Forum!",
      "contentText": "It’s good to have you here! Feel free to share anything - stories, ideas, pictures or whatever is on your mind.",
      "best_answer_comment_id": "5ce7bb354f055300a4b7f945",
      "pinned": false,
      "commentingEnabled": true,
      "commentCount": 3,
      "likeCount": 0,
      "viewCount": 11,
      "createdDate": "2019-04-09T17:27:26.171Z",
      "editedDate": "2019-04-09T17:27:26.171Z",
      "lastActivityDate": "2019-05-24T11:55:29.339Z",
      "slug": "welcome-to-the-forum",
      "postType": "QUESTION",
      "url": {
        "base": "https://wix.com",
        "path": "/forum/discussion-corner/welcome-to-the-forum"
      },
    }
  ],
  "metaData": {
    "count": 1,
    "offset": 0,
    "total": 1
  }
}
```

## Category API

### Get a Category by ID or by Slug

To get a specific category, use [Get Category](https://dev.wix.com/api/rest/community/wix-forum/category/get-category) to retrieve a category by its ID:

```
curl 'https://www.wixapis.com/forum/v1/categories/5cacd5fe04976c0015f35362' -H 'Content-Type: application/json' -H 'Authorization: <AUTH>'
```

Another option for retrieving a specific category is by using [Get Category by Slug](https://dev.wix.com/api/rest/community/wix-forum/category/get-category-by-slug-by-slug):

```
curl 'https://www.wixapis.com/forum/v1/categories/slugs/discussion-corner' -H 'Content-Type: application/json' -H 'Authorization: <AUTH>'
```

An example response to both

```
{
  "category": {
    "id": "5cacd5fe04976c0015f35362",
    "parentId": "001005fe04976c0015f35362",
    "name": "Discussion corner",
    "headerTitle": "Discussion corner",
    "description": "Share stories, ideas, pictures and more!",
    "headerType": "IMAGE",
    "headerImage": {
      "id": "image.png",
      "url": "image.png",
      "height": 760,
      "width": 2100
    },
    "rank": 0,
    "postCount": 2,
    "postViewCount": 17,
    "slug": "discussion-corner",
    "membersOnly": false
    "writeProtected": true
    "postTypes": ["DISCUSSION", "QUESTION"]
    "categoryType": "PUBLIC"
    "createdDate": "2019-04-09T17:27:26.171Z",
    "editedDate": "2019-04-09T17:27:26.171Z",
  }
}
```

#### Query Categories

If a more detailed query is needed, use [Query Categories](https://dev.wix.com/api/rest/community/wix-forum/category/query-categories).
In the example below we're going to request only categories that have a title starting with "Summer":

```
curl 'https://www.wixapis.com/forum/v1/categories/query' --data-binary '{"fieldsToInclude": ["URL"], "filter":{"name":{"$startsWith": "Summer"}}}' -H 'Content-Type: application/json' -H 'Authorization: <AUTH>'
```

The response will be an array of the categories that passed the query:

```
{
  "categories": [
    {
      "id": "5cacd5fe04976c0015f35362",
      "parentId": "001005fe04976c0015f35362",
      "name": "Discussion corner",
      "headerTitle": "Discussiosn corner",
      "description": "Share stories, ideas, pictures and more!",
      "headerType": "IMAGE",
      "headerImage": {
        "id": "image.png",
        "url": "image.png",
        "height": 760,
        "width": 2100
      },
      "rank": 0,
      "postCount": 2,
      "postViewCount": 17,
      "slug": "discussion-corner",
      "membersOnly": false
      "writeProtected": true
      "postTypes": ["DISCUSSION", "QUESTION"]
      "categoryType": "PUBLIC"
      "createdDate": "2019-04-09T17:27:26.171Z",
      "editedDate": "2019-04-09T17:27:26.171Z",
      "url": {
        "base": "https://wix.com",
        "path": "/forum/discussion-corner"
      }
    }
  ],
  "metaData": {
    "count": 1,
    "offset": 0,
    "total": 1
  }
}
```