# PrintFlow — Online Document Printing Platform

A full-stack web application where students upload documents and send them to nearby print shops for printing.

---

## Tech Stack

- **Frontend**: React 19, Vite, Tailwind CSS v4, React Router DOM, Axios, React Hook Form, Framer Motion
- **Backend**: Node.js, Express.js, MongoDB Atlas, Mongoose, JWT, bcrypt, Multer, Cloudinary

---

## Project Structure

```
/
├── frontend/          # React + Vite frontend
└── backend/           # Express.js backend
```

---

## Setup Instructions

### 1. Clone & Install

```bash
# Install backend dependencies
cd backend
npm install

# Install frontend dependencies
cd ../frontend
npm install
```

### 2. Configure Backend Environment

Copy `.env.example` to `.env` in the `/backend` folder and fill in:

```env
PORT=5000
MONGODB_URI=mongodb+srv://<username>:<password>@cluster0.mongodb.net/printflow
JWT_SECRET=your_super_secret_key
JWT_EXPIRE=7d

# Optional: Cloudinary (if not set, uses local storage)
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret

CLIENT_URL=http://localhost:5173
```

> **Without Cloudinary**: Files are stored locally in `/backend/uploads/`. This is fine for development.

### 3. Run the Application

```bash
# Terminal 1 — Backend
cd backend
npm run dev

# Terminal 2 — Frontend
cd frontend
npm run dev
```

- Frontend: http://localhost:5173
- Backend API: http://localhost:5000

---

## User Roles

### Student
- Register/Login at `/login`
- Upload documents (PDF, PNG, JPG)
- Configure print settings
- Select print shop
- Submit order and receive 6-digit OTP
- Track order status

### Admin (Print Shop Owner)
- Register/Login at `/admin/login`
- View incoming orders dashboard
- Verify student OTP to unlock documents
- Update order status (Accept → Printing → Ready → Completed)

---

## Order Status Flow

```
Pending → Waiting for OTP → OTP Verified → Printing → Ready for Pickup → Completed
```

---

## API Endpoints

### Auth
- `POST /api/auth/student/register`
- `POST /api/auth/student/login`
- `POST /api/auth/admin/register`
- `POST /api/auth/admin/login`
- `GET  /api/auth/me`

### Orders
- `POST   /api/orders` — Create order (with file upload)
- `GET    /api/orders/student` — Student's orders
- `GET    /api/orders/admin` — Admin's orders
- `GET    /api/orders/admin/stats` — Dashboard stats
- `GET    /api/orders/shops` — Available print shops
- `GET    /api/orders/:id` — Single order
- `POST   /api/orders/:id/verify-otp` — Verify OTP
- `PATCH  /api/orders/:id/status` — Update status
