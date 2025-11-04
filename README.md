# Product Store (MERN Crash Course)

A full‑stack CRUD app built with the MERN stack where you can create, read, update, and delete simple products with a name, price, and image URL. The project demonstrates a clean Express API, a MongoDB data layer via Mongoose, and a modern React UI using Chakra UI and Zustand for state.

• Live site: https://mern-crash-course-yaa3.onrender.com  
• GitHub repo: https://github.com/LukeZHar/mern-crash-course

## Features

- Browse products in a responsive grid
- Create a new product (name, price, image URL)
- Edit an existing product
- Delete a product
- Dark/light color mode toggle
- Simple, optimistic UI updates using Zustand

## Tech stack

- Frontend: React 19, Vite, React Router 7, Chakra UI, Zustand
- Backend: Node.js, Express 5
- Database: MongoDB with Mongoose 8
- Deployment: Render (serving the built frontend from the Express server in production)

## Project structure

```
mern-crash-course/
├─ backend/
│  ├─ server.js               # Express app w/ API + static file serving in prod
│  ├─ config/db.js            # Mongo connection helper
│  ├─ controllers/
│  │  └─ product.controller.js
│  ├─ models/
│  │  └─ product.model.js     # name, price, image (+timestamps)
│  └─ routes/
│     └─ product.route.js
├─ frontend/
│  ├─ src/
│  │  ├─ App.jsx              # Routes and layout
│  │  ├─ main.jsx             # App bootstrap (Router + Chakra)
│  │  ├─ components/
│  │  │  ├─ Navbar.jsx
│  │  │  └─ ProductCard.jsx
│  │  ├─ pages/
│  │  │  ├─ HomePage.jsx
│  │  │  └─ CreatePage.jsx
│  │  └─ store/product.js     # Zustand store for products
│  ├─ vite.config.js          # Dev proxy -> http://localhost:5000/api
│  └─ package.json
└─ package.json                # Root scripts (dev/build/start)
```

## Data model

Product

```
{
	name: String,   // required
	price: Number,  // required
	image: String,  // required (URL)
	createdAt: Date,
	updatedAt: Date
}
```

## REST API

Base URL: `/api/products`

- GET `/` — list all products
- POST `/` — create a product `{ name, price, image }`
- PUT `/:id` — update a product by id
- DELETE `/:id` — delete a product by id

## Getting started (local dev)

Prerequisites

- Node.js 18+ and npm
- A MongoDB connection string (local or cloud)

1. Clone and install

```bash
git clone https://github.com/LukeZHar/mern-crash-course.git
cd mern-crash-course
npm run build
```

2. Create a `.env` file at the project root

```
MONGO_URI=<your-mongodb-connection-string>
PORT=5000   # optional; defaults to 5000
NODE_ENV=development
```

3. Run backend and frontend

```bash
npm run start
```

## Deployment (Render)

This repo is set up to serve the built React app from the Express server in production.

- Build Command: `npm run build`
- Start Command: `npm start`
- Env Vars: `MONGO_URI`, `NODE_ENV=production`

Render will run the build at the repo root, build the frontend, and then serve `frontend/dist` from Express.

## Useful scripts

- `npm run dev` — Start the API with nodemon on port 5000
- `npm run build` — Install frontend deps and build the React app
- `npm start` — Start the Express server in production mode
- `npm run dev` (in `frontend/`) — Start Vite dev server with API proxy

## Notes & decisions

- State management is done with Zustand for simplicity and minimal boilerplate.
- Chakra UI enables quick, accessible styling and easy color mode switching.
- The API validates basic requirements (name, price, image) and returns consistent `{ success, data|message }` payloads.
