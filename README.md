EventChat API Specification
===========================


* [User](#user)
  * [Get a single user](#get-a-single-user)
  * [Create a new user](#create-a-new-user)
* [Post](#post)
  * [Get a single post](#get-a-single-post)
  * [Create a new post](#create-a-new-post)
  * [Delete a post](#delete-a-post)
  * [Get posts owned by a single user](#get-posts-owned-by-a-single-user)
  * [Get posts for a single user's feed](#get-posts-for-a-single-users-feed)
* [Comment](#comment)
  * [Get comments for a single post](#get-comments-for-a-single-post)
  * [Create a new comment for a single post](#create-a-new-comment-for-a-single-post)
* [Event](#event)
  * [Get a single event](#get-a-single-event)
  * [Create a new event](#create-a-new-event)
  * [Delete an event](#delete-an-event)
  * [Update an event](#update-an-event)
* [Message](#message)
  * [Get all messages for a single event](#get-all-messages-for-a-single-event)
* [Notification](#notification)
  * [Get all notifications](#get-all-notifications)
  * [Mark a single notification as read](#mark-a-single-notification-as-read)
  * [Mark all notifications as read](#mark-all-notifications-as-read)



## User

### Get a single user

```
GET /users/:user_id
```

#### Response

```
Status: 200 OK
```

```json
{
    "id": 1,
    "name": "John Dow",
    "email": "johndow@example.com",
    "info": "I'm John Dow."
}
```

### Create a new user

```
POST /users
```

#### Body

Name  |  Type  | Description
------|--------|------------
name  | String | **Required** The name of the user
email | String | **Required** The email of the user
info  | String | The self-description of the user

#### Response

```
Status: 200 OK
```
