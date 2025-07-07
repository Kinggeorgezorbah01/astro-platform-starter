# Astro on Netlify Platform Starter

[Live Demo](https://fafnet.online.netlify.app/)

A modern starter based on Astro.js, Tailwind, and [Netlify Core Primitives](https://docs.netlify.com/core/overview/#develop) (Edge Functions, Image CDN, Blob Store).

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Faith & Fellowship - Christian Community Platform</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Georgia', serif;
            line-height: 1.6;
            color: #333;
            background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
            min-height: 100vh;
        }

        /* Header Styles */
        .header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 2rem 0;
            text-align: center;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }

        .header h1 {
            font-size: 2.5rem;
            margin-bottom: 0.5rem;
            font-weight: 300;
        }

        .header p {
            font-size: 1.1rem;
            opacity: 0.9;
            max-width: 600px;
            margin: 0 auto;
            padding: 0 1rem;
        }

        /* Authentication Styles */
        .auth-container {
            max-width: 400px;
            margin: 4rem auto;
            padding: 2rem;
            background: white;
            border-radius: 15px;
            box-shadow: 0 8px 25px rgba(0,0,0,0.1);
        }

        .auth-container h2 {
            color: #667eea;
            text-align: center;
            margin-bottom: 2rem;
            font-size: 1.8rem;
        }

        .auth-form {
            margin-bottom: 2rem;
        }

        .form-group {
            margin-bottom: 1.5rem;
        }

        .form-group label {
            display: block;
            margin-bottom: 0.5rem;
            color: #555;
            font-weight: 600;
        }

        .form-group input {
            width: 100%;
            padding: 0.8rem;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            font-size: 1rem;
            transition: border-color 0.3s ease;
        }

        .form-group input:focus {
            outline: none;
            border-color: #667eea;
        }

        .auth-btn {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            padding: 1rem 2rem;
            border-radius: 25px;
            cursor: pointer;
            font-size: 1.1rem;
            transition: all 0.3s ease;
            width: 100%;
            margin-bottom: 1rem;
        }

        .auth-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 15px rgba(0,0,0,0.2);
        }

        .social-auth {
            margin-top: 2rem;
        }

        .social-auth h3 {
            text-align: center;
            color: #666;
            margin-bottom: 1rem;
            font-size: 1.1rem;
        }

        .social-btn {
            display: flex;
            align-items: center;
            justify-content: center;
            width: 100%;
            padding: 0.8rem;
            margin-bottom: 0.5rem;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            background: white;
            cursor: pointer;
            transition: all 0.3s ease;
            text-decoration: none;
            color: #333;
            font-size: 1rem;
        }

        .social-btn:hover {
            border-color: #667eea;
            transform: translateY(-2px);
        }

        .social-btn img {
            width: 20px;
            height: 20px;
            margin-right: 0.5rem;
        }

        .auth-switch {
            text-align: center;
            margin-top: 1rem;
        }

        .auth-switch a {
            color: #667eea;
            text-decoration: none;
            font-weight: 600;
        }

        .auth-switch a:hover {
            text-decoration: underline;
        }

        /* User Profile Header */
        .user-header {
            background: rgba(255,255,255,0.95);
            padding: 1rem 0;
            text-align: center;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
            display: none;
        }

        .user-info {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 1rem;
            margin-bottom: 1rem;
        }

        .user-avatar {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: #667eea;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: bold;
        }

        .welcome-message {
            color: #667eea;
            font-weight: 600;
        }

        .logout-btn {
            background: #f44336;
            color: white;
            border: none;
            padding: 0.5rem 1rem;
            border-radius: 20px;
            cursor: pointer;
            font-size: 0.9rem;
            transition: all 0.3s ease;
        }

        .logout-btn:hover {
            background: #d32f2f;
            transform: translateY(-1px);
        }

        /* Navigation */
        .nav {
            background: rgba(255,255,255,0.95);
            padding: 1rem 0;
            text-align: center;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
            position: sticky;
            top: 0;
            z-index: 100;
            display: none;
        }

        .nav-buttons {
            display: flex;
            justify-content: center;
            gap: 1rem;
            flex-wrap: wrap;
        }

        .nav-btn {
            background: #667eea;
            color: white;
            border: none;
            padding: 0.7rem 1.5rem;
            border-radius: 25px;
            cursor: pointer;
            font-size: 1rem;
            transition: all 0.3s ease;
        }

        .nav-btn:hover {
            background: #764ba2;
            transform: translateY(-2px);
        }

        .nav-btn.active {
            background: #764ba2;
            box-shadow: 0 4px 8px rgba(0,0,0,0.2);
        }

        /* Main Container */
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 2rem;
            display: none;
        }

        /* Section Styles */
        .section {
            display: none;
            animation: fadeIn 0.5s ease-in;
        }

        .section.active {
            display: block;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* Welcome Section */
        .welcome {
            background: white;
            padding: 3rem;
            border-radius: 15px;
            box-shadow: 0 8px 25px rgba(0,0,0,0.1);
            text-align: center;
            margin-bottom: 2rem;
        }

        .welcome h2 {
            color: #667eea;
            font-size: 2.2rem;
            margin-bottom: 1rem;
        }

        .welcome p {
            font-size: 1.1rem;
            color: #666;
            line-height: 1.8;
            max-width: 800px;
            margin: 0 auto;
        }

        /* Prayer Request Form */
        .prayer-form {
            background: white;
            padding: 2rem;
            border-radius: 15px;
            box-shadow: 0 8px 25px rgba(0,0,0,0.1);
            margin-bottom: 2rem;
        }

        .prayer-form h3 {
            color: #667eea;
            font-size: 1.8rem;
            margin-bottom: 1.5rem;
            text-align: center;
        }

        .prayer-form .form-group label {
            display: block;
            margin-bottom: 0.5rem;
            color: #555;
            font-weight: 600;
        }

        .prayer-form .form-group input,
        .prayer-form .form-group textarea,
        .prayer-form .form-group select {
            width: 100%;
            padding: 0.8rem;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            font-size: 1rem;
            transition: border-color 0.3s ease;
        }

        .prayer-form .form-group input:focus,
        .prayer-form .form-group textarea:focus,
        .prayer-form .form-group select:focus {
            outline: none;
            border-color: #667eea;
        }

        .prayer-form .form-group textarea {
            resize: vertical;
            min-height: 120px;
        }

        .submit-btn {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            padding: 1rem 2rem;
            border-radius: 25px;
            cursor: pointer;
            font-size: 1.1rem;
            transition: all 0.3s ease;
            width: 100%;
        }

        .submit-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 15px rgba(0,0,0,0.2);
        }

        /* Prayer Cards */
        .prayer-cards {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
            gap: 1.5rem;
            margin-top: 2rem;
        }

        .prayer-card {
            background: white;
            padding: 1.5rem;
            border-radius: 15px;
            box-shadow: 0 6px 20px rgba(0,0,0,0.1);
            transition: transform 0.3s ease;
        }

        .prayer-card:hover {
            transform: translateY(-5px);
        }

        .prayer-card h4 {
            color: #667eea;
            font-size: 1.3rem;
            margin-bottom: 0.5rem;
        }

        .prayer-meta {
            color: #888;
            font-size: 0.9rem;
            margin-bottom: 1rem;
        }

        .prayer-content {
            color: #555;
            line-height: 1.6;
            margin-bottom: 1rem;
        }

        .prayer-actions {
            display: flex;
            gap: 0.5rem;
            flex-wrap: wrap;
            margin-top: 1rem;
        }

        .prayer-action {
            background: #f0f0f0;
            border: none;
            padding: 0.5rem 1rem;
            border-radius: 20px;
            cursor: pointer;
            font-size: 0.9rem;
            transition: all 0.3s ease;
        }

        .prayer-action:hover {
            background: #667eea;
            color: white;
        }

        .prayer-action.praying {
            background: #667eea;
            color: white;
        }

        /* Response Section */
        .responses {
            margin-top: 1rem;
            padding-top: 1rem;
            border-top: 1px solid #e0e0e0;
        }

        .response {
            background: #f9f9f9;
            padding: 1rem;
            border-radius: 8px;
            margin-bottom: 0.5rem;
        }

        .response-author {
            font-weight: 600;
            color: #667eea;
            margin-bottom: 0.5rem;
        }

        .response-content {
            color: #555;
            line-height: 1.5;
        }

        /* Categories */
        .categories {
            display: flex;
            gap: 1rem;
            margin-bottom: 2rem;
            flex-wrap: wrap;
            justify-content: center;
        }

        .category-btn {
            background: white;
            border: 2px solid #667eea;
            color: #667eea;
            padding: 0.5rem 1rem;
            border-radius: 20px;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .category-btn:hover,
        .category-btn.active {
            background: #667eea;
            color: white;
        }

        /* Registration Success Message */
        .success-message {
            background: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
            padding: 1rem;
            border-radius: 8px;
            margin-bottom: 1rem;
            text-align: center;
        }

        .error-message {
            background: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
            padding: 1rem;
            border-radius: 8px;
            margin-bottom: 1rem;
            text-align: center;
        }

        /* Responsive Design */
        @media (max-width: 768px) {
            .container {
                padding: 1rem;
            }
            
            .header h1 {
                font-size: 2rem;
            }
            
            .nav-buttons {
                flex-direction: column;
                align-items: center;
            }
            
            .prayer-cards {
                grid-template-columns: 1fr;
            }

            .auth-container {
                margin: 2rem auto;
                padding: 1.5rem;
            }
        }
    </style>
</head>
<body>
    <!-- Header Section -->
    <header class="header">
        <h1>Faith & Fellowship</h1>
        <p>A sacred space for Christian community, where testimonies strengthen faith and prayers unite hearts in God's love</p>
    </header>

    <!-- Authentication Section -->
    <div id="authSection" class="auth-container">
        <!-- Login Form -->
        <div id="loginForm" class="auth-form">
            <h2>Welcome Back to Faith & Fellowship</h2>
            <p style="text-align: center; color: #666; margin-bottom: 2rem;">Sign in to continue your spiritual journey with our community</p>
            
            <form id="loginFormElement">
                <div class="form-group">
                    <label for="loginEmail">Email Address:</label>
                    <input type="email" id="loginEmail" name="email" required>
                </div>
                
                <div class="form-group">
                    <label for="loginPassword">Password:</label>
                    <input type="password" id="loginPassword" name="password" required>
                </div>
                
                <button type="submit" class="auth-btn">Sign In</button>
            </form>

            <div class="social-auth">
                <h3>Or continue with:</h3>
                <button class="social-btn" onclick="socialLogin('google')">
                    <span>🔍</span> Continue with Google
                </button>
                <button class="social-btn" onclick="socialLogin('facebook')">
                    <span>📘</span> Continue with Facebook
                </button>
                <button class="social-btn" onclick="socialLogin('twitter')">
                    <span>🐦</span> Continue with Twitter
                </button>
                <button class="social-btn" onclick="socialLogin('yahoo')">
                    <span>📧</span> Continue with Yahoo
                </button>
            </div>

            <div class="auth-switch">
                <p>New to our community? <a href="#" onclick="showRegisterForm()">Create an account</a></p>
            </div>
        </div>

        <!-- Registration Form -->
        <div id="registerForm" class="auth-form" style="display: none;">
            <h2>Join Our Christian Community</h2>
            <p style="text-align: center; color: #666; margin-bottom: 2rem;">Create your account to begin sharing in prayer and fellowship</p>
            
            <form id="registerFormElement">
                <div class="form-group">
                    <label for="registerName">Full Name:</label>
                    <input type="text" id="registerName" name="name" required>
                </div>
                
                <div class="form-group">
                    <label for="registerEmail">Email Address:</label>
                    <input type="email" id="registerEmail" name="email" required>
                </div>
                
                <div class="form-group">
                    <label for="registerPassword">Password:</label>
                    <input type="password" id="registerPassword" name="password" minlength="8" required>
                </div>
                
                <div class="form-group">
                    <label for="confirmPassword">Confirm Password:</label>
                    <input type="password" id="confirmPassword" name="confirmPassword" required>
                </div>
                
                <div class="form-group">
                    <label for="churchName">Church/Community (Optional):</label>
                    <input type="text" id="churchName" name="church" placeholder="Share your home church if you'd like">
                </div>
                
                <button type="submit" class="auth-btn">Create Account</button>
            </form>

            <div class="social-auth">
                <h3>Or sign up with:</h3>
                <button class="social-btn" onclick="socialLogin('google')">
                    <span>🔍</span> Sign up with Google
                </button>
                <button class="social-btn" onclick="socialLogin('facebook')">
                    <span>📘</span> Sign up with Facebook
                </button>
                <button class="social-btn" onclick="socialLogin('twitter')">
                    <span>🐦</span> Sign up with Twitter
                </button>
                <button class="social-btn" onclick="socialLogin('yahoo')">
                    <span>📧</span> Sign up with Yahoo
                </button>
            </div>

            <div class="auth-switch">
                <p>Already have an account? <a href="#" onclick="showLoginForm()">Sign in here</a></p>
            </div>
        </div>
    </div>

    <!-- User Profile Header (shown when logged in) -->
    <div id="userHeader" class="user-header">
        <div class="user-info">
            <div class="user-avatar" id="userAvatar"></div>
            <div class="welcome-message" id="welcomeMessage"></div>
            <button class="logout-btn" onclick="logout()">Logout</button>
        </div>
    </div>

    <!-- Navigation (shown when logged in) -->
    <nav id="mainNav" class="nav">
        <div class="nav-buttons">
            <button class="nav-btn active" onclick="showSection('home')">Home</button>
            <button class="nav-btn" onclick="showSection('share')">Share Request</button>
            <button class="nav-btn" onclick="showSection('testimonies')">Testimonies</button>
            <button class="nav-btn" onclick="showSection('prayers')">Prayer Wall</button>
            <button class="nav-btn" onclick="showSection('profile')">My Profile</button>
        </div>
    </nav>

    <!-- Main Content Container (shown when logged in) -->
    <div id="mainContainer" class="container">
        <!-- Home Section -->
        <div id="home" class="section active">
            <div class="welcome">
                <h2>Welcome to Our Community of Faith</h2>
                <p>In the spirit of bearing one another's burdens and sharing in each other's joys, this platform serves as a digital gathering place where believers can share their prayer requests, celebrate God's faithfulness through testimonies, and support one another in genuine Christian fellowship. Here, your struggles become our prayers, your victories become our celebrations, and together we witness God's amazing work in our daily lives.</p>
            </div>

            <div class="categories">
                <button class="category-btn active" onclick="filterPrayers('all')">All Requests</button>
                <button class="category-btn" onclick="filterPrayers('health')">Health & Healing</button>
                <button class="category-btn" onclick="filterPrayers('family')">Family & Relationships</button>
                <button class="category-btn" onclick="filterPrayers('work')">Work & Provision</button>
                <button class="category-btn" onclick="filterPrayers('spiritual')">Spiritual Growth</button>
                <button class="category-btn" onclick="filterPrayers('praise')">Praise Reports</button>
            </div>

            <div class="prayer-cards" id="prayerCards">
                <!-- Prayer requests will be populated here -->
            </div>
        </div>

        <!-- Share Prayer Request Section -->
        <div id="share" class="section">
            <div class="prayer-form">
                <h3>Share Your Prayer Request</h3>
                <form id="prayerForm">
                    <div class="form-group">
                        <label for="category">Category:</label>
                        <select id="category" name="category" required>
                            <option value="">Select a category</option>
                            <option value="health">Health & Healing</option>
                            <option value="family">Family & Relationships</option>
                            <option value="work">Work & Provision</option>
                            <option value="spiritual">Spiritual Growth</option>
                            <option value="praise">Praise Report</option>
                            <option value="other">Other</option>
                        </select>
                    </div>
                    
                    <div class="form-group">
                        <label for="title">Prayer Request Title:</label>
                        <input type="text" id="title" name="title" placeholder="Brief title for your request" required>
                    </div>
                    
                    <div class="form-group">
                        <label for="description">Share Your Request:</label>
                        <textarea id="description" name="description" placeholder="Share your heart with our community. How can we pray for you today?" required></textarea>
                    </div>
                    
                    <button type="submit" class="submit-btn">Share Prayer Request</button>
                </form>
            </div>
        </div>

        <!-- Testimonies Section -->
        <div id="testimonies" class="section">
            <div class="welcome">
                <h2>Testimonies of God's Faithfulness</h2>
                <p>Celebrate with us as we share stories of how God has moved in our lives, answered our prayers, and demonstrated His love and power in amazing ways.</p>
            </div>
            <div class="prayer-cards" id="testimonyCards">
                <!-- Testimonies will be populated here -->
            </div>
        </div>

        <!-- Prayer Wall Section -->
        <div id="prayers" class="section">
            <div class="welcome">
                <h2>Community Prayer Wall</h2>
                <p>Join us in lifting up these requests to our heavenly Father. Your prayers make a difference in the lives of your brothers and sisters in Christ.</p>
            </div>
            <div class="prayer-cards" id="prayerWall">
                <!-- All prayers will be displayed here -->
            </div>
        </div>

        <!-- Profile Section -->
        <div id="profile" class="section">
            <div class="welcome">
                <h2>My Profile</h2>
                <p>Manage your account settings and view your prayer history within our community.</p>
            </div>
            <div class="prayer-form">
                <h3>Account Information</h3>
                <div id="profileInfo">
                    <!-- Profile information will be populated here -->
                </div>
            </div>
        </div>
    </div>

    <script>
        // Authentication and user management system
        let currentUser = null;
        let users = []; // In a real application, this would be managed by a backend database
        let prayerRequests = [];
        let userPrayers = {}; // Track which prayers user has committed to
        let currentFilter = 'all';

        // Check if user is already logged in when page loads
        document.addEventListener('DOMContentLoaded', function() {
            const savedUser = localStorage.getItem('currentUser');
            if (savedUser) {
                currentUser = JSON.parse(savedUser);
                showMainApplication();
            }
        });

        // Handle login form submission
        document.getElementById('loginFormElement').addEventListener('submit', function(e) {
            e.preventDefault();
            const formData = new FormData(e.target);
            const email = formData.get('email');
            const password = formData.get('password');
            
            // In a real application, this would verify credentials with a backend server
            const user = users.find(u => u.email === email && u.password === password);
            
            if (user) {
                currentUser = user;
                localStorage.setItem('currentUser', JSON.stringify(user));
                showMainApplication();
                showMessage('Welcome back! You have successfully signed in.', 'success');
            } else {
                showMessage('Invalid email or password. Please try again.', 'error');
            }
        });

        // Handle registration form submission
        document.getElementById('registerFormElement').addEventListener('submit', function(e) {
            e.preventDefault();
            const formData = new FormData(e.target);
            const name = formData.get('name');
            const email = formData.get('email');
            const password = formData.get('password');
            const confirmPassword = formData.get('confirmPassword');
            const church = formData.get('church');
            
            // Validate form data
            if (password !== confirmPassword) {
                showMessage('Passwords do not match. Please try again.', 'error');
                return;
            }
            
            // Check if email already exists
            if (users.find(u => u.email === email)) {
                showMessage('An account with this email already exists. Please sign in instead.', 'error');
                return;
            }
            
            // Create new user account
            const newUser = {
                id: Date.now(),
                name: name,
                email: email,
                password: password, // In a real application, this would be hashed
                church: church,
                joinDate: new Date(),
                avatar: name.charAt(0).toUpperCase() // Use first letter of name as avatar
            };
            
            users.push(newUser);
            currentUser = newUser;
            localStorage.setItem('currentUser', JSON.stringify(newUser));
            
            showMainApplication();
            showMessage('Welcome to Faith & Fellowship! Your account has been created successfully.', 'success');
            initializeApp();
        });

        // Show registration form
        function showRegisterForm() {
            document.getElementById('loginForm').style.display = 'none';
            document.getElementById('registerForm').style.display = 'block';
        }

        // Show login form
        function showLoginForm() {
            document.getElementById('registerForm').style.display = 'none';
            document.getElementById('loginForm').style.display = 'block';
        }

        // Handle social media login (simulated)
        function socialLogin(provider) {
            // In a real application, this would integrate with OAuth providers
            const mockUser = {
                id: Date.now(),
                name: `${provider.charAt(0).toUpperCase() + provider.slice(1)} User`,
                email: `user@${provider}.com`,
                provider: provider,
                joinDate: new Date(),
                avatar: provider.charAt(0).toUpperCase()
            };
            
            currentUser = mockUser;
            localStorage.setItem('currentUser', JSON.stringify(mockUser));
            showMainApplication();
            showMessage(`Welcome! You have successfully signed in with ${provider.charAt(0).toUpperCase() + provider.slice(1)}.`, 'success');
            initializeApp();
        }

        // Show main application after successful authentication
        function showMainApplication() {
            document.getElementById('authSection').style.display = 'none';
            document.getElementById('userHeader').style.display = 'block';
            document.getElementById('mainNav').style.display = 'block';
            document.getElementById('mainContainer').style.display = 'block';
            
            // Update user interface with current user information
            document.getElementById('userAvatar').textContent = currentUser.avatar || currentUser.name.charAt(0).toUpperCase();
            document.getElementById('welcomeMessage').textContent = `Welcome, ${currentUser.name}!`;
            
            // Load user-specific data
            loadUserData();
        }

        // Load user-specific data and preferences
        function loadUserData() {
            // In a real application, this would load user's prayer history, preferences, etc.
            const userKey = `user_${currentUser.id}`;
            const userData = localStorage.getItem(userKey);
            
            if (userData) {
                const parsedData = JSON.parse(userData);
                userPrayers = parsedData.prayers || {};
            }
        }

        // Save user data to local storage
        function saveUserData() {
            const userKey = `user_${currentUser.id}`;
            const userData = {
                prayers: userPrayers,
                lastLogin: new Date()
            };
            localStorage.setItem(userKey, JSON.stringify(userData));
        }

        // Logout function
