<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SecureVault - Login</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(-45deg, #667eea, #764ba2, #f093fb, #f5576c, #4facfe, #00f2fe);
            background-size: 400% 400%;
            animation: gradientShift 15s ease infinite;
            min-height: 100vh;
            overflow-x: hidden;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        @keyframes gradientShift {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        .floating-shapes {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 1;
        }

        .shape {
            position: absolute;
            opacity: 0.15;
            animation: float 25s infinite linear;
        }

        .shape:nth-child(1) {
            top: 10%;
            left: 15%;
            width: 120px;
            height: 120px;
            background: linear-gradient(45deg, #ff6b6b, #4ecdc4);
            border-radius: 50%;
            animation-delay: 0s;
        }

        .shape:nth-child(2) {
            top: 70%;
            left: 75%;
            width: 80px;
            height: 80px;
            background: linear-gradient(45deg, #45b7d1, #96ceb4);
            transform: rotate(45deg);
            animation-delay: -8s;
        }

        .shape:nth-child(3) {
            top: 40%;
            left: 5%;
            width: 100px;
            height: 100px;
            background: linear-gradient(45deg, #f9ca24, #f0932b);
            clip-path: polygon(50% 0%, 0% 100%, 100% 100%);
            animation-delay: -12s;
        }

        .shape:nth-child(4) {
            top: 20%;
            left: 80%;
            width: 90px;
            height: 90px;
            background: linear-gradient(45deg, #6c5ce7, #a29bfe);
            border-radius: 20px;
            animation-delay: -20s;
        }

        .shape:nth-child(5) {
            top: 60%;
            left: 25%;
            width: 70px;
            height: 70px;
            background: linear-gradient(45deg, #fd79a8, #fdcb6e);
            border-radius: 50%;
            animation-delay: -5s;
        }

        .shape:nth-child(6) {
            top: 85%;
            left: 60%;
            width: 110px;
            height: 110px;
            background: linear-gradient(45deg, #00b894, #00cec9);
            clip-path: polygon(25% 0%, 100% 0%, 75% 100%, 0% 100%);
            animation-delay: -15s;
        }

        @keyframes float {
            0% { 
                transform: translateY(0px) rotate(0deg) scale(1); 
                opacity: 0.1; 
            }
            25% { 
                transform: translateY(-30px) rotate(90deg) scale(1.1); 
                opacity: 0.15;
            }
            50% { 
                transform: translateY(-15px) rotate(180deg) scale(0.9); 
                opacity: 0.1;
            }
            75% { 
                transform: translateY(-45px) rotate(270deg) scale(1.2); 
                opacity: 0.2;
            }
            100% { 
                transform: translateY(0px) rotate(360deg) scale(1); 
                opacity: 0.1;
            }
        }

        .auth-container {
            position: relative;
            z-index: 10;
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(20px);
            border-radius: 25px;
            padding: 50px;
            box-shadow: 0 30px 60px rgba(0, 0, 0, 0.3);
            border: 1px solid rgba(255, 255, 255, 0.3);
            width: 100%;
            max-width: 450px;
            transform: translateY(0);
            transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .auth-container:hover {
            transform: translateY(-10px);
            box-shadow: 0 40px 80px rgba(0, 0, 0, 0.4);
        }

        .logo {
            text-align: center;
            margin-bottom: 40px;
        }

        .logo h1 {
            color: #667eea;
            font-size: 3rem;
            font-weight: 800;
            text-shadow: 0 4px 15px rgba(102, 126, 234, 0.4);
            animation: logoGlow 3s ease-in-out infinite alternate;
            letter-spacing: -1px;
        }

        @keyframes logoGlow {
            from { 
                transform: scale(1);
                filter: drop-shadow(0 0 10px rgba(102, 126, 234, 0.3));
            }
            to { 
                transform: scale(1.05);
                filter: drop-shadow(0 0 20px rgba(102, 126, 234, 0.6));
            }
        }

        .subtitle {
            text-align: center;
            color: #666;
            font-size: 1.1rem;
            margin-bottom: 30px;
            opacity: 0.8;
        }

        .form-group {
            margin-bottom: 25px;
            position: relative;
        }

        .form-group label {
            display: block;
            margin-bottom: 8px;
            color: #333;
            font-weight: 600;
            font-size: 0.95rem;
        }

        .form-group input {
            width: 100%;
            padding: 18px 25px;
            border: 2px solid #e1e8ed;
            border-radius: 15px;
            font-size: 1.1rem;
            transition: all 0.3s ease;
            background: rgba(255, 255, 255, 0.9);
            position: relative;
        }

        .form-group input:focus {
            outline: none;
            border-color: #667eea;
            box-shadow: 0 0 0 4px rgba(102, 126, 234, 0.15);
            transform: translateY(-3px);
            background: rgba(255, 255, 255, 1);
        }

        .form-group input::placeholder {
            color: #aaa;
            opacity: 0.7;
        }

        .auth-btn {
            width: 100%;
            padding: 18px;
            background: linear-gradient(135deg, #667eea, #764ba2, #f093fb);
            background-size: 200% 200%;
            color: white;
            border: none;
            border-radius: 15px;
            font-size: 1.2rem;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.4s ease;
            position: relative;
            overflow: hidden;
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-bottom: 20px;
            animation: gradientMove 3s ease infinite;
        }

        @keyframes gradientMove {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        .auth-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 15px 35px rgba(102, 126, 234, 0.5);
            animation-play-state: paused;
        }

        .auth-btn:active {
            transform: translateY(-1px);
        }

        .auth-btn::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.3), transparent);
            transition: left 0.6s;
        }

        .auth-btn:hover::before {
            left: 100%;
        }

        .toggle-section {
            text-align: center;
            margin-top: 25px;
        }

        .toggle-text {
            color: #666;
            margin-bottom: 10px;
        }

        .toggle-btn {
            background: linear-gradient(135deg, #f093fb, #f5576c);
            color: white;
            border: none;
            padding: 12px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-weight: 600;
            transition: all 0.3s ease;
            text-decoration: none;
            display: inline-block;
        }

        .toggle-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 20px rgba(245, 87, 108, 0.4);
        }

        .popup {
            position: fixed;
            top: 30px;
            right: 30px;
            background: linear-gradient(135deg, #4CAF50, #45a049);
            color: white;
            padding: 25px 35px;
            border-radius: 20px;
            box-shadow: 0 20px 40px rgba(76, 175, 80, 0.5);
            transform: translateX(500px);
            transition: all 0.6s cubic-bezier(0.68, -0.55, 0.265, 1.55);
            z-index: 1000;
            border: 2px solid rgba(255, 255, 255, 0.3);
            min-width: 300px;
        }

        .popup.show {
            transform: translateX(0);
            animation: popupBounce 0.8s ease;
        }

        .popup.error {
            background: linear-gradient(135deg, #f5576c, #f093fb);
        }

        @keyframes popupBounce {
            0%, 20%, 50%, 80%, 100% { transform: translateX(0); }
            40% { transform: translateX(-15px); }
            60% { transform: translateX(-8px); }
        }

        .popup h3 {
            margin: 0 0 8px 0;
            font-size: 1.3rem;
            font-weight: 700;
        }

        .popup p {
            margin: 0;
            opacity: 0.9;
            font-size: 1rem;
        }

        .sparkles {
            position: absolute;
            pointer-events: none;
        }

        @keyframes sparkle {
            0% {
                transform: scale(0) rotate(0deg);
                opacity: 1;
            }
            50% {
                transform: scale(1) rotate(180deg);
                opacity: 0.8;
            }
            100% {
                transform: scale(0) rotate(360deg);
                opacity: 0;
            }
        }

        .loading {
            opacity: 0.7;
            pointer-events: none;
        }

        .loading .auth-btn {
            background: #ccc;
            animation: none;
        }

        @media (max-width: 768px) {
            .auth-container {
                margin: 20px;
                padding: 30px;
            }
            
            .logo h1 {
                font-size: 2.5rem;
            }
        }
    </style>
</head>
<body>
    <div class="floating-shapes">
        <div class="shape"></div>
        <div class="shape"></div>
        <div class="shape"></div>
        <div class="shape"></div>
        <div class="shape"></div>
        <div class="shape"></div>
    </div>

    <div class="auth-container" id="authContainer">
        <div class="logo">
            <h1>SecureVault</h1>
        </div>
        <p class="subtitle">Secure File Storage with Rewards</p>
        
        <form id="authForm">
            <div class="form-group">
                <label for="email">Email Address</label>
                <input type="email" id="email" name="email" placeholder="Enter your email" required>
            </div>
            
            <div class="form-group">
                <label for="password">Password</label>
                <input type="password" id="password" name="password" placeholder="Enter your password" required>
            </div>
            
            <div class="form-group" id="confirmPasswordGroup" style="display: none;">
                <label for="confirmPassword">Confirm Password</label>
                <input type="password" id="confirmPassword" name="confirmPassword" placeholder="Confirm your password">
            </div>
            
            <button type="submit" class="auth-btn" id="authBtn">Sign In</button>
        </form>

        <div class="toggle-section">
            <p class="toggle-text" id="toggleText">Don't have an account?</p>
            <button type="button" class="toggle-btn" id="toggleBtn">Create Account</button>
        </div>
    </div>

    <div class="popup" id="popup">
        <h3 id="popupTitle">Success!</h3>
        <p id="popupMessage">Welcome to SecureVault!</p>
    </div>

    <script>
        class AuthPage {
            constructor() {
                this.isLoginMode = true;
                this.users = this.loadUsers();
                this.init();
            }

            init() {
                this.setupEventListeners();
                this.createSparkles();
            }

            setupEventListeners() {
                const authForm = document.getElementById('authForm');
                const toggleBtn = document.getElementById('toggleBtn');

                authForm.addEventListener('submit', (e) => this.handleAuth(e));
                toggleBtn.addEventListener('click', () => this.toggleAuthMode());
            }

            toggleAuthMode() {
                this.isLoginMode = !this.isLoginMode;
                const authBtn = document.getElementById('authBtn');
                const toggleBtn = document.getElementById('toggleBtn');
                const toggleText = document.getElementById('toggleText');
                const confirmGroup = document.getElementById('confirmPasswordGroup');

                if (this.isLoginMode) {
                    authBtn.textContent = 'Sign In';
                    toggleBtn.textContent = 'Create Account';
                    toggleText.textContent = "Don't have an account?";
                    confirmGroup.style.display = 'none';
                } else {
                    authBtn.textContent = 'Register';
                    toggleBtn.textContent = 'Sign In Instead';
                    toggleText.textContent = "Already have an account?";
                    confirmGroup.style.display = 'block';
                }

                // Add animation effect
                const container = document.getElementById('authContainer');
                container.style.transform = 'scale(0.95)';
                setTimeout(() => {
                    container.style.transform = 'scale(1)';
                }, 150);
            }

            handleAuth(e) {
                e.preventDefault();
                
                const container = document.getElementById('authContainer');
                container.classList.add('loading');

                const email = document.getElementById('email').value;
                const password = document.getElementById('password').value;
                const confirmPassword = document.getElementById('confirmPassword').value;

                setTimeout(() => {
                    if (this.isLoginMode) {
                        this.login(email, password);
                    } else {
                        this.register(email, password, confirmPassword);
                    }
                    container.classList.remove('loading');
                }, 1000);
            }

            register(email, password, confirmPassword) {
                if (password !== confirmPassword) {
                    this.showPopup('Error', 'Passwords do not match!', 'error');
                    return;
                }

                if (password.length < 6) {
                    this.showPopup('Error', 'Password must be at least 6 characters!', 'error');
                    return;
                }

                if (this.users.find(user => user.email === email)) {
                    this.showPopup('Error', 'User already exists!', 'error');
                    return;
                }

                const newUser = {
                    email: email,
                    password: password,
                    points: 0,
                    joinDate: new Date().toISOString()
                };

                this.users.push(newUser);
                this.saveUsers();
                this.showPopup('Success!', 'Account created successfully! You can now sign in.', 'success');
                this.createSuccessSparkles();
                
                setTimeout(() => {
                    if (this.isLoginMode === false) {
                        this.toggleAuthMode();
                        document.getElementById('email').value = email;
                        document.getElementById('password').value = '';
                    }
                }, 2500);
            }

            login(email, password) {
                const user = this.users.find(u => u.email === email && u.password === password);
                
                if (user) {
                    // Store current user in sessionStorage for the dashboard
                    sessionStorage.setItem('currentUser', JSON.stringify(user));
                    
                    this.showPopup('Welcome!', `Hi ${email.split('@')[0]}, redirecting to dashboard...`, 'success');
                    this.createSuccessSparkles();
                    
                    // Redirect to dashboard after animation
                    setTimeout(() => {
                        // In a real app, this would redirect to dashboard.html
                        // For demo purposes, we'll show an alert
                        alert('Redirecting to Dashboard...\n\nIn a real application, this would navigate to dashboard.html');
                        // window.location.href = 'dashboard.html';
                    }, 2000);
                } else {
                    this.showPopup('Error', 'Invalid email or password!', 'error');
                }
            }

            createSparkles() {
                setInterval(() => {
                    const sparkle = document.createElement('div');
                    sparkle.className = 'sparkles';
                    sparkle.innerHTML = '✨';
                    sparkle.style.left = Math.random() * window.innerWidth + 'px';
                    sparkle.style.top = Math.random() * window.innerHeight + 'px';
                    sparkle.style.fontSize = (Math.random() * 15 + 10) + 'px';
                    sparkle.style.animation = 'sparkle 3s ease-out forwards';
                    
                    document.body.appendChild(sparkle);
                    
                    setTimeout(() => {
                        sparkle.remove();
                    }, 3000);
                }, 2000);
            }

            createSuccessSparkles() {
                for (let i = 0; i < 20; i++) {
                    setTimeout(() => {
                        const sparkle = document.createElement('div');
                        sparkle.className = 'sparkles';
                        sparkle.innerHTML = ['✨', '🌟', '⭐', '💫'][Math.floor(Math.random() * 4)];
                        sparkle.style.left = Math.random() * window.innerWidth + 'px';
                        sparkle.style.top = Math.random() * window.innerHeight + 'px';
                        sparkle.style.fontSize = (Math.random() * 25 + 15) + 'px';
                        sparkle.style.animation = 'sparkle 2s ease-out forwards';
                        
                        document.body.appendChild(sparkle);
                        
                        setTimeout(() => {
                            sparkle.remove();
                        }, 2000);
                    }, i * 100);
                }
            }

            showPopup(title, message, type = 'success') {
                const popup = document.getElementById('popup');
                const popupTitle = document.getElementById('popupTitle');
                const popupMessage = document.getElementById('popupMessage');

                popupTitle.textContent = title;
                popupMessage.textContent = message;
                
                popup.className = 'popup';
                if (type === 'error') {
                    popup.classList.add('error');
                }

                popup.classList.add('show');

                setTimeout(() => {
                    popup.classList.remove('show');
                }, 5000);
            }

            loadUsers() {
                try {
                    const saved = JSON.parse(localStorage.getItem('vaultUsers') || '[]');
                    return saved;
                } catch {
                    return [];
                }
            }

            saveUsers() {
                try {
                    localStorage.setItem('vaultUsers', JSON.stringify(this.users));
                } catch {
                    console.error('Failed to save users');
                }
            }
        }

        // Initialize the authentication page
        document.addEventListener('DOMContentLoaded', () => {
            new AuthPage();
        });
    </script>
</body>
</html># secure-vault
we can store files securely and rewards are provided according to the size of the file.
