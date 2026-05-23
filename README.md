# STI RoomFinder - Real-Time Classroom Tracker and Booking System

A modern, interactive web application designed to help STI students and faculty find available classrooms in real time using an interactive 3D school building viewer and room reservation system.

## 🎯 Problem Statement

Students waste time searching for vacant classrooms or study areas because there is no centralized system for checking room availability in real time.

## 👥 Target Users

- **STI Students** - Find and book available study spaces
- **Faculty Members** - Manage class schedules and room allocations
- **Department Chairs** - Oversee room usage and scheduling
- **Laboratory Facilitators** - Manage lab availability

## ✨ Main Features

### 1. **Live Status Dashboard**
   - Real-time display of all classrooms
   - Show current room availability
   - Display pending reservations
   - Search functionality for classrooms
   - Filter by building/floor

### 2. **Schedule Synchronization**
   - Integrates with STI calendars
   - Automatic room status updates
   - Conflict detection and prevention

### 3. **Authentication**
   - STI O365 Login Integration
   - Email/Password authentication
   - Google Sign-In support

### 4. **Room Reservation System**
   - Students can request room reservations
   - Specify date, time, and duration
   - Add room requirements (projector, whiteboard, etc.)
   - View reservation history

### 5. **Approval Workflow**
   - Admin/faculty can approve or reject reservations
   - Approved reservations automatically change room status
   - Notifications for approval/rejection

### 6. **Notification Alerts**
   - Real-time notifications for approvals
   - Reservation reminders
   - Room status changes

### 7. **Interactive 3D Building Viewer**
   - 3D visualization of school building using Three.js
   - Click on classrooms to view details
   - Real-time color updates:
     - **Green** = Available
     - **Red** = Occupied
     - **Blue** = Reserved
   - Orbit camera controls
   - Zoom and rotate functionality

## 🏗️ Technology Stack

### Frontend
- **HTML5** - Semantic markup
- **CSS3** - Modern styling with custom properties
- **JavaScript (ES6+)** - Core application logic
- **Three.js** - 3D building visualization
- **Tailwind CSS** - Utility-first styling
- **Font Awesome** - Icon library

### Backend
- **Firebase Firestore** - Real-time database
- **Firebase Authentication** - User authentication
- **Firebase Hosting** - Application hosting

### Development
- **Modern browsers** - Chrome, Firefox, Safari, Edge
- **Responsive design** - Mobile-friendly layouts
- **Dark/Light mode** - Theme switching

## 📱 Required Screens

1. **Login Screen** - User authentication
2. **Dashboard Screen** - Main overview with stats
3. **Room Status Grid Screen** - Visual room availability
4. **Reservation Form Screen** - Book a room
5. **Approval Dashboard** - Manage reservations
6. **Profile and Settings Screen** - User preferences
7. **3D Interactive Building Screen** - 3D visualization

## 📊 Dashboard Requirements

- Display all classrooms with status
- Show real-time room availability
- Display current user's reservations
- Search classroom feature
- Filter by building/floor/status

## 📅 Reservation System

- Students can request room reservations
- Specify date, time, and duration
- Add special requirements
- Admin approval/rejection workflow
- Automatic status updates

## 🗄️ Database Collections

### users
- User profile information
- Authentication data
- Preferences and settings
- Role information

### rooms
- Room details and metadata
- Current status (available/occupied/reserved)
- Equipment and facilities
- Capacity information
- Building and floor information

### reservations
- Booking records (CRUD)
- Status tracking (pending/approved/rejected)
- User and room references
- Time details
- Special requirements

### schedules
- Integration with class schedules
- Automatic room occupancy
- Class information
- Faculty assignments

### notifications
- Reservation updates
- Approval/rejection alerts
- Room status changes
- System announcements

## 📦 Room Data Example

```json
{
    "roomName": "Room 301",
    "roomNumber": "301",
    "building": "Building A",
    "floor": 3,
    "capacity": 40,
    "status": "available",
    "equipment": ["Projector", "Whiteboard", "AC"],
    "currentSubject": "",
    "reservedBy": ""
}
```

## 🎨 3D Viewer Features

- **Interactive 3D Building** - Visualize entire school building
- **Dynamic Room Representation** - Each classroom is clickable
- **Real-time Status Updates** - Room colors change based on availability
- **Smooth Camera Movement** - Orbit controls with smooth transitions
- **Zoom Controls** - Zoom in/out for detailed viewing
- **Room Details** - Click room to view information and reserve

## 🎨 UI Design

