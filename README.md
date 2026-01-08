🎯 CodeBid - Competitive Coding Auction Platform
A real-time competitive coding auction platform where teams bid on coding problems and compete to solve them. Built with React, Node.js, Express, PostgreSQL, and Socket.IO for real-time updates.

🌟 Features
For Students/Teams:
✅ Team Registration - Quick signup with team name
✅ Real-time Bidding - Bid on coding problems in live auctions
✅ Live Updates - See highest bids and competing teams instantly
✅ Coin System - Start with 1,000 coins, earn more by winning
✅ Problem Solving - Solve LeetCode-style coding problems
✅ Leaderboard - Track rankings and scores
For Admins:
✅ Problem Management - Add/edit/delete coding problems
✅ Event Control - Start auctions and coding phases
✅ Team Monitoring - View all registered teams and their coins
✅ Real-time Dashboard - Monitor auction progress
Technical Features:
✅ Real-time Communication - WebSocket with Socket.IO
✅ JWT Authentication - Secure token-based auth
✅ PostgreSQL Database - Persistent data storage
✅ Responsive UI - Works on desktop and mobile
✅ In-Memory Fallback - Works without database if needed
🚀 Quick Start
Prerequisites:
Node.js (v16+)
PostgreSQL (v12+)
npm or yarn
Installation:
Clone the repository:
git clone https://github.com/YOUR_USERNAME/codebid.git
cd codebid-1
Install dependencies:
# Frontend
npm install

# Backend
cd backend
npm install
cd ..
Setup PostgreSQL:
# Start PostgreSQL service
net start postgresql-x64-17  # Windows
# or
brew services start postgresql  # macOS

# Create database
psql -U postgres -c "CREATE DATABASE codebid;"

# Run migrations
cd backend
npm run db:migrate
cd ..
Configure environment variables:
Frontend (.env):

VITE_API_BASE=http://localhost:4000
VITE_WS_BASE=http://localhost:4000
Backend (backend/.env):

PORT=4000
FRONTEND_ORIGIN=http://localhost:5173
JWT_SECRET=your-secret-key-change-in-production
DB_HOST=localhost
DB_PORT=5432
DB_NAME=codebid
DB_USER=postgres
DB_PASSWORD=postgres
Start the servers:
Terminal 1 - Backend:

cd backend
npm run dev
Terminal 2 - Frontend:

npm run dev
Open in browser:
http://localhost:5173
📖 Usage
For Students:
Register:

Go to http://localhost:5173
Click "Student"
Enter your team name
Click "REGISTER & JOIN AUCTION"
Participate in Auction:

Wait for admin to start auction
See the current problem and highest bid
Place your bid (must be higher than current highest)
Win the problem if you have the highest bid
Solve Problem:

After auction ends, coding phase begins
Solve the problem within time limit
Submit your solution
For Admin:
Login:

Go to http://localhost:5173
Click "Admin"
Password: code@bid123
Manage Problems:

Click "📝 MANAGE PROBLEMS"
Add new problems with:
Title (e.g., "Two Sum")
Difficulty (Easy/Medium/Hard)
Description
Test cases (JSON format)
Solution (optional)
Run Auction:

