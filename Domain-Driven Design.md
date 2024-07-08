# Domain Driven Design Analysis for FriendPost

## 1. Domain Overview
FriendPost is a social media platform that enables users to interact through posts and friendships. It allows users to manage their profiles, create and manage posts, send and receive friend requests, view a personalized timeline, and receive friend suggestions. This analysis will break down the domain into various components using Domain Driven Design principles.

## 2. Core Domains
- **User Management**: Handles registration, authentication, profile management, and account deactivation.
- **Post Management**: Manages creation, modification, and visibility of posts.
- **Friendship Management**: Handles sending, receiving, accepting, and rejecting friend requests, as well as managing friends and friend suggestions.
- **Timeline Management**: Manages the generation of the timeline for users based on posts and friendships.

## 3. Subdomains and Entities

### 3.1 User Management
**Entities:**
- **User**
  - Attributes: 
    - userId
    - email
    - password
    - profile (basic information)
    - status (active/deactivated)
  - Actions: 
    - Register
    - Login
    - Logout
    - Update Profile
    - Deactivate Account

### 3.2 Post Management
**Entities:**
- **Post**
  - Attributes: 
    - postId
    - author (User)
    - content (text)
    - createdDateTime
    - modifiedDateTime
    - audience (Public/Private)
  - Actions: 
    - Create Post
    - Edit Post
    - Delete Post

### 3.3 Friendship Management
**Entities:**
- **FriendRequest**
  - Attributes:
    - requestId
    - requester (User)
    - target (User)
    - status (Pending/Accepted/Rejected)
  - Actions: 
    - Send Request
    - Accept Request
    - Reject Request
    - View Pending Requests

- **Friendship**
  - Attributes:
    - userId1
    - userId2
  - Actions: 
    - Add Friend
    - Remove Friend

### 3.4 Timeline Management
**Entities:**
- **Timeline**
  - Attributes: 
    - userId
    - posts (list of Post objects)
  - Actions: 
    - Generate Timeline
    - Prioritize Posts (friend posts over public posts)

## 4. Aggregates
- **UserAggregate**: Comprises User, Post, FriendRequest, and Friendship entities. Manages lifecycle of a User and related actions.
- **PostAggregate**: Manages the lifecycle of a Post, including creation, modification, and deletion.
- **FriendshipAggregate**: Manages the process of sending, accepting, rejecting friend requests, and maintaining friendships.

## 5. Repositories
- **UserRepository**: Handles the persistence and retrieval of User entities.
- **PostRepository**: Manages the storage and retrieval of Post entities.
- **FriendshipRepository**: Manages FriendRequest and Friendship entities.

## 6. Services
- **UserService**: Business logic for user registration, authentication, profile management, and deactivation.
- **PostService**: Handles business logic for creating, editing, and deleting posts.
- **FriendshipService**: Manages the logic for friend requests and friendships.
- **TimelineService**: Generates and prioritizes posts for user timelines, including logic for friend suggestions.

## 7. Value Objects
- **Profile**: Contains immutable profile information of a user such as name, age, location, etc.
- **Credentials**: Encapsulates the email and password for authentication.

## 8. Domain Events
- **UserRegistered**: Triggered when a new user registers.
- **PostCreated**: Triggered when a new post is created.
- **FriendRequestSent**: Triggered when a friend request is sent.
- **FriendRequestAccepted**: Triggered when a friend request is accepted.

## 9. Bounded Contexts
- **UserContext**: Manages everything related to users, including registration, authentication, profile management, and deactivation.
- **PostContext**: Manages post creation, modification, and visibility.
- **FriendshipContext**: Handles sending, receiving, and managing friend requests and friendships.
- **TimelineContext**: Manages the generation and prioritization of user timelines and friend suggestions.

## 10. Application Flow

### 10.1 Registration
1. User submits registration form.
2. **UserService** validates and creates a new User.
3. **UserRepository** saves the User entity.
4. **UserRegistered** event is triggered.

### 10.2 Creating a Post
1. User submits a new post.
2. **PostService** validates and creates a new Post.
3. **PostRepository** saves the Post entity.
4. **PostCreated** event is triggered.

### 10.3 Sending a Friend Request
1. User sends a friend request.
2. **FriendshipService** validates and creates a new FriendRequest.
3. **FriendshipRepository** saves the FriendRequest entity.
4. **FriendRequestSent** event is triggered.

### 10.4 Generating Timeline
1. User logs in and requests their timeline.
2. **TimelineService** retrieves user's friends and relevant posts.
3. **TimelineService** prioritizes and orders posts.
4. Timeline is displayed to the user.

## 11. Conclusion
The FriendPost application is divided into distinct bounded contexts with clear responsibilities. Each context manages its entities and aggregates, ensuring separation of concerns and maintainability. This domain-driven design approach helps in organizing the complex business logic and interactions within the application.

This structured analysis provides a foundation for further development and implementation of FriendPost, ensuring scalability and flexibility for future enhancements.