- **Modern Futuristic Dashboard** - Sleek, professional appearance
- **Responsive Mobile-Friendly Layout** - Works on all devices
- **Dark/Light Mode Support** - User theme preference
- **Clean Cards and Navigation** - Intuitive user experience
- **Real-time Updates** - Live status changes
- **Smooth Transitions** - Polished animations

## 📁 Project Folder Structure

```
RoomFinder/
├── index.html                 # Main HTML file
├── src/
│   ├── app.js                # Main application controller
│   ├── components/           # Reusable components
│   ├── pages/               # Screen components
│   │   ├── LoginScreen.js
│   │   ├── DashboardScreen.js
│   │   ├── RoomStatusScreen.js
│   │   ├── ReservationScreen.js
│   │   ├── ApprovalScreen.js
│   │   └── ProfileScreen.js
│   ├── firebase/            # Firebase configuration
│   │   └── firebaseConfig.js
│   ├── models/              # 3D models and viewers
│   │   └── Viewer3D.js
│   ├── styles/              # CSS files
│   │   └── main.css
│   ├── assets/              # Images, fonts, etc.
│   ├── utils/               # Utility functions
│   │   └── themeManager.js
│   └── data/                # Sample data
│       └── rooms.json
├── .gitignore
├── README.md
└── package.json (optional)
```

## 🚀 Getting Started

### Prerequisites
- Modern web browser (Chrome, Firefox, Safari, Edge)
- Firebase account with Firestore enabled
- STI O365 account (for integration)

### Installation

1. **Clone or Download** the project
   ```bash
   git clone https://github.com/yourusername/RoomFinder.git
   cd RoomFinder
   ```

2. **Configure Firebase**
   - Update Firebase credentials in `src/firebase/firebaseConfig.js`
   - Ensure Firestore database is created
   - Enable Authentication (Email/Password, Google, O365)

3. **Setup Database Collections**
   - Create collections: `users`, `rooms`, `reservations`, `schedules`, `notifications`
   - Import sample data from `src/data/rooms.json`

4. **Launch Application**
   - Option A: Use Live Server VS Code extension
   - Option B: Deploy to Firebase Hosting
   - Option C: Run on local development server

### Firebase Setup

1. Create a Firestore database
2. Enable authentication methods:
   - Email/Password
   - Google Sign-In
   - O365 (Microsoft)
3. Set up security rules for data access
4. Create collections with proper indexes

## 🔐 Security Features

- User authentication required
- Role-based access control (RBAC)
- Firestore security rules
- Data validation on client and server
- Secure token management

## 📱 Responsive Design

- **Desktop** - Full feature set
- **Tablet** - Optimized layout
- **Mobile** - Touch-friendly interface
- **Minimum Width** - 320px support

## 🌓 Theme Support

- **Dark Mode** - Default theme
- **Light Mode** - Alternative theme
- **System Preference** - Auto-detect
- **User Control** - Manual toggle

## 📊 Real-time Features

- Live room status updates
- Instant reservation feedback
- Real-time notifications
- Live approval processing
- Concurrent user support

## 🔔 Notification System

- Reservation approved/rejected
- Room status changes
- Booking reminders
- System announcements
- Email notifications (optional)

## 🎓 Key Concepts

### Room Status Flow
1. **Available** → Student reserves
2. **Reserved** → Pending approval
3. **Approved** → Becomes "Occupied"
4. **Occupied** → Class in session
5. **Available** → Class ends

### Reservation Workflow
1. Student selects room and time
2. Submits reservation request
3. System checks availability
4. Faculty/Admin reviews
5. Approval or rejection notification
6. Status updates automatically

## 📈 Future Enhancements

- Bulk room operations
- Advanced analytics dashboard
- Calendar integration (Google Calendar, Outlook)
- Email reminders
- SMS notifications
- Room equipment management
- Building capacity planning
- Usage analytics and reports
- AI-powered room recommendations

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## 📄 License

This project is licensed under the MIT License - see LICENSE file for details.

## 📞 Support

For issues, questions, or suggestions:
- Create an issue on GitHub
- Contact the development team
- Email: support@roomfinder.sti.edu

## 🎉 Acknowledgments

- STI (Sistemas Tecnológicos Integrados)
- Three.js team for 3D graphics library
- Firebase team for backend services
- Font Awesome for icons

## 📝 Version History

### v1.0.0 (Current)
- Initial release
- Core features implemented
- 3D building viewer
- Real-time updates
- Reservation system
- Approval workflow

---

**STI RoomFinder** © 2026 - Making classroom finding easier, one click at a time! 🏫
