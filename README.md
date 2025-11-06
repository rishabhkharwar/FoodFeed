# 🍽️ FoodFeed

**A modern food-sharing and discovery app for users and food partners**

FoodFeed is a full-stack application that lets food partners create and share food items, and lets users browse, like, save, and interact with food posts. It includes authentication, media uploads, and a responsive React frontend built with Vite.

---

## ✨ What is FoodFeed?

FoodFeed is a lightweight social-style food discovery platform connecting food partners (restaurants, cooks, vendors) with users. Partners can create food posts (with images), and users can browse a feed, like and save items, and view partner profiles. The project is split into a Node.js/Express backend and a Vite + React frontend.

### Key Highlights

- Role-based auth: users and food partners
- Food posting with image upload
- Like and save features for user engagement
- Responsive frontend powered by Vite + React
- REST API built with Express and MongoDB (Mongoose)

---

## 🌟 Features

- Create, update, delete food posts (partners)
- Browse a feed of food posts (users)
- Like and save food posts
- User / Food partner authentication (JWT)
- Image uploads (ImageKit / multer integration)
- Simple, component-driven frontend with routing

---

## 🛠️ Tech Stack

### Backend
- Node.js + Express
- MongoDB via Mongoose
- JWT for authentication
- bcryptjs for password hashing
- multer for file handling
- imagekit (optional) for media storage

### Frontend
- Vite
- React
- react-router-dom
- axios for API calls

### Development tools
- ESLint for linting (frontend)

---

## 📁 Project Structure

```
FoodFeed/
├── backend/                    # Express backend
│   ├── .env                    # Environment variables (not committed)
│   ├── package.json            # backend scripts & deps
│   └── src/
│       ├── app.js              # Express app setup
│       ├── server.js           # Entry (root server.js exists)
│       ├── controllers/        # Route handlers
│       ├── db/                 # DB connection (mongoose)
│       ├── middlewares/        # Auth and helper middlewares
│       ├── models/             # Mongoose models (User, Food, etc.)
│       ├── routes/             # Route definitions
│       └── services/           # Storage and helper services
├── frontend/                   # Vite + React frontend
│   ├── package.json
│   ├── index.html
│   └── src/
│       ├── App.jsx
│       ├── main.jsx
│       ├── pages/              # Page components
│       ├── components/         # Reusable UI components
│       └── styles/             # CSS files
└── videos/                     # (optional) demo/asset videos
```

---

## 🚀 Quick Start

These instructions assume you're on Windows PowerShell (default for your workspace). Adjust commands for other shells as needed.

### Prerequisites

- Node.js 18+ and npm
- MongoDB (local or cloud, e.g. Atlas)
- Git

### Backend: install & run

Open a terminal, then:

```powershell
cd d:\FoodFeed\backend
npm install

# If you have a template .env.example, run:


# Start the backend server
npm start
```

The backend `package.json` in this project includes a start script that runs `node server.js`.

### Frontend: install & run

In a separate terminal:

```powershell
cd d:\FoodFeed\frontend
npm install
npm run dev
```

This will start the Vite dev server (default port printed by Vite). Open the printed local URL (usually http://localhost:5173) to view the app.

---

## 📖 Usage Guide

### Typical developer workflow

1. Start MongoDB (local or ensure Atlas connection is available).
2. Start backend: `cd backend && npm start`.
3. Start frontend: `cd frontend && npm run dev`.
4. Register a user or partner via the frontend auth pages and test create/browse flows.

### Environment variables (backend)

Create a `.env` file in `backend/` with at least:

```
# MongoDB connection
MONGO_URI="your_mongo_connection_string"

# JWT
JWT_SECRET=your_jwt_secret

# Optional: ImageKit (if used for uploads)
IMAGEKIT_PUBLIC_KEY=...
IMAGEKIT_PRIVATE_KEY=...
IMAGEKIT_URL_ENDPOINT=https://ik.imagekit.io/your_endpoint

# Optional: other keys
```

For the frontend you may set a variable for the API URL (optional):

```
VITE_API_URL=http://localhost:5000
```

(If you use this, reference it in your frontend axios base URL as `import.meta.env.VITE_API_URL`.)

---

## 🔌 API Reference (high-level)

The backend exposes REST endpoints under `src/routes/`. Example endpoints include:

### Authentication
- POST `/api/auth/register` — create a user/partner account
- POST `/api/auth/login` — authenticate and receive a JWT

### Food posts
- GET `/api/foods` — list feed items
- GET `/api/foods/:id` — get a single food post
- POST `/api/foods` — create a new food post (protected — partner)
- PUT `/api/foods/:id` — update a food post (protected — owner)
- DELETE `/api/foods/:id` — delete a food post (protected — owner)

### Food partner
- GET `/api/food-partners/:id` — get partner profile
- POST `/api/food-partners` — create/approve partner (depends on your flow)

### Likes & Saves
- POST `/api/likes` — like/unlike a post
- POST `/api/saves` — save/unsave a post

Note: Exact routes and request bodies are defined in `backend/src/routes` and handled by corresponding controllers in `backend/src/controllers/`.

---

## 🗄️ Data Models (Mongoose, example shapes)

These are simplified examples based on the models folder in the backend.

User (example)

```js
{
  _id: ObjectId,
  name: String,
  email: String,
  passwordHash: String,
  role: "user" | "partner",
  createdAt: Date
}
```

Food (example)

```js
{
  _id: ObjectId,
  title: String,
  description: String,
  images: [String], // image URLs
  price: Number,
  partnerId: ObjectId,
  likesCount: Number,
  savesCount: Number,
  createdAt: Date
}
```

Like / Save (example)

```js
{
  _id: ObjectId,
  userId: ObjectId,
  foodId: ObjectId,
  createdAt: Date
}
```

---

## 🚀 Deployment

### Quick production notes

- Use a managed MongoDB (Atlas) for production.
- Configure environment variables in your hosting provider.
- For simple deployments you can host the frontend as static assets (build with `npm run build` in `frontend/`) and host the backend on platforms like Heroku, Render, or a VPS.

### Build frontend for production

```powershell
cd d:\FoodFeed\frontend
npm run build
# Serve the built static files or integrate into your backend static serving
```

---

## 🤝 Contributing

Contributions are welcome. Suggested flow:

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/your-feature`
3. Implement your changes and add tests where appropriate
4. Open a pull request with a short description of the change

Please follow consistent commit message style and run linters/tests before submitting.

---

## 🐛 Troubleshooting

Common issues:

- Database connection errors: verify `MONGO_URI` and that the DB is reachable.
- Auth errors: ensure `JWT_SECRET` matches between tokens and validation.
- Image upload issues: check ImageKit / storage credentials and upload middleware.
- Frontend dev server not starting: ensure `vite` is installed and Node version is compatible.

Enable verbose logs in backend by adding debug prints or logging; check console output for stack traces.

---


## 🙏 Acknowledgments

Thanks to the community libraries used in this project (Express, Mongoose, Vite, React, ImageKit) and to the original project inspiration.

---

## 📞 Support

If you need help, open an issue in the repository or reach out to the project maintainer(s).


---

Made with ❤️ by the FoodFeed team
