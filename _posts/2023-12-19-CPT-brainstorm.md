---
toc: false
comments: false
layout: post
title: CPT Project Brainstorm
description: :D
type: ccc
courses: { csp: {week: 16} }
---

### Requirements
- Login Screen w/ different accounts to log into
- Database information storage
- Main Idea

---

**Code Review: Social Media/Blog Page with Login System**

**Overview:**
We will have a front page that has 2 main features: Post and Direct Messaging. The post feature will put out a post onto a main page that everyone else can see. Meanwhile, the direct messaging feature will send a message directly to someone else. 


**Strengths:**

1. **Team Collaboration:**
   - The use of team-based development aligns well with the collaborative nature of CPT projects.
   - Teams are encouraged to maintain their project time, promoting responsibility and effective time management.

2. **Ethical Computing:**
   - Clear guidelines on citing the use of teacher starters, generative AI code, and third-party resources demonstrate a commitment to ethical computing practices.

3. **Starter Code Refactoring:**
   - The recommendation to use starter code from `flask_portfolio` and `teacher_portfolio` is prudent.
   - The emphasis on refactoring code ensures a solid and appropriate foundation for individual projects.

4. **REST API and Database Paradigm:**
   - Integration of REST API and adherence to the Database paradigm showcase a structured and scalable approach to system development.

5. **Individual Project Selection:**
   - Encouraging students to pick projects based on their interests enhances motivation and engagement.
   - Teacher assistance in project selection adds a valuable guidance element.

6. **JWT Integration:**
   - Incorporating JWT login as a feature in all projects aligns with the cooperative practice of CPT requirements.
   - Ensuring that JWT is not for individual CPT submissions maintains clarity on its purpose.

7. **Collaborative Development Practices:**
   - The focus on co-development, concept sharing, write-ups, and video creation fosters a rich learning environment.
   - Student and teacher reviews contribute to continuous improvement and knowledge sharing.

8. **Multimedia Elements:**
   - Integration of multimedia elements, such as videos and write-ups, enhances the learning experience and promotes effective communication.

9. **Skill Development Emphasis:**
   - The end goal of developing high skills in language, process, and procedure for College Board standards is clearly communicated.

**Features:**
1. **Sign Up / Log in:**
   - Users can create unique accounts for themselves
     - Accounts have usernames/passwords
     - Their username will be the main method of identification
   - Users can log in whenever they want
     - Use indexing to verify the username/password combo
     - Use a .CSV file to store the account info
   - Concept Page:
   - ![CPT Login Image](/SAAK_repo/images/image_720.png)
  
2. **Direct Messaging:**
   - Allow users to search up users by username and send messages to them
   - Only the sender and the reciever can see the messages

3. **Posting:**
   - Send out a post that everyone else can see
   - Use databases to store each post (Size of each post should be negligble as storing text takes very little space)
   - ![Posting Concept Design](https://file%252B.vscode-resource.vscode-cdn.net/Users/Akhil/vscode/SAAK_repo/images/image.png?version%253D1705081160264)

4. **Likes:**
   - Allow users to be able to like posts
   - Store the amount of likes as metadata to the post

5. **Comment:**
   - Allow users to comment onto posts
   - The comment will be stored/displayed under the post it was commented under

**UML Drawings**
![UML Class interactions](/SAAK_repo/images/UML%2520Class%2520diagram.png)
