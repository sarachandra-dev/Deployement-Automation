# CodeRoom – Real-Time Temporary Chat Rooms + Public Doubt Discussion Platform

<p align="center">
  <b>A full-stack real-time communication platform built for quick collaboration, anonymous group discussions, and technical doubt solving.</b>
</p>

📌 Overview

**CodeRoom** is a **full-stack real-time collaboration platform** that combines:

- **Temporary private chat rooms** for instant group communication
- **Public doubt discussion board** for persistent Q&A conversations

The project was designed to solve a practical problem:

> Students and small groups often need a **quick room-based communication space** for interview preparation, coding discussions, or group study **without the friction of login/signup**. At the same time, they also need a **persistent public discussion area** where doubts and answers can be stored for later access.

To solve this, CodeRoom uses **two different storage strategies** based on the nature of data:

- **Redis** → for **temporary private room state**, room members, and real-time room chat data
- **MongoDB** → for **persistent public doubt posts and replies**

This makes CodeRoom a hybrid platform for **instant collaboration + long-term doubt solving**.

---

🚀 Why this project is different

Most messaging applications are either:

- focused only on **real-time chat**
- or focused only on **public discussion / forum-based communication**

**CodeRoom combines both** in a single application:

1) Temporary Private Rooms
- Create a room instantly
- Share a unique room code
- Let up to **5 users** join without login
- Use it for **quick interview discussion / coding collaboration / group study**

2) Public Doubt Board
- Ask technical doubts publicly using only a nickname
- View all posts from other users
- Open discussions and reply to posts
- Build a persistent knowledge-sharing space

This combination makes the project more meaningful than a standard “chat app clone”.

---

✨ Core Features

1. Temporary Private Chat Rooms
- Create a private room without authentication
- Generate a unique room code
- Join room using **nickname + room code**
- Support **up to 5 users per room**
- Real-time room-based chat using **Socket.IO**
- Online users tracking
- Typing indicator support
- Temporary room and chat storage using **Redis**
- Room expiry support for auto-cleanup of temporary sessions

2. Public Doubt Discussion Board
- Create public technical doubt posts without login
- Add title, description, and tags
- View all public doubt posts
- Open a single post and read full discussion
- Add replies to public posts
- Store posts and replies permanently in **MongoDB**

3. Anonymous and Fast User Experience
- No signup / no login
- Only nickname-based interaction
- Lower friction for quick collaboration

4. Full-Stack Real-Time Architecture
- React frontend
- Express REST APIs
- Socket.IO for bi-directional real-time messaging
- Redis for ephemeral room state
- MongoDB for persistent public discussion content

---

🧠 Problem Statement

Traditional chat apps are not optimized for **temporary academic or coding collaboration**.

A student preparing for an interview or discussing a coding problem with friends usually needs:

- a room that can be created quickly
- no authentication barrier
- instant real-time communication
- a way to share doubts publicly when the discussion should be persistent

Existing apps often solve only one part of this problem.

**CodeRoom** addresses this gap by offering:

- **ephemeral room-based collaboration**
- **persistent public doubt discussion**
- **nickname-only access**
- **separate storage strategies for temporary vs permanent data**

---

💡 Solution Approach

CodeRoom is designed as a **two-module communication platform**:

Module A – Private Temporary Collaboration Rooms
Used for:
- quick group chat
- interview prep discussion
- temporary team communication
- small coding sessions

How it works
1. User creates a room
2. Backend generates a room code
3. Room is stored in Redis
4. Other users join using room code + nickname
5. All room communication happens in real time through Socket.IO
6. Room data remains temporary and can expire automatically

---

Module B – Public Doubt Discussion Board
Used for:
- asking doubts publicly
- viewing other users’ technical questions
- replying to discussions
- building a small persistent community Q&A board

How it works
1. User creates a public post with title, description, tag, and nickname
2. Backend stores it in MongoDB
3. Other users browse posts and open a discussion
4. Replies are added and stored persistently

---

🏗️ System Architecture

```text
                        +----------------------+
                        |      React Client    |
                        |  (UI + API + Socket) |
                        +----------+-----------+
                                   |
             ----------------------------------------------
             |                                            |
             | REST APIs                                  | Socket Events
             v                                            v
+----------------------------+              +-----------------------------+
|    Node.js + Express API   |              |   Socket.IO Event Server    |
+-------------+--------------+              +-------------+---------------+
              |                                             |
              |                                             |
              v                                             v
      +---------------+                           +------------------+
      |   MongoDB     |                           |      Redis       |
      | Public Posts  |                           | Temporary Rooms  |
      | Replies       |                           | Members/Messages |
      +---------------+                           +------------------+
