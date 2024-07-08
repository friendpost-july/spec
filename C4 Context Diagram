# FriendPost C4 Context Diagram

```mermaid
C4Context
title System Context diagram for FriendPost Application
    
Boundary(f1, "Friendbook") {
    System(frontend, "Web Application")
    System(postsservice,"Posts Service")
    System(profileservice, "Profile Service")
    
    System(timelineservice, "Timeline Service")

    System(friendsservice, "Friends Service")  
}

Person(user1, "User","signs up/in, gets timeline, manages friends, manages posts")
Rel(user1, frontend, "interacts with")
Rel(frontend, postsservice, "make posts")
Rel(user1, frontend, "interacts with")
Rel(frontend, profileservice, "sign up, update profile")
Rel(frontend, timelineservice, "get timeline")
Rel(frontend, friendsservice, "get friends, manage requests")
Rel(frontend, postsservice, "make posts")
Rel(timelineservice, postsservice, "get posts")
Rel(timelineservice, friendsservice, "get friendships")
Rel(timelineservice, profileservice, "check user status")
Rel(friendsservice, profileservice,"get suggestion data")

UpdateLayoutConfig("2","1")
```