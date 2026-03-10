# Secure Snap

Secure Snap is a full-stack web application for protecting a user's digital identity by managing face image uploads, tracking potential misuse alerts, and recording consent decisions. The project combines a React frontend with a Node.js/Express backend and MongoDB for persistent storage.

## Overview

The application is designed around a privacy-first workflow:

- Users can create an account and sign in securely.
- Users can upload facial images for monitoring.
- The system stores uploaded images and metadata.
- Detection alerts can be reviewed and marked as approved or denied.
- Profile preferences such as sensitivity, connected accounts, and subscription details can be updated.

## Features

- User signup and login with hashed passwords using `bcryptjs`
- JWT-based authentication
- Image upload support using `multer`
- MongoDB persistence using `mongoose`
- Detection alert history and consent decisions
- Profile management for:
  - Aadhaar verification status
  - Monitoring sensitivity
  - Connected social accounts
  - Subscription plan
- Responsive React UI with multiple pages and protected app flows

## Tech Stack

### Frontend

- React
- React Router
- Tailwind CSS
- Create React App

### Backend

- Node.js
- Express
- MongoDB
- Mongoose
- Multer
- JSON Web Token
- bcryptjs

## Project Structure

```text
secure_snap/
├── public/
├── src/
│   ├── assets/
│   ├── components/
│   └── pages/
├── server/
│   ├── lib/
│   ├── middleware/
│   ├── models/
│   ├── uploads/
│   └── index.js
├── .env.example
├── package.json
└── README.md
```

## Pages

- `Login` - user authentication
- `SignUp` - new account creation
- `Home` - image upload dashboard
- `Uploads` - uploaded image history
- `Warnings` - detection alert history and consent actions
- `Profile` - security preferences and account settings

## Backend Models

The MongoDB database uses these collections:

- `users`
- `profiles`
- `uploads`
- `warnings`

## Environment Variables

Create a `.env` file in the project root. The project currently expects:

```env
MONGO_URI=mongodb://127.0.0.1:27017/secure_snap
JWT_SECRET=replace-with-a-strong-secret
PORT=4000
```

An example file is already included at `.env.example`.

## MongoDB Setup

This project is configured to work with a local MongoDB instance by default.

### Using MongoDB Compass

Use this connection string in MongoDB Compass:

```text
mongodb://127.0.0.1:27017
```

After the backend runs and data is created, you should see a database named `secure_snap`.

## Installation

Clone the repository and install dependencies:

```bash
npm install
```

## Running the Project

### 1. Start MongoDB

Make sure MongoDB is running locally on `127.0.0.1:27017`.

### 2. Start the backend server

```bash
npm run start:server
```

The backend runs on:

```text
http://localhost:4000
```

### 3. Start the frontend

In a separate terminal:

```bash
npm start
```

The frontend runs on:

```text
http://localhost:3000
```

## Available Scripts

In the project directory, you can run:

- `npm start` - starts the React frontend
- `npm run start:server` - starts the Express backend
- `npm run build` - builds the frontend for production
- `npm test` - runs frontend tests

## API Summary

### Authentication

- `POST /api/auth/signup`
- `POST /api/auth/login`

### Uploads

- `GET /api/uploads`
- `POST /api/uploads`
- `DELETE /api/uploads/:id`

### Warnings

- `GET /api/warnings`
- `POST /api/warnings/detect`
- `PATCH /api/warnings/:id/status`

### Profile

- `GET /api/profile`
- `PATCH /api/profile`

### Health Check

- `GET /api/health`

## Authentication Flow

- On signup or login, the backend returns a JWT token.
- The frontend stores the token in `localStorage`.
- Authenticated API requests send the token using the `Authorization: Bearer <token>` header.

## File Upload Notes

- Uploaded images are stored in `server/uploads`.
- The backend serves them statically through `/uploads/...`.
- Maximum upload size is `10 MB`.
- Only image files are accepted.

## Current Status

The project currently supports:

- Full frontend UI flow
- Express backend with MongoDB integration
- Local MongoDB usage through Compass
- Persistent storage for users, uploads, warnings, and profile data

## Future Improvements

- Route protection on the frontend
- Better error handling and loading states
- Role-based access control
- Real detection engine integration
- Cloud file storage
- MongoDB Atlas deployment
- Automated backend tests

## Screens and Flow

Typical user flow:

1. Sign up or log in
2. Upload one or more face images
3. Review upload history
4. Trigger or review detection alerts
5. Approve or deny detected usage
6. Update monitoring and profile settings

## Security Notes

- Passwords are never stored in plain text.
- Passwords are hashed using `bcryptjs`.
- Protected routes require JWT authentication.
- The default local MongoDB setup is only accessible on your own machine unless you explicitly expose it.

## Deployment Notes

For production deployment, update:

- `MONGO_URI` to a production MongoDB instance such as MongoDB Atlas
- `JWT_SECRET` to a strong private secret
- CORS configuration in the backend
- Static asset and upload storage strategies 

## License

This project currently does not include a license file. Add one before making the repository public if needed.
