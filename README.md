<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CloudSave - Animated File Storage</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Arial', sans-serif;
            overflow: hidden;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            height: 100vh;
            position: relative;
        }

        /* Animated Background Bubbles */
        .bubbles {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            overflow: hidden;
            z-index: 1;
        }

        .bubble {
            position: absolute;
            bottom: -100px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 50%;
            animation: rise 10s infinite linear;
            backdrop-filter: blur(5px);
            border: 1px solid rgba(255, 255, 255, 0.2);
        }

        .bubble:nth-child(1) { left: 10%; width: 80px; height: 80px; animation-delay: 0s; }
        .bubble:nth-child(2) { left: 20%; width: 50px; height: 50px; animation-delay: 1s; }
        .bubble:nth-child(3) { left: 35%; width: 100px; height: 100px; animation-delay: 2s; }
        .bubble:nth-child(4) { left: 50%; width: 60px; height: 60px; animation-delay: 3s; }
        .bubble:nth-child(5) { left: 70%; width: 90px; height: 90px; animation-delay: 4s; }
        .bubble:nth-child(6) { left: 85%; width: 40px; height: 40px; animation-delay: 5s; }
        .bubble:nth-child(7) { left: 5%; width: 70px; height: 70px; animation-delay: 6s; }
        .bubble:nth-child(8) { left: 90%; width: 55px; height: 55px; animation-delay: 7s; }

        @keyframes rise {
            0% {
                bottom: -100px;
                transform: translateX(0px);
            }
            50% {
                transform: translateX(100px);
            }
            100% {
                bottom: 100vh;
                transform: translateX(-50px);
            }
        }

        /* Floating particles */
        .particles {
            position: absolute;
            width: 100%;
            height: 100%;
            z-index: 1;
        }

        .particle {
            position: absolute;
            background: rgba(255, 255, 255, 0.3);
            border-radius: 50%;
            animation: float 8s infinite ease-in-out;
        }

        .particle:nth-child(1) { width: 4px; height: 4px; left: 15%; animation-delay: 0s; }
        .particle:nth-child(2) { width: 6px; height: 6px; left: 45%; animation-delay: 2s; }
        .particle:nth-child(3) { width: 3px; height: 3px; left: 75%; animation-delay: 4s; }
        .particle:nth-child(4) { width: 5px; height: 5px; left: 25%; animation-delay: 6s; }
        .particle:nth-child(5) { width: 4px; height: 4px; left: 85%; animation-delay: 1s; }

        @keyframes float {
            0%, 100% { transform: translateY(0px) rotate(0deg); }
            33% { transform: translateY(-30px) rotate(120deg); }
            66% { transform: translateY(30px) rotate(240deg); }
        }

        /* Sign In Page Styles */
        #signin-page {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            z-index: 10;
            position: relative;
        }

        .signin-container {
            background: rgba(255, 255, 255, 0.15);
            backdrop-filter: blur(20px);
            padding: 40px;
            border-radius: 20px;
            border: 1px solid rgba(255, 255, 255, 0.2);
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
            width: 400px;
            text-align: center;
            animation: slideIn 1s ease-out;
        }

        @keyframes slideIn {
            from {
                opacity: 0;
                transform: translateY(-50px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .signin-container h1 {
            color: white;
            margin-bottom: 30px;
            font-size: 2.5em;
            text-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
        }

        .input-group {
            margin-bottom: 20px;
            position: relative;
        }

        .input-group input {
            width: 100%;
            padding: 15px;
            border: none;
            border-radius: 10px;
            background: rgba(255, 255, 255, 0.2);
            color: white;
            font-size: 16px;
            outline: none;
            transition: all 0.3s ease;
        }

        .input-group input::placeholder {
            color: rgba(255, 255, 255, 0.7);
        }

        .input-group input:focus {
            background: rgba(255, 255, 255, 0.3);
            transform: scale(1.02);
        }

        .signin-btn {
            width: 100%;
            padding: 15px;
            border: none;
            border-radius: 10px;
            background: linear-gradient(45deg, #ff6b6b, #ee5a24);
            color: white;
            font-size: 18px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            margin-top: 20px;
        }

        .signin-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
        }

        /* Dashboard Styles */
        #dashboard {
            display: none;
            height: 100vh;
            z-index: 10;
            position: relative;
        }

        .dashboard-header {
            background: rgba(255, 255, 255, 0.15);
            backdrop-filter: blur(20px);
            padding: 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid rgba(255, 255, 255, 0.2);
        }

        .dashboard-header h2 {
            color: white;
            font-size: 1.8em;
        }

        .points-display {
            background: linear-gradient(45deg, #ffd700, #ffed4a);
            color: #333;
            padding: 10px 20px;
            border-radius: 25px;
            font-weight: bold;
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }

        .dashboard-content {
            padding: 30px;
            height: calc(100vh - 80px);
            overflow-y: auto;
        }

        .upload-area {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(15px);
            border: 2px dashed rgba(255, 255, 255, 0.3);
            border-radius: 20px;
            padding: 40px;
            text-align: center;
            margin-bottom: 30px;
            transition: all 0.3s ease;
            cursor: pointer;
        }

        .upload-area:hover {
            background: rgba(255, 255, 255, 0.2);
            transform: translateY(-5px);
        }

        .upload-area h3 {
            color: white;
            margin-bottom: 20px;
            font-size: 1.5em;
        }

        .file-input {
            display: none;
        }

        .upload-btn {
            background: linear-gradient(45deg, #4facfe, #00f2fe);
            color: white;
            padding: 12px 30px;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            transition: all 0.3s ease;
        }

        .upload-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
        }

        .files-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 20px;
            margin-top: 30px;
        }

        .file-card {
            background: rgba(255, 255, 255, 0.15);
            backdrop-filter: blur(15px);
            border-radius: 15px;
            padding: 20px;
            border: 1px solid rgba(255, 255, 255, 0.2);
            transition: all 0.3s ease;
            animation: fadeInUp 0.5s ease-out;
        }

        .file-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2);
        }

        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .file-card h4 {
            color: white;
            margin-bottom: 10px;
            font-size: 1.2em;
        }

        .file-card p {
            color: rgba(255, 255, 255, 0.8);
            font-size: 0.9em;
            margin-bottom: 15px;
        }

        .save-btn {
            background: linear-gradient(45deg, #56ab2f, #a8e6cf);
            color: white;
            padding: 8px 20px;
            border: none;
            border-radius: 15px;
            cursor: pointer;
            font-size: 14px;
            transition: all 0.3s ease;
        }

        .save-btn:hover {
            transform: scale(1.05);
        }

        .save-btn:disabled {
            background: rgba(255, 255, 255, 0.3);
            cursor: not-allowed;
        }

        .reward-popup {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: linear-gradient(45deg, #ffd700, #ffed4a);
            color: #333;
            padding: 20px 40px;
            border-radius: 15px;
            font-weight: bold;
            font-size: 1.2em;
            z-index: 1000;
            animation: rewardPop 0.5s ease-out;
            display: none;
        }

        @keyframes rewardPop {
            0% {
                opacity: 0;
                transform: translate(-50%, -50%) scale(0.5);
            }
            100% {
                opacity: 1;
                transform: translate(-50%, -50%) scale(1);
            }
        }

        /* Background animation for dashboard */
        .dashboard-bg {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(45deg, #667eea 0%, #764ba2 50%, #667eea 100%);
            background-size: 400% 400%;
            animation: gradientShift 10s ease infinite;
            z-index: -1;
        }

        @keyframes gradientShift {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }
    </style>
</head>
<body>
    <!-- Animated Background Elements -->
    <div class="bubbles">
        <div class="bubble"></div>
        <div class="bubble"></div>
        <div class="bubble"></div>
        <div class="bubble"></div>
        <div class="bubble"></div>
        <div class="bubble"></div>
        <div class="bubble"></div>
        <div class="bubble"></div>
    </div>

    <div class="particles">
        <div class="particle"></div>
        <div class="particle"></div>
        <div class="particle"></div>
        <div class="particle"></div>
        <div class="particle"></div>
    </div>

    <!-- Sign In Page -->
    <div id="signin-page">
        <div class="signin-container">
            <h1>CloudSave</h1>
            <form id="signin-form">
                <div class="input-group">
                    <input type="email" id="email" placeholder="Enter your email" required>
                </div>
                <div class="input-group">
                    <input type="password" id="password" placeholder="Enter your password" required>
                </div>
                <button type="submit" class="signin-btn">Sign In & Start Saving</button>
            </form>
        </div>
    </div>

    <!-- Dashboard -->
    <div id="dashboard">
        <div class="dashboard-bg"></div>
        
        <div class="dashboard-header">
            <h2>Welcome to CloudSave Dashboard</h2>
            <div class="points-display">
                🏆 Points: <span id="points-count">0</span>
            </div>
        </div>

        <div class="dashboard-content">
            <div class="upload-area" onclick="document.getElementById('file-input').click()">
                <h3>📁 Upload Your Files</h3>
                <p style="color: rgba(255, 255, 255, 0.8); margin-bottom: 20px;">
                    Drag and drop files here or click to browse
                </p>
                <button class="upload-btn">Choose Files</button>
                <input type="file" id="file-input" class="file-input" multiple>
            </div>

            <div class="files-grid" id="files-grid">
                <!-- Files will be displayed here -->
            </div>
        </div>
    </div>

    <div class="reward-popup" id="reward-popup">
        🎉 +10 Points Earned! 🎉
    </div>

    <script>
        let userPoints = 0;
        let userFiles = [];

        // Sign in functionality
        document.getElementById('signin-form').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const email = document.getElementById('email').value;
            const password = document.getElementById('password').value;
            
            if (email && password) {
                // Simulate loading
                setTimeout(() => {
                    document.getElementById('signin-page').style.display = 'none';
                    document.getElementById('dashboard').style.display = 'block';
                    
                    // Update background for dashboard
                    document.body.style.background = 'none';
                }, 500);
            }
        });

        // File upload functionality
        document.getElementById('file-input').addEventListener('change', function(e) {
            const files = Array.from(e.target.files);
            
            files.forEach(file => {
                const fileObj = {
                    id: Date.now() + Math.random(),
                    name: file.name,
                    size: (file.size / 1024).toFixed(2) + ' KB',
                    type: file.type || 'Unknown',
                    saved: false,
                    file: file
                };
                
                userFiles.push(fileObj);
                displayFile(fileObj);
            });
        });

        function displayFile(fileObj) {
            const filesGrid = document.getElementById('files-grid');
            
            const fileCard = document.createElement('div');
            fileCard.className = 'file-card';
            fileCard.innerHTML = `
                <h4>📄 ${fileObj.name}</h4>
                <p>Size: ${fileObj.size}</p>
                <p>Type: ${fileObj.type}</p>
                <button class="save-btn" onclick="saveFile('${fileObj.id}')" ${fileObj.saved ? 'disabled' : ''}>
                    ${fileObj.saved ? '✅ Saved' : '💾 Save File'}
                </button>
            `;
            
            filesGrid.appendChild(fileCard);
        }

        function saveFile(fileId) {
            const file = userFiles.find(f => f.id == fileId);
            if (file && !file.saved) {
                file.saved = true;
                userPoints += 10;
                
                // Update points display
                document.getElementById('points-count').textContent = userPoints;
                
                // Show reward popup
                const popup = document.getElementById('reward-popup');
                popup.style.display = 'block';
                setTimeout(() => {
                    popup.style.display = 'none';
                }, 2000);
                
                // Update the button
                const filesGrid = document.getElementById('files-grid');
                filesGrid.innerHTML = '';
                userFiles.forEach(f => displayFile(f));
                
                // Add sparkle effect
                createSparkles();
            }
        }

        function createSparkles() {
            for (let i = 0; i < 10; i++) {
                const sparkle = document.createElement('div');
                sparkle.style.position = 'fixed';
                sparkle.style.width = '4px';
                sparkle.style.height = '4px';
                sparkle.style.background = '#ffd700';
                sparkle.style.borderRadius = '50%';
                sparkle.style.left = Math.random() * window.innerWidth + 'px';
                sparkle.style.top = Math.random() * window.innerHeight + 'px';
                sparkle.style.zIndex = '1000';
                sparkle.style.animation = 'sparkle 1s ease-out forwards';
                
                document.body.appendChild(sparkle);
                
                setTimeout(() => {
                    document.body.removeChild(sparkle);
                }, 1000);
            }
        }

        // Add sparkle animation
        const style = document.createElement('style');
        style.textContent = `
            @keyframes sparkle {
                0% {
                    opacity: 1;
                    transform: scale(0) rotate(0deg);
                }
                100% {
                    opacity: 0;
                    transform: scale(1) rotate(180deg);
                }
            }
        `;
        document.head.appendChild(style);

        // Drag and drop functionality
        const uploadArea = document.querySelector('.upload-area');

        uploadArea.addEventListener('dragover', function(e) {
            e.preventDefault();
            uploadArea.style.background = 'rgba(255, 255, 255, 0.3)';
        });

        uploadArea.addEventListener('dragleave', function(e) {
            e.preventDefault();
            uploadArea.style.background = 'rgba(255, 255, 255, 0.1)';
        });

        uploadArea.addEventListener('drop', function(e) {
            e.preventDefault();
            uploadArea.style.background = 'rgba(255, 255, 255, 0.1)';
            
            const files = Array.from(e.dataTransfer.files);
            
            files.forEach(file => {
                const fileObj = {
                    id: Date.now() + Math.random(),
                    name: file.name,
                    size: (file.size / 1024).toFixed(2) + ' KB',
                    type: file.type || 'Unknown',
                    saved: false,
                    file: file
                };
                
                userFiles.push(fileObj);
                displayFile(fileObj);
            });
        });
    </script>
</body>
</html>
