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
  * [Get posts for current user's feed](#get-posts-for-current-users-feed)
* [Comment](#comment)
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
    "info": "I'm John Dow.",
    "avatar_url": "http://gravatar.com/1.png"
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


## Post

### Get a single post

```
GET /posts/:post_id
```

#### Response

```
Status: 200 OK
```

```json
{
    "id": 1,
    "title": "what's the answer to life the universe and everything?",
    "type": "text",
    "body": "It's 42",
    "created_at": "Fri May 23 2014 12:54:31 GMT-0700 (PDT)",
    "author": {
        "id": 1,
        "avatar_url": "http://gravatar.com/1.png",
        "name": "John Dow"
    },
    "comments": [
        {
            "id": 3,
            "author": {
                "id": 2,
                "avatar_url": "http://gravatar.com/2.png",
                "name": "John Snow"
            },
            "body": "This is awesome!!!",
            "created_at": "Fri May 23 2014 12:54:31 GMT-0700 (PDT)"
        }
    ]
}
```

### Create a new post

```
POST /posts
```

#### Body

Name  |  Type  | Description
------|--------|------------
title | String | **Required** The title of the post
type  | String | **Required** The type of the post, can be "text", "picture" or "video"
body  | String | **Required** The content of the post

#### Response

```
Status: 200 OK
```


### Delete a post

```
DELETE /posts/:post_id
```

#### Response

```
Status: 200 OK
```



### Get posts owned by a single user

```
GET /users/:user_id/posts
```

#### Response

```
Status: 200 OK
```

```json
[
    {
        "id": 1,
        "title": "what's the answer to life the universe and everything?",
        "type": "text",
        "body": "It's 42",
        "created_at": "Fri May 23 2014 12:54:31 GMT-0700 (PDT)",
        "author": {
            "id": 1,
            "avatar_url": "http://gravatar.com/1.png",
            "name": "John Dow"
        },
        "comments": [
            {
                "id": 3,
                "author": {
                    "id": 2,
                    "avatar_url": "http://gravatar.com/2.png",
                    "name": "John Snow"
                },
                "body": "This is awesome!!!",
                "created_at": "Fri May 23 2014 12:54:31 GMT-0700 (PDT)"
            }
        ]
    }
]
```

### Get posts for current user's feed

```
GET /posts/feed
```

#### Response

```
Status: 200 OK
```

```json
[
    {
        "id": 1,
        "title": "what's the answer to life the universe and everything?",
        "type": "text",
        "body": "It's 42",
        "created_at": "Fri May 23 2014 12:54:31 GMT-0700 (PDT)",
        "author": {
            "id": 1,
            "avatar_url": "http://gravatar.com/1.png",
            "name": "John Dow"
        },
        "comments": [
            {
                "id": 3,
                "author": {
                    "id": 2,
                    "avatar_url": "http://gravatar.com/2.png",
                    "name": "John Snow"
                },
                "body": "This is awesome!!!",
                "created_at": "Fri May 23 2014 12:54:31 GMT-0700 (PDT)"
            }
        ]
    }
]
```


## Comment

### Create a new comment for a single post

```
POST /posts/:post_id/comments
```

#### Body

Name  |  Type  | Description
------|--------|------------
body  | String | **Required** The content of the comment


#### Response

```
Status: 200 OK
```


## Event

### Get a single event

```
GET /events/:event_id
```

#### Response

```json
{
    "id": 1,
    "name": "Pycon",
    "longitude": 23.562312,
    "latitude": -53.90145,
    "start_time": "Fri May 23 2014 14:10:05 GMT-0700 (PDT)",
    "end_time": "Fri May 23 2014 15:10:05 GMT-0700 (PDT)",
    "description": "Python Conference"
}
```

### Create a new event

```
POST /events
```

#### Body

Name        |  Type  | Description
------------|--------|------------
name        | String | **Required** The name of the event
longitude   | Number | **Required** The longitude of the event location
latitude    | Number | **Required** The latitude of the event location
start_time  | String | The start time of the event
end_time    | String | The end time of the event
description | String | The description of the event


#### Response

```
Status: 200 OK
```


### Update an event

```
PATCH /events
```

#### Body

Name        |  Type  | Description
------------|--------|------------
name        | String | **Required** The name of the event
longitude   | Number | **Required** The longitude of the event location
latitude    | Number | **Required** The latitude of the event location
start_time  | String | The start time of the event
end_time    | String | The end time of the event
description | String | The description of the event

#### Response

```
Status: 200 OK
```

### Delete an event

```
DELETE /events/:event_id
```

#### Response

```
Status: 200 OK
```

## Message

### Get all messages for a single event

```
GET /events/:event_id/messages
```

#### Response

```
Status: 200 OK
```

```json
[
    {
        "id": 1,
        "author": {
            "id": 1,
            "avatar_url": "http://gravatar.com/1.png",
            "name": "John Dow"
        },
        "body": "Hello everyone :)",
        "created_at": "Fri May 23 2014 15:10:05 GMT-0700 (PDT)"
    }
]
```

## Notification

### Get all notifications

```
GET /notifications
```

#### Response

```
Status: 200 OK
```

```json
[
    {
        "id": 1,
        "type": "comment",
        "body": "@john commented on your post",
        "is_read": false,
        "created_at": "Fri May 23 2014 15:10:05 GMT-0700 (PDT)"
    }
]
```


### Mark a single notification as read

```
PATCH /notifications/:notification_id
```


#### Response

```
Status: 200 OK
```


### Mark all notifications as read

```
PATCH /notifications
```


#### Response

```
Status: 200 OK
```
