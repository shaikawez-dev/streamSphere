# 📺 StreamSphere — A YouTube-Inspired Full-Stack Video Platform

> A feature-rich video sharing platform built with the MERN stack, extending the YouTube experience with an integrated **Tweet/microblogging** feature — letting creators share short updates alongside their video content.

---

## 🚀 Features

### 🎥 Video Management
- Upload, publish/unpublish, and stream videos with thumbnail support
- Track view counts, duration, and publish status per video
- Organize videos into custom playlists

### 👤 User System
- Secure authentication with **JWT (access + refresh tokens)**
- User profiles with avatar, cover image, and watch history
- Password hashing and session management

### 🐦 Tweet Feed *(Unique Feature)*
- Creators can post short text updates (tweets) independent of videos
- Builds a social layer on top of the video platform
- Tweet feed tied to user subscriptions

### 🔔 Subscriptions
- Subscribe/unsubscribe to channels
- Channel-subscriber relationship tracked in real time

### 💬 Comments
- Comment on videos with full CRUD support
- Comments linked to both the video and the author

### 👍 Likes
- Like videos, comments, and tweets
- Polymorphic likes model supporting multiple content types

### 📂 Playlists
- Create and manage video playlists
- Public/private playlist support with ownership control

---

## 🗄️ Data Models

| Model | Key Fields |
|-------|-----------|
| `users` | id, username, email, fullName, avatar, coverImage, watchHistory, refreshToken |
| `videos` | id, videoFile, thumbnail, owner, title, description, duration, views, isPublished |
| `tweets` | id, owner, content, createdAt |
| `comments` | id, content, video, owner |
| `likes` | id, video, comment, tweet, likedBy |
| `playlists` | id, name, description, videos[], owner |
| `subscriptions` | id, subscriber, channel |

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| **Backend** | Node.js, Express.js |
| **Database** | MongoDB, Mongoose (ODM) |
| **Auth** | JWT (Access + Refresh Tokens), bcrypt |
| **File Storage** | Cloudinary / Multer |
| **API Style** | RESTful APIs |

---

## 📁 Project Structure

```
src/
├── controllers/
│   ├── user.controller.js
│   ├── video.controller.js
│   ├── tweet.controller.js
│   ├── comment.controller.js
│   ├── like.controller.js
│   ├── playlist.controller.js
│   └── subscription.controller.js
├── models/
│   ├── user.model.js
│   ├── video.model.js
│   ├── tweet.model.js
│   ├── comment.model.js
│   ├── like.model.js
│   ├── playlist.model.js
│   └── subscription.model.js
├── routes/
├── middlewares/
│   ├── auth.middleware.js
│   └── multer.middleware.js
├── utils/
│   ├── cloudinary.js
│   └── ApiResponse.js
└── app.js
```

---

## ⚙️ Getting Started

### Prerequisites
- Node.js v18+
- MongoDB (local or Atlas)
- Cloudinary account (for media storage)

### Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/videotweet.git
cd videotweet

# Install dependencies
npm install

# Set up environment variables
cp .env.example .env
# Fill in your MongoDB URI, JWT secrets, and Cloudinary credentials

# Start the development server
npm run dev
```

### Environment Variables

```env
PORT=8000
MONGODB_URI=your_mongodb_connection_string
ACCESS_TOKEN_SECRET=your_access_token_secret
ACCESS_TOKEN_EXPIRY=1d
REFRESH_TOKEN_SECRET=your_refresh_token_secret
REFRESH_TOKEN_EXPIRY=10d
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret
```

---

## 📡 API Endpoints (Overview)

| Resource | Endpoints |
|----------|-----------|
| Auth | `POST /api/v1/users/register`, `/login`, `/logout`, `/refresh-token` |
| Videos | `GET /api/v1/videos`, `POST /`, `PATCH /:videoId`, `DELETE /:videoId` |
| Tweets | `POST /api/v1/tweets`, `GET /user/:userId`, `PATCH /:tweetId`, `DELETE /:tweetId` |
| Comments | `GET /api/v1/comments/:videoId`, `POST /`, `PATCH /:commentId` |
| Likes | `POST /api/v1/likes/toggle/v/:videoId`, `/c/:commentId`, `/t/:tweetId` |
| Playlists | `POST /api/v1/playlists`, `GET /:playlistId`, `PATCH /:playlistId` |
| Subscriptions | `POST /api/v1/subscriptions/c/:channelId`, `GET /c/:channelId` |

---

## 🧠 Key Design Decisions

- **Polymorphic Likes** — A single `likes` collection handles likes across videos, comments, and tweets using optional ObjectId references, keeping the schema clean and extensible.
- **Refresh Token Rotation** — Stored in the user document, enabling secure session persistence without compromising access token lifetime.
- **Watch History as Array** — Embedded directly in the user document for fast read access on the dashboard.
- **Tweet as First-Class Entity** — Tweets are a standalone model (not tied to videos), enabling a dedicated creator feed separate from video content.

---

## 🤝 Contributing

Pull requests are welcome! For major changes, please open an issue first to discuss what you'd like to change.

---

## 📄 License

[MIT](LICENSE)

---

> Built with ❤️ as a backend engineering deep-dive project.