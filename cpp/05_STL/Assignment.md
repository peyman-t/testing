## Library Management System with STL

### Introduction

**Learning objectives** 
The assignment tests whether you can:

1. Understand and utilize the Standard Template Library (STL) in C++, including containers, iterators, algorithms, and function objects.
2. Implement modern memory management techniques using smart pointers, such as unique_ptr, shared_ptr, and weak_ptr.
3. Learn and apply lambda expressions in C++ for concise and efficient function definitions.

### Scenario
Develop a C++ program that simulates a social media platform, where users can post messages, follow other users, and view a feed of posts from the users they follow. Implement the necessary features using advanced C++ techniques such as the Standard Template Library, smart pointers, and lambda expressions.

In this project, you will develop a C++ program that simulates a simplified social media platform. The platform should allow users to perform the following actions:

1. Registration: Users can create accounts by providing a unique username. The system should assign a unique userID to each user upon registration.
2. Follow/Unfollow Users: Users can follow or unfollow other users by specifying the target user's userID. The system should maintain a list of followers for each user, taking care to prevent duplicate followers.
3. Create/Delete Posts: Users can create new posts with textual content and an automatically generated timestamp. Each post should be assigned a unique postID. Users should also be able to delete their posts by specifying the postID.
4. View Feed: Users can view a feed of posts from the users they follow. The feed should display posts sorted by timestamp, with the most recent posts appearing first. Optionally, you can implement additional sorting or filtering options, such as sorting by the number of likes or filtering by keywords.
5. Search Functionality: Implement a search functionality that allows users to search for other users by username, or search for posts based on keywords, author, or other criteria.

Requirements:

1. User and Post Classes:
    1. Create a User class with attributes such as userID, username, and a list of followers. Use appropriate STL containers for storage and management, such as std::vector or std::unordered_set.
    2. Create a Post class with attributes such as postID, userID (author), content, and timestamp.
    3. Implement methods in the User class for following and unfollowing other users, updating the list of followers accordingly.
2. STL Algorithms and Function Objects:
    1. Implement functionality to display a list of all users, sorted by username or userID, using STL algorithms such as std::sort.
    2. Use STL algorithms and function objects to filter posts based on criteria like author or content keywords.
    3. Implement a method to display a user's feed, showing posts from the users they follow, sorted by timestamp or other relevant criteria.
3. User Interface:
    1. Design a user-friendly command-line interface (CLI) for users to register, follow/unfollow other users, create/delete posts, and view their feeds.
    2. Implement basic input validation to prevent errors and ensure smooth operation of the platform.

Note: The social media platform simulation should be implemented in C++ using advanced techniques such as the Standard Template Library, smart pointers, and lambda expressions. The overall design should adhere to best practices for code efficiency, readability, and reusability. The source code should be well-structured, modular, and appropriately commented for readability and maintainability.

### Deliverable
A link to the git repository containing the program.