EventChat API Specification
===========================


* [Overview](#overview)
  * [API Server](#api-server)
  * [ID](#id)
  * [DateTime](#datetime)
* [Authentication](#authentication)
  * [Login](#login)
  * [Logout](#logout)
  * [Check login status](#check-login-status)
* [User](#user)
  * [Get a single user](#get-a-single-user)
  * [Create a new user](#create-a-new-user)
* [Post](#post)
  * [Get a single post](#get-a-single-post)
  * [Create a new post](#create-a-new-post)
  * [Delete a post](#delete-a-post)
  * [Get posts owned by a single user](#get-posts-owned-by-a-single-user)
  * [Search posts](#search-posts)
  * [Like a post](#like-a-post)
  * [Unlike a post](#unlike-a-post)
* [Comment](#comment)
  * [Create a new comment for a single post](#create-a-new-comment-for-a-single-post)
* [Event](#event)
  * [Get a single event](#get-a-single-event)
  * [Create a new event](#create-a-new-event)
  * [Delete an event](#delete-an-event)
  * [Update an event](#update-an-event)
  * [Search events](#search-events)
  * [Join an event](#join-an-event)
  * [Get attendees for a single event](#get-attendees-for-a-single-event)
  * [Get all events that a user attends](#get-all-events-that-a-user-attends)
* [Message](#message)
  * [Get all messages for a single event](#get-all-messages-for-a-single-event)
* [Friend](#friend)
  * [Get all friends of a single user](#get-all-friends-of-a-single-user)
  * [Send a friend request to a user](#send-a-friend-request-to-a-user)
* [Notification](#notification)
  * [Get all notifications](#get-all-notifications)
  * [Mark a single notification as read](#mark-a-single-notification-as-read)
  * [Mark all notifications as read](#mark-all-notifications-as-read)
* [Chat](#chat)
  * [Get all unread messages sent to the current user](#get-all-unread-messages-sent-to-the-current-user)
  * [Send a message to a specific user](#send-a-message-to-a-specific-user)


## Overview


### API Server

The API Server is deployed on Heroku and is available at

http://eventchat.herokuapp.com

All API paths described below are relative to this url.

### ID

Since MongoDB is being used as the backend storage, the IDs are in the MongoDB
ObjectID format, which look like "5384c6cc96eb36aa242cfdc6",
instead of the traditional auto-incrementing number ID such as 1, 2, 3.


### DateTime

All datetimes are represented in ISO8601 standard, which looks like "2012-01-01T12:00:00Z".


## Authentication


### Login

```
POST /session
```

#### Body

Name     |  Type  | Description
---------|--------|------------
name     | String | **Required** The name of the user
password | String | **Required** The password of the user

#### Response

```
Status: 200 OK
```

```json
{
    "id": "5384c6cc96eb36aa242cfdc6",
    "name": "John Doe",
    "email": "johndoe@example.com",
    "info": "I'm John Doe.",
    "avatar_url": "http://gravatar.com/1.png",
    "created_at": "2014-05-27T17:16:28.709Z"
}
```

### Logout

```
DELETE /session
```

#### Response

```
Status: 200 OK
```

### Check login status

```
GET /session
```

#### Response

```
Status: 200 OK
```


```json
{
    "logged_in": true
}
```

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
    "id": "5384c6cc96eb36aa242cfdc6",
    "name": "John Doe",
    "email": "johndoe@example.com",
    "info": "I'm John Doe.",
    "avatar_url": "http://gravatar.com/1.png",
    "created_at": "2014-05-27T17:16:28.709Z"
}
```

### Create a new user

```
POST /users
```

#### Body

Name     |  Type  | Description
---------|--------|------------
name     | String | **Required** The name of the user
email    | String | **Required** The email of the user
password | String | **Required** The password of the user
info     | String | The self-description of the user

#### Response

```
Status: 200 OK
```

```json
{
    "id": "5384c6cc96eb36aa242cfdc6",
    "name": "John Doe",
    "email": "johndoe@example.com",
    "info": "I'm John Doe.",
    "avatar_url": "http://gravatar.com/1.png",
    "created_at": "2014-05-27T17:16:28.709Z"
}
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
    "id": "5384c6cc96eb36aa242cfdc6",
    "title": "what's the answer to life the universe and everything?",
    "type": "text",
    "body": "It's 42",
    "created_at": "2014-05-27T17:16:28.709Z",
    "author": {
        "id": "5384c6cc96eb36aa242cfdc6",
        "name": "John Doe",
        "email": "johndoe@example.com",
        "info": "I'm John Doe.",
        "avatar_url": "http://gravatar.com/1.png",
        "created_at": "2014-05-27T17:16:28.709Z"
    },
    "event": {
        "organizer": {
            "id": "5384c6cc96eb36aa242cfdc6",
            "name": "John Doe",
            "email": "johndoe@example.com",
            "info": "I'm John Doe.",
            "avatar_url": "http://gravatar.com/1.png",
            "created_at": "2014-05-27T17:16:28.709Z"
        },
        "id": "5384c6cc96eb36aa242cfdc6",
        "name": "PyCon",
        "description": "Python Conference",
        "latitude": 23.4567,
        "longitude": -122.4535,
        "address": "777 W MiddleField Rd. Mountain View, CA, 94043",
        "start_time": "2014-05-27T17:16:28.709Z",
        "end_time": "2014-05-27T17:16:28.709Z"
    },
    "comments": [
        {
            "id": "5384c6cc96eb36aa242cfdc6",
            "author": {
                "id": "5384c6cc96eb36aa242cfdc6",
                "name": "John Doe",
                "email": "johndoe@example.com",
                "info": "I'm John Doe.",
                "avatar_url": "http://gravatar.com/1.png",
                "created_at": "2014-05-27T17:16:28.709Z"
            },
            "body": "This is awesome!!!",
            "created_at": "2014-05-27T17:16:28.709Z"
        }
    ],
    "liked_by": [
        {
            "id": "5384c6cc96eb36aa242cfdc6",
            "name": "John Doe",
            "email": "johndoe@example.com",
            "info": "I'm John Doe.",
            "avatar_url": "http://gravatar.com/1.png",
            "created_at": "2014-05-27T17:16:28.709Z"
        }
    ]
}
```

### Create a new post

```
POST /posts
```

#### Body

Name     |  Type  | Description
---------|--------|------------
title    | String | **Required** The title of the post
type     | String | **Required** The type of the post, can be "text", "picture" or "video"
body     | String | **Required** The content of the post
event_id | String | **Required** The id of the associated event

#### Response

```
Status: 200 OK
```

```json
{
    "id": "5384c6cc96eb36aa242cfdc6",
    "title": "what's the answer to life the universe and everything?",
    "type": "text",
    "body": "It's 42",
    "created_at": "2014-05-27T17:16:28.709Z",
    "author": {
        "id": "5384c6cc96eb36aa242cfdc6",
        "name": "John Doe",
        "email": "johndoe@example.com",
        "info": "I'm John Doe.",
        "avatar_url": "http://gravatar.com/1.png",
        "created_at": "2014-05-27T17:16:28.709Z"
    },
    "event": {
        "organizer": {
            "id": "5384c6cc96eb36aa242cfdc6",
            "name": "John Doe",
            "email": "johndoe@example.com",
            "info": "I'm John Doe.",
            "avatar_url": "http://gravatar.com/1.png",
            "created_at": "2014-05-27T17:16:28.709Z"
        },
        "id": "5384c6cc96eb36aa242cfdc6",
        "name": "PyCon",
        "description": "Python Conference",
        "latitude": 23.4567,
        "longitude": -122.4535,
        "address": "777 W MiddleField Rd. Mountain View, CA, 94043",
        "start_time": "2014-05-27T17:16:28.709Z",
        "end_time": "2014-05-27T17:16:28.709Z"
    },
    "comments": [
        {
            "id": "5384c6cc96eb36aa242cfdc6",
            "author": {
                "id": "5384c6cc96eb36aa242cfdc6",
                "name": "John Doe",
                "email": "johndoe@example.com",
                "info": "I'm John Doe.",
                "avatar_url": "http://gravatar.com/1.png",
                "created_at": "2014-05-27T17:16:28.709Z"
            },
            "body": "This is awesome!!!",
            "created_at": "2014-05-27T17:16:28.709Z"
        }
    ],
    "liked_by": [
        {
            "id": "5384c6cc96eb36aa242cfdc6",
            "name": "John Doe",
            "email": "johndoe@example.com",
            "info": "I'm John Doe.",
            "avatar_url": "http://gravatar.com/1.png",
            "created_at": "2014-05-27T17:16:28.709Z"
        }
    ]
}
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
        "id": "5384c6cc96eb36aa242cfdc6",
        "title": "what's the answer to life the universe and everything?",
        "type": "text",
        "body": "It's 42",
        "created_at": "2014-05-27T17:16:28.709Z",
        "author": {
            "id": "5384c6cc96eb36aa242cfdc6",
            "name": "John Doe",
            "email": "johndoe@example.com",
            "info": "I'm John Doe.",
            "avatar_url": "http://gravatar.com/1.png",
            "created_at": "2014-05-27T17:16:28.709Z"
        },
        "event": {
            "organizer": {
                "id": "5384c6cc96eb36aa242cfdc6",
                "name": "John Doe",
                "email": "johndoe@example.com",
                "info": "I'm John Doe.",
                "avatar_url": "http://gravatar.com/1.png",
                "created_at": "2014-05-27T17:16:28.709Z"
            },
            "id": "5384c6cc96eb36aa242cfdc6",
            "name": "PyCon",
            "description": "Python Conference",
            "latitude": 23.4567,
            "longitude": -122.4535,
            "address": "777 W MiddleField Rd. Mountain View, CA, 94043",
            "start_time": "2014-05-27T17:16:28.709Z",
            "end_time": "2014-05-27T17:16:28.709Z"
        },
        "comments": [
            {
                "id": "5384c6cc96eb36aa242cfdc6",
                "author": {
                    "id": "5384c6cc96eb36aa242cfdc6",
                    "name": "John Doe",
                    "email": "johndoe@example.com",
                    "info": "I'm John Doe.",
                    "avatar_url": "http://gravatar.com/1.png",
                    "created_at": "2014-05-27T17:16:28.709Z"
                },
                "body": "This is awesome!!!",
                "created_at": "2014-05-27T17:16:28.709Z"
            }
        ],
        "liked_by": [
            {
                "id": "5384c6cc96eb36aa242cfdc6",
                "name": "John Doe",
                "email": "johndoe@example.com",
                "info": "I'm John Doe.",
                "avatar_url": "http://gravatar.com/1.png",
                "created_at": "2014-05-27T17:16:28.709Z"
            }
        ]
    }
]
```

### Search Posts

```
GET /posts/search
```

#### Parameters

Name         |  Type  | Description
-------------|--------|----------------------
latitude     | Number | Latitude of the post
longitude    | Number | Longitude of the post
max_distance | Number | Max distance from the specified coordinate, in meters. (Default 500)

#### Example


```
GET /posts/search?latitude=23.4567&longitude=-122.4535&max_distance=1000
```

will return posts within 1000 meters from the coordinate 23.4567° N, 122.4535° W.

#### Response

```
Status: 200 OK
```

```json
[
    {
        "id": "5384c6cc96eb36aa242cfdc6",
        "title": "what's the answer to life the universe and everything?",
        "type": "text",
        "body": "It's 42",
        "created_at": "2014-05-27T17:16:28.709Z",
        "author": {
            "id": "5384c6cc96eb36aa242cfdc6",
            "name": "John Doe",
            "email": "johndoe@example.com",
            "info": "I'm John Doe.",
            "avatar_url": "http://gravatar.com/1.png",
            "created_at": "2014-05-27T17:16:28.709Z"
        },
        "event": {
            "organizer": {
                "id": "5384c6cc96eb36aa242cfdc6",
                "name": "John Doe",
                "email": "johndoe@example.com",
                "info": "I'm John Doe.",
                "avatar_url": "http://gravatar.com/1.png",
                "created_at": "2014-05-27T17:16:28.709Z"
            },
            "id": "5384c6cc96eb36aa242cfdc6",
            "name": "PyCon",
            "description": "Python Conference",
            "latitude": 23.4567,
            "longitude": -122.4535,
            "address": "777 W MiddleField Rd. Mountain View, CA, 94043",
            "start_time": "2014-05-27T17:16:28.709Z",
            "end_time": "2014-05-27T17:16:28.709Z"
        },
        "comments": [
            {
                "id": "5384c6cc96eb36aa242cfdc6",
                "author": {
                    "id": "5384c6cc96eb36aa242cfdc6",
                    "name": "John Doe",
                    "email": "johndoe@example.com",
                    "info": "I'm John Doe.",
                    "avatar_url": "http://gravatar.com/1.png",
                    "created_at": "2014-05-27T17:16:28.709Z"
                },
                "body": "This is awesome!!!",
                "created_at": "2014-05-27T17:16:28.709Z"
            }
        ],
        "liked_by": [
            {
                "id": "5384c6cc96eb36aa242cfdc6",
                "name": "John Doe",
                "email": "johndoe@example.com",
                "info": "I'm John Doe.",
                "avatar_url": "http://gravatar.com/1.png",
                "created_at": "2014-05-27T17:16:28.709Z"
            }
        ]
    }
]
```

### Like a post

```
POST /posts/:post_id/liked_by
```

#### Response

```
Status: 200 OK
```


### Unlike a post

```
DELETE /posts/:post_id/liked_by
```

#### Response

```
Status: 200 OK
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

```json
{
    "id": "5384c6cc96eb36aa242cfdc6",
    "title": "what's the answer to life the universe and everything?",
    "type": "text",
    "body": "It's 42",
    "created_at": "2014-05-27T17:16:28.709Z",
    "author": {
        "id": "5384c6cc96eb36aa242cfdc6",
        "name": "John Doe",
        "email": "johndoe@example.com",
        "info": "I'm John Doe.",
        "avatar_url": "http://gravatar.com/1.png",
        "created_at": "2014-05-27T17:16:28.709Z"
    },
    "event": {
        "organizer": {
            "id": "5384c6cc96eb36aa242cfdc6",
            "name": "John Doe",
            "email": "johndoe@example.com",
            "info": "I'm John Doe.",
            "avatar_url": "http://gravatar.com/1.png",
            "created_at": "2014-05-27T17:16:28.709Z"
        },
        "id": "5384c6cc96eb36aa242cfdc6",
        "name": "PyCon",
        "description": "Python Conference",
        "latitude": 23.4567,
        "longitude": -122.4535,
        "address": "777 W MiddleField Rd. Mountain View, CA, 94043",
        "start_time": "2014-05-27T17:16:28.709Z",
        "end_time": "2014-05-27T17:16:28.709Z"
    },
    "comments": [
        {
            "id": "5384c6cc96eb36aa242cfdc6",
            "author": {
                "id": "5384c6cc96eb36aa242cfdc6",
                "name": "John Doe",
                "email": "johndoe@example.com",
                "info": "I'm John Doe.",
                "avatar_url": "http://gravatar.com/1.png",
                "created_at": "2014-05-27T17:16:28.709Z"
            },
            "body": "This is awesome!!!",
            "created_at": "2014-05-27T17:16:28.709Z"
        }
    ],
    "liked_by": [
        {
            "id": "5384c6cc96eb36aa242cfdc6",
            "name": "John Doe",
            "email": "johndoe@example.com",
            "info": "I'm John Doe.",
            "avatar_url": "http://gravatar.com/1.png",
            "created_at": "2014-05-27T17:16:28.709Z"
        }
    ]
}
```



## Event

### Get a single event

```
GET /events/:event_id
```

#### Response

```json
{
    "organizer": {
        "id": "5384c6cc96eb36aa242cfdc6",
        "name": "John Doe",
        "email": "johndoe@example.com",
        "info": "I'm John Doe.",
        "avatar_url": "http://gravatar.com/1.png",
        "created_at": "2014-05-27T17:16:28.709Z"
    },
    "id": "5384c6cc96eb36aa242cfdc6",
    "name": "Pycon",
    "longitude": 23.562312,
    "latitude": -53.90145,
    "address": "777 W MiddleField Rd. Mountain View, CA, 94043",
    "start_time": "2014-05-27T17:16:28.709Z",
    "end_time": "2014-05-27T17:16:28.709Z",
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
address     | String | The postal address of the event
start_time  | String | The start time of the event
end_time    | String | The end time of the event
description | String | The description of the event


#### Response

```
Status: 200 OK
```

```json
{
    "organizer": {
        "id": "5384c6cc96eb36aa242cfdc6",
        "name": "John Doe",
        "email": "johndoe@example.com",
        "info": "I'm John Doe.",
        "avatar_url": "http://gravatar.com/1.png",
        "created_at": "2014-05-27T17:16:28.709Z"
    },
    "id": "5384c6cc96eb36aa242cfdc6",
    "name": "Pycon",
    "longitude": 23.562312,
    "latitude": -53.90145,
    "address": "777 W MiddleField Rd. Mountain View, CA, 94043",
    "start_time": "2014-05-27T17:16:28.709Z",
    "end_time": "2014-05-27T17:16:28.709Z",
    "description": "Python Conference"
}
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
address     | String | The postal address of the event
start_time  | String | The start time of the event
end_time    | String | The end time of the event
description | String | The description of the event

#### Response

```
Status: 200 OK
```

```json
{
    "organizer": {
        "id": "5384c6cc96eb36aa242cfdc6",
        "name": "John Doe",
        "email": "johndoe@example.com",
        "info": "I'm John Doe.",
        "avatar_url": "http://gravatar.com/1.png",
        "created_at": "2014-05-27T17:16:28.709Z"
    },
    "id": "5384c6cc96eb36aa242cfdc6",
    "name": "Pycon",
    "longitude": 23.562312,
    "latitude": -53.90145,
    "address": "777 W MiddleField Rd. Mountain View, CA, 94043",
    "start_time": "2014-05-27T17:16:28.709Z",
    "end_time": "2014-05-27T17:16:28.709Z",
    "description": "Python Conference"
}
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
        "id": "5384c6cc96eb36aa242cfdc6",
        "author": {
            "id": "5384c6cc96eb36aa242cfdc6",
            "name": "John Doe",
            "email": "johndoe@example.com",
            "info": "I'm John Doe.",
            "avatar_url": "http://gravatar.com/1.png",
            "created_at": "2014-05-27T17:16:28.709Z"
        },
        "body": "Hello everyone :)",
        "created_at": "2014-05-27T17:16:28.709Z"
    }
]
```


### Get all events that a user attends

```
GET /users/:user_id/events
```

#### Response

```
Status: 200 OK
```

```json
[
    {
        "organizer": {
            "id": "5384c6cc96eb36aa242cfdc6",
            "name": "John Doe",
            "email": "johndoe@example.com",
            "info": "I'm John Doe.",
            "avatar_url": "http://gravatar.com/1.png",
            "created_at": "2014-05-27T17:16:28.709Z"
        },
        "id": "5384c6cc96eb36aa242cfdc6",
        "name": "Pycon",
        "longitude": 23.562312,
        "latitude": -53.90145,
        "address": "777 W MiddleField Rd. Mountain View, CA, 94043",
        "start_time": "2014-05-27T17:16:28.709Z",
        "end_time": "2014-05-27T17:16:28.709Z",
        "description": "Python Conference"
    }
]
```



### Search Events

```
GET /events/search
```

#### Parameters

Name         |  Type  | Description
-------------|--------|----------------------
latitude     | Number | Latitude of the post
longitude    | Number | Longitude of the post
max_distance | Number | Max distance from the specified coordinate, in meters. (Default 500)

#### Example


```
GET /events/search?latitude=23.4567&longitude=-122.4535&max_distance=1000
```

will return events within 1000 meters from the coordinate 23.4567° N, 122.4535° W.

#### Response

```
Status: 200 OK
```

```json
[
    {
        "organizer": {
            "id": "5384c6cc96eb36aa242cfdc6",
            "name": "John Doe",
            "email": "johndoe@example.com",
            "info": "I'm John Doe.",
            "avatar_url": "http://gravatar.com/1.png",
            "created_at": "2014-05-27T17:16:28.709Z"
        },
        "id": "5384c6cc96eb36aa242cfdc6",
        "name": "Pycon",
        "longitude": 23.562312,
        "latitude": -53.90145,
        "address": "777 W MiddleField Rd. Mountain View, CA, 94043",
        "start_time": "2014-05-27T17:16:28.709Z",
        "end_time": "2014-05-27T17:16:28.709Z",
        "description": "Python Conference"
    }
]
```

### Join an event

```
POST /events/:event_id/attendees
```

#### Response

```
Status: 200 OK
```


### Get attendees for a single event

```
GET /events/:event_id/attendees
```

#### Response

```
Status: 200 OK
```

```json
[
    {
        "id": "5384c6cc96eb36aa242cfdc6",
        "name": "John Doe",
        "email": "johndoe@example.com",
        "info": "I'm John Doe.",
        "avatar_url": "http://gravatar.com/1.png",
        "created_at": "2014-05-27T17:16:28.709Z"
    }
]
```

## Friend

### Get all friends of a single user

```
GET /users/:user_id/friends
```

#### Response

```json
[
    {
        "id": "5384c6cc96eb36aa242cfdc6",
        "name": "John Doe",
        "email": "johndoe@example.com",
        "info": "I'm John Doe.",
        "avatar_url": "http://gravatar.com/1.png",
        "created_at": "2014-05-27T17:16:28.709Z"
    },
    {
        "id": "5384c6cc96eb36aa242cfdc7",
        "name": "Lyman",
        "email": "lyman@example.com",
        "info": "I'm Lyman.",
        "avatar_url": "http://gravatar.com/2.png",
        "created_at": "2014-05-27T17:16:28.709Z"
    }
]
```

### Send a friend request to a user

A friend request will be sent to the target user as an notification.
The target user has to resend another friend request back to the initiator
so as the acknowledge the friendship.

```
POST /users/:user_id/friends
```

#### Response

```
Status: 200 OK
```

#### Example

User A wants to add user B as friend, then A should first 

```
POST /users/B/friends
```
(substitute B with B's id)

Then B will receive a notification (See [Friend request notification](#friend-request-notification) for the format
of a friend request notification) regarding A's request. In order to acknowledge the 
friendship, B should send another friend request back to A.

```
POST /users/A/friends
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
        "id": "5384c6cc96eb36aa242cfdc6",
        "type": "comment",
        "body": "@john commented on your post",
        "is_read": false,
        "created_at": "2014-05-27T17:16:28.709Z"
    }
]
```

##### Friend request notification

More specifically, if the notification is a friend request,
then the response will be like the following:

```json
[
    {
        "id": "5384c6cc96eb36aa242cfdc6",
        "type": "friend",
        "body": "{\"id\": \"5384c6cc96eb36aa242cfdc6\", \"name\": \"John Doe\", \"email\": \"johndoe@example.com\", \"info\": \"I'm John Doe.\", \"avatar_url\": \"http://gravatar.com/1.png\", \"created_at\": \"2014-05-27T17:16:28.709Z\" }",
        "is_read": false,
        "created_at": "2014-05-27T17:16:28.709Z"
    }
]
```

The body field is a serialized json containing the info of the user
who initiated the friend request.



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


## Chat

### Get all unread messages sent to the current user

NOTE: login required

```
GET /chat
```

#### Response

```
Status: 200 OK
```

```json
[
    {
        "from": {
            "id": "5384c6cc96eb36aa242cfdc6",
            "name": "John Doe",
            "email": "johndoe@example.com",
            "info": "I'm John Doe.",
            "avatar_url": "http://gravatar.com/1.png",
            "created_at": "2014-05-27T17:16:28.709Z"
        },
        "message": "how are you?",
        "created_at": "2014-05-27T17:16:28.709Z"
    },
    {
        "from": {
            "id": "5384c6cc96eb36aa242cfdc6",
            "name": "John Doe",
            "email": "johndoe@example.com",
            "info": "I'm John Doe.",
            "avatar_url": "http://gravatar.com/1.png",
            "created_at": "2014-05-27T17:16:28.709Z"
        },
        "message": "how do you do",
        "created_at": "2014-05-27T17:16:28.709Z"
    }
]
```


### Send a message to a specific user

NOTE: login required

```
POST /chat
```

#### Body

Name        |  Type  | Description
------------|--------|------------
to          | String | **Required** The id of the receiver
message     | String | **Required** The message to send

#### Response

```
Status: 200 OK
```
