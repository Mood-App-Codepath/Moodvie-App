Original App Design Project - README Template
===

# Moodvie

## Table of Contents
1. [Overview](#Overview)
1. [Product Spec](#Product-Spec)
1. [Wireframes](#Wireframes)
2. [Schema](#Schema)

## Overview
### Description
Moodvie is an iOS application where users can find a movie depending on the user's mood. Users could find other users who have watched the movie.

### App Evaluation

- **Category:** Social Networking/ Movie
- **Mobile:** This application will solely be built for iOS, but will be available in other devices as well soon.
- **Story:** Analyzes user's preferences for the movie, and finds the movie's reviews left by other users, and streaming platform that it is posted on, and join communities within the application.
- **Market:** Any users trying to find movies, and make friends who have seen that movie
- **Habit:** Users can use this app whenever they are trying to look for a movie, and connect with people who had seen that movie. Any time a user has downtime to watch movie.
- **Scope:** We would try to find what kind of movies to recommend to the user, then allow user to pick a movie and connect with users that have watched the movie previously.

## Product Spec

### 1. User Stories (Required and Optional)

**Required Must-have Stories**

* Users will need to log in or register to find a random movie and connect with other users
* Users can find the description of the movie, streaming services it is on, whether it is showing in theatres and its times, and online reviews from IMDB
* Users can leave reviews and see other users who have left those reviews and access their profile


**Optional Nice-to-have Stories**
* Chatting feature with other users
* Page where it lists all the movies that are popular on the app
### 2. Screen Archetypes

* After launch screen, there will be a login/ register page where users can login or register
* Checking your mood screen (Answer questions regarding mood, genre and type of rating you would be interested in watching)
* Settings screen would help you change your username, password, email and upload a photo
* Recommendation screen is a table full of movies that you would be interested in
* Mood clubs is a screen where you can join a community of people who have watched the same movie as you
* Profile screen allows users to find all the clubs that the user is associated with


### 3. Navigation

**Tab Navigation** (Tab to Screen)

* Mood checker
* Mood Club
* Profile
* Settings

**Flow Navigation** (Screen to Screen)

* Forced Log-In (Can register at this step)
* Choosing your mood and movie preferences
* Find the list of all the movies and once you click on a movie you are intested in, it will go to a screen where you can show the details of the movie such as the rating, streaming services and description of the movie
* You can join a community and in that community you can post and comment on posts relating to that movie.

## Wireframes
<img src=https://i.imgur.com/rmEwAQA.jpg width=600>

### [BONUS] Digital Wireframes & Mockups
<img src=https://i.imgur.com/gLKxoDn.png width=600>

### [BONUS] Interactive Prototype
<img src=https://i.imgur.com/LFroOSM.gif width=300>


## Schema 
### Models
#### Post for Profile Table

   | Property      | Type     | Description |
   | ------------- | -------- | ------------|
   | userId      | Int   | unique id for the user and will auto increment |
   | username        | String | username for user |
   | password         | Password (string)     | password for user |
   | name       | String   | user's name |

#### Post for Mood Table
   | Property      | Type     | Description |
   | ------------- | -------- | ------------|
   | moodId      | String   | unique id for the mood and will auto increment |
   | userId      | Int   | unique id for the user|
   | feeling       | Int (?)   | how the user is feeling that day |
   | movie_type | Number   | Genre that the user is interested in |
   | movie_rating    | Number   | rating for the movie that user is interested in |
  
#### Post for Club Table
   | Property      | Type     | Description |
   | ------------- | -------- | ------------|
   | club_id       | Int   | unique id for clubs|
   | club_name | Number   | number of comments that has been posted to an image |
   | post    | String   | what the user posted in the Club |
   | created_time     | DateTime | date when post is created (default field) |


### Networking
#### List of network requests by screen
   - Login Screen
      - (Read/GET) Check to see username and password is correct
         
      - (Create/POST) Create a new user (username, password, and name)
         ```swift
        func myMethod() {
          var user = PFUser()
          user.username = "myUsername"
          user.password = "myPassword"
          user.email = "email@example.com"
          // other fields can be set just like with PFObject
          user["phone"] = "415-392-0202"

          user.signUpInBackground {
            (succeeded: Bool, error: Error?) -> Void in
            if let error = error {
              let errorString = error.localizedDescription
              // Show the errorString somewhere and let the user try again.
            } else {
              // Hooray! Let them use the app now.
            }
          }
        }
        ```
   - Mood Screen
      - (Create/POST) Create a new mood post of the user into the database
      - (Read/GET) Check to see mode of the user
         ```swift
         let query = PFQuery(className:"Mood")
         query.whereKey("author", equalTo: currentUser)
         query.order(byDescending: "createdAt")
         query.findObjectsInBackground { (posts: [PFObject]?, error: Error?) in
            if let error = error { 
               print(error.localizedDescription)
            } else if let posts = posts {
               print("Successfully retrieved \(posts.count) posts.")
           // TODO: Do something with posts...
            }
         }
        ```



   - Club Screen
      - (Create/POST) Create a new post in club
      - (Read/GET) Check the posts from each user in the club
         ```swift
         let query = PFQuery(className:"Post")
         query.whereKey("author", equalTo: currentUser)
         query.order(byDescending: "createdAt")
         query.findObjectsInBackground { (posts: [PFObject]?, error: Error?) in
            if let error = error { 
               print(error.localizedDescription)
            } else if let posts = posts {
               print("Successfully retrieved \(posts.count) posts.")
           // TODO: Do something with posts...
            }
         }
        ```
        
        
       Mood and Search Page
       
       


https://user-images.githubusercontent.com/88856401/142971515-dc2d7801-8b4b-45da-bf7f-43bc2cedde77.mov

