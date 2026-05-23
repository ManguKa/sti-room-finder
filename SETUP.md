# Environment Configuration Guide

## Firebase Setup Instructions

### Step 1: Create Firebase Project

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Click "Add project"
3. Enter project name: "STI-RoomFinder"
4. Enable Google Analytics
5. Create project

### Step 2: Configure Authentication

1. In Firebase Console, go to **Authentication**
2. Click **Get Started**
3. Enable these sign-in providers:
   - Email/Password
   - Google
   - Microsoft (for O365)

### Step 3: Create Firestore Database

1. Go to **Firestore Database**
2. Click **Create database**
3. Choose production mode
4. Select region closest to STI
5. Create database

### Step 4: Create Collections

Create these collections in Firestore:

#### users
- Auto ID documents
- Fields: email, displayName, photoURL, role, createdAt, preferences

#### rooms
- Document ID: room-[number]
- Sample data in `src/data/rooms.json`

#### reservations
- Auto ID documents
- Fields: roomId, userId, date, startTime, endTime, status, createdAt

#### schedules
- Auto ID documents
- Fields: roomId, startTime, endTime, subject, faculty, createdAt

#### notifications
- Auto ID documents
- Fields: userId, message, type, read, createdAt

### Step 5: Update Firebase Config

Edit `src/firebase/firebaseConfig.js`:

```javascript
const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  authDomain: "your-project.firebaseapp.com",
  projectId: "your-project-id",
  storageBucket: "your-project.appspot.com",
  messagingSenderId: "YOUR_SENDER_ID",
  appId: "YOUR_APP_ID",
  measurementId: "YOUR_MEASUREMENT_ID"
};
```

Get these values from Firebase Console > Project Settings > General tab

### Step 6: Set Security Rules

In Firestore, go to **Rules** tab and set:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read: if request.auth != null;
      allow write: if request.auth != null;
    }
  }
}
```

## Development Server Setup

### Option 1: VS Code Live Server

1. Install "Live Server" extension
2. Right-click `index.html`
3. Select "Open with Live Server"
4. Runs on http://localhost:5500

### Option 2: Python Server

```bash
# Python 3
python -m http.server 8000

# Python 2
python -m SimpleHTTPServer 8000
```

Access at http://localhost:8000

### Option 3: Node.js Server

```bash
# Install http-server globally
npm install -g http-server

# Run server
http-server
```

Access at http://localhost:8080

## Deployment

### Firebase Hosting

1. Install Firebase CLI:
   ```bash
   npm install -g firebase-tools
   ```

2. Login to Firebase:
   ```bash
   firebase login
   ```

3. Initialize Firebase:
   ```bash
   firebase init hosting
   ```

4. Deploy:
   ```bash
   firebase deploy
   ```

## Environment Variables

Create `.env` file (for reference only, not used in client-side):

```
FIREBASE_API_KEY=your_api_key
FIREBASE_AUTH_DOMAIN=your_auth_domain
FIREBASE_PROJECT_ID=your_project_id
FIREBASE_STORAGE_BUCKET=your_storage_bucket
FIREBASE_MESSAGING_SENDER_ID=your_sender_id
FIREBASE_APP_ID=your_app_id
```

## Testing

### Test Accounts

Create test accounts in Firebase Authentication:

1. **Student Account**
   - Email: student@test.com
   - Password: Test@12345

2. **Faculty Account**
   - Email: faculty@test.com
   - Password: Test@12345

3. **Approver Account**
   - Email: approver@test.com
   - Password: Test@12345

### Test Rooms

Sample room data is provided in `src/data/rooms.json`. Import via:

1. Firebase Console > Firestore
2. Collections > rooms > Add documents

## Troubleshooting

### Issue: "Firebase is not defined"
- Ensure firebaseConfig.js is properly imported
- Check CDN links are accessible

### Issue: "Authentication failed"
- Verify Firebase authentication is enabled
- Check Firebase project ID matches config

### Issue: "Firestore connection error"
- Ensure Firestore database is created
- Check security rules allow read/write
- Verify internet connection

### Issue: "3D Viewer not loading"
- Check Three.js CDN link
- Verify WebGL support in browser
- Check browser console for errors

## Performance Optimization

- Enable Cloud CDN in Firebase
- Optimize images and assets
- Use lazy loading for screens
- Implement pagination for large datasets
- Cache frequently accessed data

## Browser Support

- Chrome 90+
- Firefox 88+
- Safari 14+
- Edge 90+
- Mobile browsers (iOS Safari, Chrome Mobile)

## Accessibility

- WCAG 2.1 AA compliance
- Keyboard navigation support
- Screen reader friendly
- High contrast mode support
- Proper ARIA labels

---

For more help, check [Firebase Documentation](https://firebase.google.com/docs)
