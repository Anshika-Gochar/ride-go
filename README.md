# Ride Booking Platform (Real-Time Driver & Customer Tracking)

![React Native](https://img.shields.io/badge/React_Native-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)
![Express.js](https://img.shields.io/badge/Express.js-000000?style=for-the-badge&logo=express&logoColor=white)
![Socket.IO](https://img.shields.io/badge/Socket.IO-010101?style=for-the-badge&logo=socketdotio&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-4EA94B?style=for-the-badge&logo=mongodb&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-007ACC?style=for-the-badge&logo=typescript&logoColor=white)

A full-stack, real-time ride-booking application built with React Native and an event-driven Node.js backend. Features live driver-passenger location streaming, automated state machines, geospatial proximity matching, and dual-token JWT authentication across HTTP and WebSocket channels.

---

## 🚀 Key Features

- **Real-Time Bidirectional Tracking**: Sub-second location streaming between rider and passenger using WebSockets (Socket.IO).
- **Geospatial Proximity Matching**: Dynamic radius search pairing pickup coordinates with active on-duty drivers via `geolib`.
- **Battery & Network Optimization**: Threshold-based GPS throttling prevents excessive battery drain and reduces redundant network traffic.
- **Secure Dual-Token Authentication**: JWT Access and Refresh token lifecycle protecting both REST endpoints and WebSocket handshakes.
- **State Management**: Predictable ride lifecycles (`IDLE` → `SEARCHING` → `ACCEPTED` → `IN_TRANSIT` → `COMPLETED`).
- **Interactive Maps**: Marker smoothing using animated coordinates for fluid vehicle transitions without visual jumping or jank.

---

## 🛠️ Architecture & Tech Stack

### Client (React Native)
- **Framework**: React Native / Expo (TypeScript)
- **State Management**: Zustand
- **Real-Time Client**: `socket.io-client`
- **Mapping & Location**: `react-native-maps`, Geolocation services

### Server (Node.js & Express)
- **Runtime**: Node.js (ES Modules)
- **Framework**: Express.js
- **Database**: MongoDB with Mongoose ODM
- **Real-Time Protocol**: Socket.IO
- **Geospatial Engine**: `geolib`
- **Security**: `jsonwebtoken` (JWT), `bcryptjs`

---

## 📡 WebSocket Event Flow

| Event Name | Direction | Payload / Purpose |
| :--- | :--- | :--- |
| `goOnDuty` | Client (Driver) → Server | Registers driver into the active pool with initial coordinates. |
| `goOffDuty` | Client (Driver) → Server | Removes driver from active matching and duty rooms. |
| `updateLocation` | Client (Driver) → Server | Sends throttled coordinate updates broadcasted to subscribed passengers. |
| `searchrider` | Client (Passenger) → Server | Initiates proximity search for nearby drivers with retry intervals. |
| `rideAccepted` | Client (Driver) → Server | Confirms ride acceptance and links driver to passenger room. |
| `cancelRide` | Client → Server | Clears active search session and removes pending ride records. |

---

## ⚙️ Getting Started

### Prerequisites
- Node.js (v18+)
- MongoDB Atlas or local MongoDB instance

### Installation & Setup

1. **Clone the repository:**
   ```bash
   git clone https://github.com/Anshika-Gochar/ride-booking-app.git
   cd ride-booking-app
   ```

2. **Install dependencies:**
   ```bash
   npm install
   ```

3. **Configure Environment Variables:**
   Create a `.env` file from `.env.example`:
   ```env
   PORT=3000
   MONGO_URI=your_mongodb_connection_string
   ACCESS_TOKEN_SECRET=your_access_token_secret
   ACCESS_TOKEN_EXPIRY=4d
   REFRESH_TOKEN_SECRET=your_refresh_token_secret
   REFRESH_TOKEN_EXPIRY=30d
   ```

4. **Start the Development Server:**
   ```bash
   npm start
   ```

---

## 📄 License
This project is licensed under the MIT License.
