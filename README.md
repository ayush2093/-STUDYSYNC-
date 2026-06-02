# 📚 Online Study Collaboration Portal

A full-stack MERN (MongoDB, Express, React, Node.js) web application that combines an **online learning management system** with powerful **real-time group collaboration** features — giving students and instructors one unified platform to learn and work together.

---

## ✨ Features

### 👩‍🎓 Student Features
- Browse and purchase courses via **PayPal** integration
- Watch video lessons with progress tracking
- Take **tests/quizzes** and view results & history
- Join or create **study groups**
- Chat with groupmates in **real-time** (Socket.io)
- Upload and download **shared files** (up to 50MB)
- Participate in **group polls**
- Manage tasks within groups
- Access an AI-powered **chatbot** assistant

### 🧑‍🏫 Instructor Features
- Create and manage courses with video content
- Upload media via **Cloudinary**
- Build a course curriculum with multiple lectures
- Create and manage **tests** for students
- View student enrollment and progress via a dashboard
- Send messages to students

### 🛡️ Admin Features
- User management dashboard
- Course oversight and control
- Role-based access control (admin, instructor, student)

### ⚡ Real-Time Collaboration (Socket.io)
- Instant group messaging with typing indicators
- Online/offline member status tracking
- Real-time notifications for new messages, resources, and task updates
- Auto-reconnection on disconnect

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| **Frontend** | React 18, Vite, Tailwind CSS, shadcn/ui, Radix UI |
| **Backend** | Node.js, Express.js |
| **Database** | MongoDB (Mongoose) |
| **Real-time** | Socket.io |
| **Auth** | JWT (JSON Web Tokens), bcryptjs |
| **File Storage** | Cloudinary (media), Multer (group files) |
| **Payments** | PayPal REST SDK |
| **Email** | Nodemailer |
| **Animations** | Framer Motion |

---

## 📁 Project Structure

```
Online-Study-Collaboration-portal/
├── client/                        # React frontend (Vite)
│   ├── src/
│   │   ├── components/
│   │   │   ├── instructor-view/   # Instructor UI components
│   │   │   ├── student-view/      # Student UI components
│   │   │   ├── chatbot/           # AI chatbot widget
│   │   │   └── ui/                # Reusable shadcn/ui components
│   │   ├── pages/
│   │   │   ├── instructor/        # Instructor pages (courses, tests)
│   │   │   └── student/           # Student pages (home, groups, courses, tests)
│   │   ├── hooks/                 # Custom React hooks (useSocket, etc.)
│   │   ├── context/               # React Context providers
│   │   └── services/              # Axios API service functions
│   └── package.json
│
└── server/                        # Node.js/Express backend
    ├── controllers/               # Route handler logic
    ├── models/                    # Mongoose schemas
    │   ├── User.js
    │   ├── Course.js
    │   ├── Group.js
    │   ├── GroupMessage.js
    │   ├── GroupFile.js
    │   ├── GroupPoll.js
    │   ├── GroupTask.js
    │   ├── Test.js / TestResult.js
    │   └── Order.js
    ├── routes/                    # Express route definitions
    ├── socket/                    # Socket.io event handlers
    ├── middleware/                # Auth & admin middleware
    ├── helpers/                   # Cloudinary, email, PayPal helpers
    └── server.js                  # Entry point
```

---

## 🚀 Getting Started

### Prerequisites
- [Node.js](https://nodejs.org/) v18+
- [MongoDB Atlas](https://www.mongodb.com/cloud/atlas) account (or local MongoDB)
- [Cloudinary](https://cloudinary.com/) account (for media uploads)
- [PayPal Developer](https://developer.paypal.com/) account (for payments)

---

### 1️⃣ Clone the Repository

```bash
git clone https://github.com/ayush2093/-STUDYSYNC-
cd Online-Study-Collaboration-portal
```

---

### 2️⃣ Configure the Server

```bash
cd server
cp .env.example .env
```

Open `.env` and fill in your values:

```env
PORT=5000
MONGO_URI=mongodb+srv://<username>:<password>@cluster0.xxxxx.mongodb.net/<dbname>
CLIENT_URL=http://localhost:5173
JWT_SECRET=your_super_secret_jwt_key

# PayPal
PAYPAL_CLIENT_ID=your_paypal_client_id
PAYPAL_SECRET_ID=your_paypal_secret

# Cloudinary
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret

# Email (Nodemailer)
EMAIL_USER=your_email@gmail.com
EMAIL_PASS=your_email_app_password
```

Install dependencies and start:

```bash
npm install
npm run dev       # Development (nodemon)
# or
npm start         # Production
```

The server runs on **http://localhost:5000** 🟢

---

### 3️⃣ Configure the Client

```bash
cd client
```

Create a `.env` file:

```env
VITE_API_URL=http://localhost:5000
```

Install dependencies and start:

```bash
npm install
npm run dev
```

The client runs on **http://localhost:5173** 🟢

---

### 4️⃣ Create an Admin User

```bash
cd server
node create-admin.js
```

---

## 🔌 API Routes Overview

| Prefix | Description |
|---|---|
| `/auth` | Register, login, password reset |
| `/instructor/course` | Course CRUD for instructors |
| `/media` | Media upload via Cloudinary |
| `/student/course` | Course browsing for students |
| `/student/order` | PayPal course purchases |
| `/student/course-progress` | Track lesson completion |
| `/groups` | Study groups, chat, files, polls, tasks |
| `/tests` | Test creation, submission, results |
| `/admin` | Admin user/course management |
| `/chatbot` | AI chatbot endpoint |

---

## 🔧 Real-Time Features (Socket.io)

The server uses Socket.io for live collaboration inside study groups.

**Events emitted by client:**
- `join-group` — Join a group room
- `send-message` — Send a chat message
- `typing` / `stop-typing` — Typing indicator

**Events received by client:**
- `new-message` — A new chat message arrived
- `user-typing` — Someone is typing
- `online-users` — Updated online member list
- `notification` — New resource/task/message alert

---

## 🐛 Troubleshooting

**Socket.io not connecting?**
- Confirm the server is running on port 5000
- Check `VITE_API_URL` in the client `.env`
- Verify your JWT token is valid

**File uploads failing?**
- Files must be under **50MB**
- Ensure the `uploads/groups` directory exists on the server

**MongoDB not connecting?**
- Double-check your `MONGO_URI` in `.env`
- Make sure your IP is whitelisted in MongoDB Atlas

**PayPal errors?**
- Confirm you're using **sandbox** credentials during development

---

## 🗺️ Roadmap

- [x] Real-time chat & typing indicators
- [x] Online status tracking
- [x] File uploads in groups
- [x] Polls & voting
- [x] Tests & quiz history
- [x] AI chatbot assistant
- [ ] 🎥 Voice/Video rooms (WebRTC / Agora.io)
- [ ] 🖊️ Shared whiteboard (tldraw / Excalidraw)
- [ ] 📱 Mobile app (React Native)

---

## 📄 License

This project is licensed under the **ISC License**.

---

## 🙌 Contributing

Pull requests are welcome! For major changes, please open an issue first to discuss what you'd like to change.

1. Fork the repository
2. Create your feature branch: `git checkout -b feature/awesome-feature`
3. Commit your changes: `git commit -m 'Add awesome feature'`
4. Push to the branch: `git push origin feature/awesome-feature`
5. Open a Pull Request

---

> Built with ❤️ using the MERN stack + Socket.io