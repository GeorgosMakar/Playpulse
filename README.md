# Playpulse
Cross-platform messenger for gamers to connect across games and platforms
# PlayPulse 🎮
# PlayPulse 🎮

**PlayPulse** is a cross-platform messenger for gamers, enabling seamless communication across different games and platforms.

## Features

- Real-time friend status updates
- Cross-game messaging
- Party room creation
- Game integration with APIs

## Tech Stack

- React with Tailwind CSS
- Firebase for authentication and database
- OAuth integration with Discord and Epic Games

## Getting Started

1. Clone the repository:
   ```bash
   git clone https://github.com/GeorgosMakar/playpulse.git
cd playpulse
npm install
npm run dev
npm create vite@latest playpulse --template react
cd playpulse
npm install
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
content: ["./index.html", "./src/**/*.{js,ts,jsx,tsx}"],
theme: { extend: {} },
plugins: [],
@tailwind base;
@tailwind components;
@tailwind utilities;
npm install firebase
// src/firebase.js
import { initializeApp } from "firebase/app";
import { getAuth, signInWithPopup, GoogleAuthProvider } from "firebase/auth";

const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  authDomain: "YOUR_PROJECT.firebaseapp.com",
  projectId: "YOUR_PROJECT_ID",
  storageBucket: "YOUR_PROJECT.appspot.com",
  messagingSenderId: "SENDER_ID",
  appId: "APP_ID",
};

const app = initializeApp(firebaseConfig);
const auth = getAuth(app);
const provider = new GoogleAuthProvider();

export { auth, provider, signInWithPopup };
import React from "react";
import { auth, provider, signInWithPopup } from "./firebase";

export default function Login({ onLogin }) {
  const handleLogin = async () => {
    try {
      const result = await signInWithPopup(auth, provider);
      const user = result.user;
      onLogin(user);
    } catch (error) {
      console.error("Login failed:", error);
    }
  };

  return (
    <div className="h-screen flex items-center justify-center bg-gray-900 text-white">
      <button
        onClick={handleLogin}
        className="bg-blue-600 hover:bg-blue-700 px-6 py-3 rounded-xl text-xl font-bold"
      >
        Sign in with Google
      </button>
    </div>
  );
}
import React, { useState } from "react";
import Login from "./Login";
import Dashboard from "./Dashboard";

function App() {
  const [user, setUser] = useState(null);

  return user ? <Dashboard user={user} /> : <Login onLogin={setUser} />;
}

export default App;