Click "START EVENT (AUCTION)"
Teams will see the problem and start bidding
Monitor bids in real-time
Click "START CODING PHASE" when auction ends
🏗️ Project Structure
codebid-1/
├── frontend/
│   ├── src/
│   │   ├── views/           # Page components
│   │   ├── components/      # Reusable components
│   │   ├── context/         # React context (state management)
│   │   ├── api.js           # API client
│   │   └── socket.js        # WebSocket client
│   ├── package.json
│   └── vite.config.js
│
├── backend/
│   ├── src/
│   │   ├── routes/          # API endpoints
│   │   ├── db/              # Database models
│   │   ├── socket/          # WebSocket handlers
│   │   ├── app.js           # Express app
│   │   └── index.js         # Server entry point
│   ├── sql/                 # Database migrations
│   ├── package.json
│   └── .env
│
└── README.md
🗄️ Database Schema
Teams Table:
- id (Primary Key)
- name (Unique)
- coins (Default: 1000)
- is_admin (Boolean)
- full_name, registration_number, branch, email, phone, year_of_study
- created_at, updated_at
Problems Table:
- id (Primary Key)
- title
- description
- difficulty (easy/medium/hard)
- test_cases (JSON)
- solution
- created_at
Events Table:
- id (Primary Key)
- state (WAITING/AUCTION/CODING/COMPLETED)
- current_problem_id (Foreign Key)
- highest_bid
- highest_bidder_id (Foreign Key)
- auction_start_time, coding_start_time, coding_end_time
- created_at, updated_at
Bids Table:
- id (Primary Key)
- event_id (Foreign Key)
- team_id (Foreign Key)
- amount
- created_at
🔌 API Endpoints
Authentication:
POST /auth/login - Register/login team
POST /auth/signup - Detailed signup with info
GET /auth/me - Get current team info
Events:
GET /event/state - Get current auction state
GET /event/problems - Get all problems
Admin:
POST /admin/start-auction - Start auction
POST /admin/start-coding - Start coding phase
GET /admin/teams - View all teams
GET /admin/problems - View all problems
POST /admin/problems - Add new problem
DELETE /admin/problems/:id - Delete problem
GET /admin/leaderboard - Get top teams
WebSocket Events:
JOIN_AUCTION - Join auction room
PLACE_BID - Place a bid
BID_UPDATED - Broadcast bid update
STATE_CHANGED - Broadcast state change
🛠️ Available Scripts
Frontend:
npm run dev      # Start development server
npm run build    # Build for production
npm run preview  # Preview production build
npm run lint     # Run ESLint
Backend:
npm run dev           # Start with auto-reload
npm run start         # Start production server
npm run db:migrate    # Run database migrations
npm run db:test       # Test database connection
📊 View Database
Using psql:
# Connect to database
psql -U postgres -h localhost -d codebid

# View teams
SELECT * FROM teams;

# View bids
SELECT * FROM bids;

# View problems
SELECT * FROM problems;

# View events
SELECT * FROM events;
Using pgAdmin:
Open pgAdmin
Servers → PostgreSQL → Databases → codebid → Tables
Right-click table → View/Edit Data
🚀 Deployment
Frontend (Vercel):
Push code to GitHub
Go to vercel.com
Import repository
Set build command: npm run build
Set output: dist
Deploy
Backend (Railway):
Go to railway.app
Create new project from GitHub
Add PostgreSQL database
Set environment variables
Deploy
Database (Railway PostgreSQL):
Add PostgreSQL plugin in Railway
Get connection string
Update backend .env
🔐 Security Notes
Change JWT_SECRET in production
Use HTTPS in production
Set FRONTEND_ORIGIN to your actual domain
Never commit .env files with real credentials
Use strong database passwords
🐛 Troubleshooting
"Failed to fetch" error:
Check if backend is running on port 4000
Check if frontend proxy is configured correctly
Check browser console for errors (F12)
PostgreSQL connection failed:
Make sure PostgreSQL service is running
Check database credentials in .env
Run npm run db:test to test connection
Port already in use:
Frontend: Change port in vite.config.js
Backend: Change PORT in .env
WebSocket connection failed:
Check if backend is running
Check CORS settings in backend/src/app.js
Check browser console for errors
📝 Sample Data
Default Admin:
Username: admin
Password: code@bid123 (for admin dashboard)
Coins: 10,000
Sample Problems:
Two Sum (Easy)
Reverse String (Easy)
Valid Parentheses (Medium)
🤝 Contributing
Fork the repository
Create a feature branch (git checkout -b feature/amazing-feature)
Commit changes (git commit -m 'Add amazing feature')
Push to branch (git push origin feature/amazing-feature)
Open a Pull Request
📄 License
This project is licensed under the MIT License - see LICENSE file for details.

👨‍💻 Author
Created as a competitive coding auction platform for educational purposes.

📞 Support
For issues and questions:

Check the troubleshooting section
Open an issue on GitHub
Check existing issues for solutions
🎓 Learning Resources
React Documentation
Node.js Documentation
PostgreSQL Documentation
Socket.IO Documentation
Express.js Guide
