# Quick Start Guide

## 🚀 5-Minute Setup

### Step 1: Get Firebase Credentials
1. Visit [Firebase Console](https://console.firebase.google.com/)
2. Create a new project
3. Go to Project Settings (⚙️ icon)
4. Copy the Web SDK config

### Step 2: Update Configuration
Edit `src/firebase/firebaseConfig.js` and paste your credentials:

```javascript
const firebaseConfig = {
  apiKey: "YOUR_KEY_HERE",
  authDomain: "your-project.firebaseapp.com",
  projectId: "your-project-id",
  storageBucket: "your-project.appspot.com",
  messagingSenderId: "YOUR_SENDER_ID",
  appId: "YOUR_APP_ID",
  measurementId: "YOUR_MEASUREMENT_ID"
};
```

### Step 3: Enable Authentication
In Firebase Console:
1. Go to **Authentication**
2. Click **Get Started**
3. Enable: Email/Password, Google, Microsoft

### Step 4: Create Firestore Database
1. Go to **Firestore Database**
2. Click **Create database** (Production Mode)
3. Select your region

### Step 5: Create Collections
1. Create collection: `rooms`
2. Create collection: `reservations`
3. Create collection: `users`
4. Create collection: `schedules`
5. Create collection: `notifications`

### Step 6: Run Locally
Choose one:

**Option A: VS Code**
- Install "Live Server" extension
- Right-click `index.html` → "Open with Live Server"
- Opens at `http://localhost:5500`

**Option B: Python**
```bash
python -m http.server 8000
# Access: http://localhost:8000
```

**Option C: Node.js**
```bash
npx http-server
# Access: http://localhost:8080
```

### Step 7: Test Login
- Click "Create Account"
- Sign up with test email
- Login with your account

## 📁 Project Structure

```
RoomFinder/
├── index.html                 ← Main entry point
├── src/
│   ├── app.js                ← Application controller
│   ├── firebase/
│   │   └── firebaseConfig.js ← Your Firebase config here
│   ├── pages/                ← Screen components
│   ├── models/               ← 3D viewer
│   ├── styles/
│   │   └── main.css          ← All styling
│   ├── utils/
│   │   └── themeManager.js   ← Dark/light mode
│   └── data/
│       └── rooms.json        ← Sample data
├── README.md                 ← Full documentation
├── SETUP.md                  ← Detailed setup
├── API.md                    ← API reference
└── FIXES.md                  ← What was fixed
```

## 🎯 Main Features

| Feature | Location | Status |
|---------|----------|--------|
| Login/Auth | `LoginScreen.js` | ✅ Ready |
| Dashboard | `DashboardScreen.js` | ✅ Ready |
| Room Status | `RoomStatusScreen.js` | ✅ Ready |
| Reservations | `ReservationScreen.js` | ✅ Ready |
| Approvals | `ApprovalScreen.js` | ✅ Ready |
| Profile | `ProfileScreen.js` | ✅ Ready |
| 3D Viewer | `Viewer3D.js` | ✅ Ready |
| Dark Mode | `themeManager.js` | ✅ Ready |

## 🔧 Troubleshooting

### "Firebase is not defined"
- Check `src/firebase/firebaseConfig.js` has correct credentials
- Verify `index.html` loads scripts correctly

### "Firestore connection failed"
- Ensure Firestore database is created
- Check security rules allow reads/writes
- Verify internet connection

### "3D Viewer not loading"
- Check browser supports WebGL
- Open DevTools (F12) > Console for errors
- Verify Three.js CDN is accessible

### "Login not working"
- Ensure Authentication is enabled in Firebase
- Verify Email/Password provider is enabled
- Check browser console for errors

## 📱 Features Checklist

- [x] Modern dark/light UI
- [x] Firebase authentication
- [x] Real-time room status
- [x] Room booking system
- [x] Approval workflow
- [x] 3D building viewer
- [x] Responsive design
- [x] User profiles
- [x] Notifications
- [x] Dark mode toggle

## 🚀 Next Steps

1. **Test Login** - Create test account
2. **Explore Screens** - Click through all screens
3. **Test Reservations** - Try booking a room
4. **Configure Approvals** - Set user roles
5. **Deploy to Firebase** - Follow SETUP.md

## 📊 Sample Room Data

Pre-configured rooms in `src/data/rooms.json`:
- Room 101, 102 (Floor 1)
- Room 201, 202 (Floor 2)
- Room 301, 302 (Floor 3)
- Room 401, 402 (Floor 4)

## 🎓 Key Technologies

- **Frontend**: HTML5, CSS3, JavaScript (ES6+)
- **3D Graphics**: Three.js
- **Backend**: Firebase Firestore + Authentication
- **Hosting**: Firebase Hosting (optional)
- **Styling**: CSS Custom Properties + Responsive Design

## 📞 Support

Stuck? Check:
1. `README.md` - Full documentation
2. `SETUP.md` - Detailed setup guide
3. `API.md` - API reference
4. `FIXES.md` - What was corrected
5. [Firebase Docs](https://firebase.google.com/docs)

## ⚡ Performance Tips

- Use browser cache
- Enable Firestore indexing
- Lazy load 3D models
- Optimize images
- Use CDN for static files

## 🔐 Security

- All Firebase security rules configured
- Authentication required for access
- Input validation on all forms
- XSS protection enabled
- CORS headers configured

## 📈 Deployment

Ready to deploy?

**Firebase Hosting:**
```bash
npm install -g firebase-tools
firebase login
firebase init hosting
firebase deploy
```

See SETUP.md for detailed deployment steps.

---

**Ready to use! Build amazing things with STI RoomFinder!** 🎉

Questions? Check the documentation or Firebase official guides.
