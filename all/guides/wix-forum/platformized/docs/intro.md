SortOrder: 0
# About Forum

Wix Forum allows users to create and manage forum posts. The posts can be organized in categories.

Learn more [about Wix Forum](https://support.wix.com/en/article/wix-forum-about-wix-forum).

## Terminology

- **Post**
  A post written by the site member.
- **Category**
  A logical group that the site member assigns their post(s) to in forum.

## Use cases

The Forum API allows developers to reuse forum content in a modular fashion and give site members access to a forum's functionality without having to acccess the full site.

Examples could be:
 - display available discussion forum categories from multiple sites, in an aggregator app for participating community sites, using the [Query Categories endpoint](https://bo.wix.com/wix-docs/rest/community/wix-forum/category/query-categories).
 - set up an automated feed of new posts and sub-forums based on news, events, or other topics (not even necessarily from the site itself) so that members and admins don't have to do it manually:
    1. Decide criteria for selecting forum posts to display, e.g. based on keywords or listing all categories, and retrieve these categories using the [Query Categories endpoint](https://bo.wix.com/wix-docs/rest/community/wix-forum/category/query-categories).
   2. Consume the [Post Created Domain Event](https://bo.wix.com/wix-docs/rest/community/wix-forum/post/post-created-domain-event) to get all new posts
   3. Filter the new posts by their `categoryId`, or by keywords found in `contentText`, and link back to them using `url` and `title` to create links.
   
