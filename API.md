# API Documentation

## Firebase Collections Schema

### users Collection

```json
{
  "uid": "firebase_user_id",
  "email": "user@example.com",
  "displayName": "John Doe",
  "photoURL": "https://...",
  "role": "student",
  "department": "Computer Science",
  "phone": "09171234567",
  "createdAt": "2026-05-21T10:00:00Z",
  "preferences": {
    "darkMode": true,
    "notifications": true,
    "emailNotifications": true
  }
}
```

**Roles:**
- `student` - Regular student
- `faculty` - Faculty member
- `approver` - Can approve reservations
- `admin` - Full system access

---

### rooms Collection

```json
{
  "id": "room-301",
  "roomNumber": "301",
  "roomName": "Room 301",
  "building": "Building A",
  "floor": 3,
  "capacity": 40,
  "status": "available",
  "equipment": ["Projector", "Whiteboard", "AC"],
  "currentSubject": "Mathematics 101",
  "reservedBy": "Prof. John Smith",
  "reservedUntil": "2026-05-21T12:00:00Z",
  "createdAt": "2026-01-01T00:00:00Z"
}
```

**Status Values:**
- `available` - Room is free
- `occupied` - Room is in use
- `reserved` - Room is reserved

---

### reservations Collection

```json
{
  "id": "reservation_id",
  "roomId": "room-301",
  "roomName": "Room 301",
  "userId": "firebase_uid",
  "userName": "Jane Doe",
  "userEmail": "jane@example.com",
  "date": "2026-05-21",
  "startTime": "2026-05-21T14:00:00Z",
  "endTime": "2026-05-21T16:00:00Z",
  "purpose": "Study Group",
  "participants": 5,
  "requirements": "Projector, Whiteboard",
  "status": "pending",
  "approvedBy": "prof@example.com",
  "rejectionReason": "",
  "createdAt": "2026-05-21T10:00:00Z",
  "approvedAt": null,
  "rejectedAt": null
}
```

**Status Values:**
- `pending` - Awaiting approval
- `approved` - Approved and confirmed
- `rejected` - Rejected by approver
- `cancelled` - Cancelled by user

---

### schedules Collection

```json
{
  "id": "schedule_id",
  "roomId": "room-301",
  "startTime": "2026-05-21T09:00:00Z",
  "endTime": "2026-05-21T10:30:00Z",
  "subject": "Mathematics 101",
  "faculty": "Prof. John Smith",
  "facultyEmail": "john@sti.edu",
  "semester": "2026-1",
  "section": "A",
  "studentCount": 35,
  "createdAt": "2026-01-01T00:00:00Z"
}
```

---

### notifications Collection

```json
{
  "id": "notification_id",
  "userId": "firebase_uid",
  "type": "reservation_approved",
  "title": "Reservation Approved",
  "message": "Your reservation for Room 301 on 05/21 has been approved",
  "relatedId": "reservation_id",
  "read": false,
  "createdAt": "2026-05-21T10:00:00Z",
  "expiresAt": "2026-06-21T10:00:00Z"
}
```

**Notification Types:**
- `reservation_approved` - Reservation approved
- `reservation_rejected` - Reservation rejected
- `room_status_changed` - Room status changed
- `booking_reminder` - Upcoming booking reminder
- `system_announcement` - System announcement

---

## Application Events

### Authentication Events

```javascript
// User logs in
firebase.auth().onAuthStateChanged((user) => {
  if (user) {
    // User is signed in
  } else {
    // User is signed out
  }
});
```

### Real-time Listeners

```javascript
// Listen to room updates
db.collection('rooms').onSnapshot((snapshot) => {
  snapshot.docs.forEach(doc => {
    console.log(doc.data());
  });
});

// Listen to user's reservations
db.collection('reservations')
  .where('userId', '==', uid)
  .onSnapshot((snapshot) => {
    // Handle updates
  });
```

---

## Error Codes

### Authentication Errors
- `auth/invalid-email` - Invalid email format
- `auth/user-not-found` - User doesn't exist
- `auth/wrong-password` - Incorrect password
- `auth/user-disabled` - User account disabled
- `auth/too-many-requests` - Too many login attempts

### Database Errors
- `permission-denied` - No read/write permission
- `not-found` - Document not found
- `already-exists` - Document already exists
- `resource-exhausted` - Quota exceeded

---

## Usage Examples

### Create Reservation

```javascript
import { collection, addDoc, serverTimestamp } from "firebase/firestore";

const reservation = {
  roomId: "room-301",
  roomName: "Room 301",
  userId: auth.currentUser.uid,
  userName: auth.currentUser.displayName,
  userEmail: auth.currentUser.email,
  date: "2026-05-21",
  startTime: new Date("2026-05-21T14:00:00"),
  endTime: new Date("2026-05-21T16:00:00"),
  purpose: "Study Group",
  participants: 5,
  requirements: "Projector",
  status: "pending",
  createdAt: serverTimestamp()
};

await addDoc(collection(db, 'reservations'), reservation);
```

### Update Reservation Status

```javascript
import { doc, updateDoc, serverTimestamp } from "firebase/firestore";

await updateDoc(doc(db, 'reservations', reservationId), {
  status: 'approved',
  approvedBy: auth.currentUser.email,
  approvedAt: serverTimestamp()
});
```

### Get Room Details

```javascript
import { doc, getDoc } from "firebase/firestore";

const roomDoc = await getDoc(doc(db, 'rooms', 'room-301'));
if (roomDoc.exists()) {
  console.log(roomDoc.data());
}
```

### Query Reservations

```javascript
import { collection, query, where, getDocs } from "firebase/firestore";

const q = query(
  collection(db, 'reservations'),
  where('userId', '==', uid),
  where('status', '==', 'approved')
);

const querySnapshot = await getDocs(q);
querySnapshot.forEach(doc => {
  console.log(doc.data());
});
```

---

## Data Validation

### Client-side Validation

All inputs are validated before submission:

```javascript
// Email validation
const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
if (!emailRegex.test(email)) {
  throw new Error('Invalid email format');
}

// Date validation
const reservationDate = new Date(date);
if (reservationDate < new Date()) {
  throw new Error('Cannot reserve past dates');
}

// Participants validation
if (participants < 1 || participants > room.capacity) {
  throw new Error('Invalid participant count');
}
```

---

## Security Rules

### Basic Rules

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Any authenticated user can read
    match /{document=**} {
      allow read: if request.auth != null;
    }

    // Users can only write their own data
    match /users/{userId} {
      allow create, update: if request.auth.uid == userId;
      allow delete: if false;
    }

    // Only approvers can update reservations
    match /reservations/{document=**} {
      allow update: if request.auth.customClaims.approver == true;
    }
  }
}
```

---

## Rate Limiting

To prevent abuse, implement client-side delays:

```javascript
const RESERVATION_COOLDOWN = 2000; // 2 seconds
let lastReservationTime = 0;

async function submitReservation(data) {
  const now = Date.now();
  if (now - lastReservationTime < RESERVATION_COOLDOWN) {
    throw new Error('Please wait before submitting another request');
  }
  lastReservationTime = now;
  // Submit reservation
}
```

---

## Performance Tips

1. **Use indexes** for frequently queried fields
2. **Limit query results** with pagination
3. **Cache data** locally when possible
4. **Use field masks** to read/write only needed fields
5. **Batch operations** when possible

For detailed API reference, visit: [Firebase Firestore Documentation](https://firebase.google.com/docs/firestore)
