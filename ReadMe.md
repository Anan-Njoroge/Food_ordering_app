A simple food ordering app:
 Folder structure

 food-app/
│
├── assets/                # Client-side static files
│   ├── css/
│   │   └── style.css      # Custom styling for all pages
│   ├── js/
│   │   ├── auth.js        # JS for Login/Signup validation & AJAX
│   │   └── app.js         # JS for Add to Cart & Placing Orders
│   └── img/               # Food thumbnails (pizza.jpg, burger.png)
│
├── config/                
│   └── db.php             # Database connection (mysqli)
│
├── includes/              # Reusable UI components
│   ├── header.php         # Navbar (Home, Menu, My Orders, Logout)
│   └── footer.php         # Copyright & Script tags
│
├── actions/               # Pure PHP Logic (The "Engine")
│   ├── signup_process.php # Handles creating new accounts
│   ├── login_process.php  # Handles authentication & Sessions
│   └── place_order.php    # Handles inserting orders into DB
│
├── index.php              # Home Page (The "Home Feed" with new/featured food)
├── menu.php               # Full Menu Page (Browse all items)
├── orders.php             # User's Personal Order History
├── login.php              # Login Screen
└── signup.php             # Account Creation Screen

<!-- Paul Mutavuta -->
1. The Project Architecture
We are building a Mobile-First food ordering app. The frontend uses Vanilla JavaScript (AJAX/Fetch) to communicate with the backend. To keep our work clean, we are using the following folder structure:

Plaintext
food-app/
│
├── assets/                # Client-side static files (Frontend)
│   ├── css/
│   │   └── style.css      # Shared styling
│   └── js/
│       ├── auth.js        # Logic for Login/Signup AJAX
│       └── app.js         # Logic for Menu/Orders AJAX
│
├── config/                
│   └── db.php             # MySQLi Connection Configuration
│
├── includes/              # UI Templates (Shared)
│   ├── header.php         # Top nav and meta tags
│   └── footer.php         # Bottom nav and script tags
│
├── actions/               # Backend Logic (Your Domain)
│   ├── signup_process.php # CREATE user
│   ├── login_process.php  # AUTH user & Start Session
│   └── place_order.php    # CREATE order entry
│
├── index.php              # Home Feed (Dynamic)
├── menu.php               # Full Menu (Dynamic)
├── orders.php             # Order History (Dynamic)
├── login.php              # Login UI
└── signup.php             # Registration UI
2. Database Schema (MySQL)
Please initialize the database with these three core tables. Use Prepared Statements for all queries to prevent SQL injection.

users: id (INT), name (VARCHAR), email (UNIQUE), password (HASHED), created_at (TIMESTAMP).

menu: id, name, description, price, image_url, category, created_at.

orders: id, user_id, total_price, status (pending/delivered), created_at.

3. Implementation Rules
🔑 Authentication
Sign-Up: Hash passwords using password_hash($pass, PASSWORD_DEFAULT).

Login: Use password_verify() and start a session.

Session Keys: Store $_SESSION['user_id'] and $_SESSION['user_name'] upon successful login.

📡 Data Exchange (JSON)
Since I am using AJAX for the frontend, the files in your actions/ folder must return JSON responses instead of redirecting with header().

Success Example: echo json_encode(['success' => true, 'user' => $name]);

Error Example: echo json_encode(['success' => false, 'message' => 'Invalid email']);

4. Immediate Tasks
Set up config/db.php so I can start testing database pings.

Code actions/signup_process.php: I have built the form with input names name, email, and password.

Create database.sql: Share the SQL dump once the tables are ready so I can import it locally.