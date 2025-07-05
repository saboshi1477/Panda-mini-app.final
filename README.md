<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Panda Community</title>
    <script src="https://telegram.org/js/telegram-web-app.js"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Arial', sans-serif;
        }
        
        body {
            background-color: #0f0f0f;
            color: #fff;
            padding: 10px;
            padding-bottom: 70px;
        }
        
        .header {
            text-align: center;
            padding: 10px 0;
            margin-bottom: 15px;
            position: relative;
        }
        
        .panda-logo {
            text-align: center;
            margin: 10px 0;
        }
        
        .panda-logo img {
            width: 80px;
            height: 80px;
            border-radius: 50%;
        }
        
        .panda-title {
            font-size: 24px;
            font-weight: bold;
            margin-top: 5px;
            color: #fff;
        }
        
        .bottom-nav {
            position: fixed;
            bottom: 0;
            left: 0;
            right: 0;
            background-color: #212121;
            display: flex;
            justify-content: space-around;
            padding: 10px 0;
            border-top: 1px solid #333;
            z-index: 1000;
        }
        
        .nav-btn {
            display: flex;
            flex-direction: column;
            align-items: center;
            color: #aaa;
            text-decoration: none;
            font-size: 10px;
            width: 25%;
        }
        
        .nav-btn.active {
            color: #fff;
        }
        
        .nav-icon {
            font-size: 20px;
            margin-bottom: 5px;
        }
        
        .box-container {
            display: flex;
            flex-direction: column;
            gap: 15px;
            margin-top: 20px;
        }
        
        .box {
            background-color: #212121;
            padding: 15px;
            border-radius: 10px;
            text-align: center;
            cursor: pointer;
            color: #fff;
            transition: transform 0.2s;
        }
        
        .box:active {
            transform: scale(0.98);
        }
        
        .box-title {
            font-weight: bold;
            margin-bottom: 10px;
        }
        
        .task-grid {
            display: grid;
            grid-template-columns: 1fr;
            gap: 15px;
            margin-top: 20px;
            padding: 10px;
        }

        .task-box {
            background-color: #212121;
            padding: 15px;
            border-radius: 10px;
            text-align: left;
            cursor: pointer;
            color: #fff;
            transition: transform 0.2s;
            position: relative;
        }

        .task-box:active {
            transform: scale(0.98);
        }

        .task-box-name {
            font-weight: bold;
            margin-bottom: 5px;
            font-size: 16px;
        }

        .task-box-reward {
            color: #3aa856;
            font-weight: bold;
            margin-bottom: 15px;
            font-size: 14px;
        }

        .task-box-btn {
            background-color: #3aa856;
            color: white;
            border: none;
            padding: 10px 15px;
            border-radius: 5px;
            cursor: pointer;
            font-weight: bold;
            width: 100%;
            transition: background-color 0.2s;
            font-size: 14px;
            text-align: center;
        }

        .task-box-btn:active {
            background-color: #2d8a47;
        }

        .task-box-btn.complete-btn {
            background-color: #f39c12;
        }

        .task-box.completed {
            opacity: 0.7;
            position: relative;
        }

        .task-box.completed::after {
            content: "";
            position: absolute;
            top: 10px;
            right: 10px;
            width: 10px;
            height: 10px;
            background-color: #ff4444;
            border-radius: 50%;
        }

        .task-box-btn.completed-btn {
            background-color: #666;
            cursor: default;
        }
        
        .balance-box {
            background-color: #212121;
            padding: 15px;
            border-radius: 10px;
            margin: 10px auto;
            text-align: center;
            width: 80%;
        }
        
        .balance-amount {
            font-size: 18px;
            font-weight: bold;
            color: #3aa856;
        }
        
        .balance-label {
            font-size: 14px;
            color: #aaa;
            margin-bottom: 5px;
        }
        
        .settings-btn {
            position: absolute;
            top: 15px;
            right: 15px;
            background: none;
            border: none;
            color: #aaa;
            font-size: 20px;
            cursor: pointer;
            z-index: 1001;
        }
        
        .password-screen {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: rgba(0,0,0,0.9);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 1000;
        }
        
        .password-box {
            background-color: #212121;
            padding: 20px;
            border-radius: 10px;
            width: 80%;
            max-width: 400px;
            color: #fff;
            position: relative;
        }
        
        .password-input {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            border: 1px solid #333;
            border-radius: 5px;
            background-color: #121212;
            color: #fff;
        }
        
        .submit-btn {
            background-color: #3aa856;
            color: white;
            border: none;
            padding: 10px 15px;
            border-radius: 5px;
            cursor: pointer;
            width: 100%;
            font-weight: bold;
        }
        
        .admin-controls {
            margin-top: 20px;
            color: #fff;
        }
        
        .admin-input {
            width: 100%;
            padding: 8px;
            margin: 5px 0;
            border: 1px solid #333;
            border-radius: 5px;
            background-color: #121212;
            color: #fff;
        }
        
        .file-input-label {
            display: block;
            margin: 10px 0;
            padding: 8px;
            background-color: #333;
            border-radius: 5px;
            text-align: center;
            cursor: pointer;
        }
        
        .file-input {
            display: none;
        }
        
        .delete-account-btn {
            background-color: #ff4444;
            color: white;
            border: none;
            padding: 10px 15px;
            border-radius: 5px;
            cursor: pointer;
            width: 100%;
            font-weight: bold;
            margin-top: 20px;
        }
        
        .hidden {
            display: none;
        }
        
        .settings-options {
            display: none;
            margin-top: 15px;
        }
        
        .settings-options.show {
            display: block;
        }
        
        .close-settings {
            position: absolute;
            top: 10px;
            right: 10px;
            background: none;
            border: none;
            color: #aaa;
            font-size: 20px;
            cursor: pointer;
        }
        
        .invite-container {
            background-color: #212121;
            padding: 15px;
            border-radius: 10px;
            margin-bottom: 15px;
        }
        
        .invite-header {
            font-size: 18px;
            font-weight: bold;
            margin-bottom: 10px;
            color: #3aa856;
        }
        
        .invite-text {
            margin-bottom: 15px;
            line-height: 1.4;
        }
        
        .invite-reward {
            font-weight: bold;
            color: #3aa856;
            margin-bottom: 15px;
        }
        
        .invite-stats {
            display: flex;
            justify-content: space-between;
            margin-bottom: 15px;
        }
        
        .invite-stat {
            text-align: center;
        }
        
        .invite-stat-value {
            font-size: 18px;
            font-weight: bold;
            color: #3aa856;
        }
        
        .invite-stat-label {
            font-size: 12px;
            color: #aaa;
        }
        
        .custom-content-box {
            background-color: #212121;
            padding: 15px;
            border-radius: 10px;
            margin: 15px 0;
            text-align: center;
        }
        
        .no-tasks-message {
            text-align: center;
            margin-top: 20px;
            color: #aaa;
        }
        
        .task-content {
            display: flex;
            flex-direction: column;
        }
        
        .task-action-btn {
            align-self: flex-end;
            width: 100px;
        }
        
        .completed-tasks-box {
            background-color: #212121;
            padding: 15px;
            border-radius: 10px;
            margin: 10px auto;
            text-align: center;
            width: 80%;
        }
        
        .completed-tasks-label {
            font-size: 14px;
            color: #aaa;
            margin-bottom: 5px;
        }
        
        .completed-tasks-amount {
            font-size: 18px;
            font-weight: bold;
            color: #3aa856;
        }
        
        .balance-info-text {
            font-size: 16px;
            color: #fff;
            text-align: center;
            margin: 15px 20px;
            padding: 15px;
            line-height: 1.5;
            font-weight: bold;
        }
        
        .balance-container {
            margin-top: 10px;
        }
        
        .referral-list {
            margin-top: 20px;
            background-color: #212121;
            border-radius: 10px;
            padding: 15px;
        }
        
        .referral-item {
            display: flex;
            justify-content: space-between;
            padding: 10px 0;
            border-bottom: 1px solid #333;
        }
        
        .referral-item:last-child {
            border-bottom: none;
        }
        
        .referral-username {
            font-weight: bold;
        }
        
        .referral-earned {
            color: #3aa856;
            font-weight: bold;
        }
        
        .referral-list-title {
            font-size: 16px;
            font-weight: bold;
            margin-bottom: 15px;
            color: #3aa856;
        }
        
        .no-referrals {
            text-align: center;
            color: #aaa;
            padding: 10px;
        }
        
        .invite-btn {
            background-color: #3aa856;
            color: white;
            border: none;
            padding: 12px 20px;
            border-radius: 5px;
            cursor: pointer;
            font-weight: bold;
            width: 100%;
            font-size: 16px;
            margin-top: 10px;
            text-transform: uppercase;
        }
        
        /* New styles for better button interaction */
        .btn {
            transition: all 0.2s ease;
        }
        
        .btn:active {
            transform: scale(0.95);
        }
        
        .btn:disabled {
            opacity: 0.6;
            cursor: not-allowed;
        }
        
        /* New styles for invite link box */
        .invite-link-box {
            background-color: #333;
            padding: 15px;
            border-radius: 8px;
            margin: 15px 0;
            position: relative;
        }
        
        .invite-link {
            word-break: break-all;
            font-size: 14px;
            color: #3aa856;
            font-weight: bold;
            margin: 10px 0;
        }
        
        .copy-btn {
            background-color: #3aa856;
            color: white;
            border: none;
            padding: 8px 15px;
            border-radius: 5px;
            cursor: pointer;
            font-weight: bold;
            width: 100%;
            margin-top: 10px;
        }
        
        .copy-btn:active {
            background-color: #2d8a47;
        }
        
        .copied-message {
            color: #3aa856;
            font-size: 12px;
            text-align: center;
            margin-top: 5px;
            display: none;
        }
        
        .share-btn {
            background-color: #0088cc;
            color: white;
            border: none;
            padding: 12px 20px;
            border-radius: 5px;
            cursor: pointer;
            font-weight: bold;
            width: 100%;
            font-size: 16px;
            margin-top: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }
        
        .share-btn i {
            font-size: 18px;
        }
        
        /* Share options */
        .share-options {
            display: none;
            position: fixed;
            bottom: 80px;
            left: 0;
            right: 0;
            background-color: #212121;
            padding: 15px;
            border-radius: 10px 10px 0 0;
            z-index: 1001;
            box-shadow: 0 -2px 10px rgba(0,0,0,0.5);
        }
        
        .share-options.show {
            display: block;
        }
        
        .share-option {
            display: flex;
            align-items: center;
            padding: 12px;
            margin: 5px 0;
            border-radius: 5px;
            background-color: #333;
            cursor: pointer;
        }
        
        .share-option i {
            margin-right: 10px;
            font-size: 20px;
        }
        
        .share-close {
            text-align: center;
            margin-top: 10px;
            padding: 10px;
            color: #aaa;
            cursor: pointer;
        }
        
        /* Admin task management styles */
        .task-management {
            margin-top: 20px;
        }
        
        .task-list {
            margin-top: 15px;
        }
        
        .task-item {
            background-color: #333;
            padding: 10px;
            border-radius: 5px;
            margin-bottom: 10px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .task-item-info {
            flex: 1;
        }
        
        .task-item-name {
            font-weight: bold;
            margin-bottom: 5px;
        }
        
        .task-item-reward {
            color: #3aa856;
            font-size: 14px;
        }
        
        .task-item-actions {
            display: flex;
            gap: 5px;
        }
        
        .task-action {
            background-color: #444;
            border: none;
            color: white;
            padding: 5px 10px;
            border-radius: 3px;
            cursor: pointer;
        }
        
        .task-action.edit {
            background-color: #f39c12;
        }
        
        .task-action.delete {
            background-color: #ff4444;
        }
        
        .add-task-form {
            margin-top: 20px;
            background-color: #333;
            padding: 15px;
            border-radius: 5px;
        }
        
        .form-group {
            margin-bottom: 15px;
        }
        
        .form-label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
        }
        
        .form-input {
            width: 100%;
            padding: 8px;
            border-radius: 4px;
            border: 1px solid #555;
            background-color: #222;
            color: white;
        }
        
        .form-actions {
            display: flex;
            gap: 10px;
            margin-top: 15px;
        }
        
        .form-btn {
            padding: 8px 15px;
            border-radius: 4px;
            border: none;
            cursor: pointer;
            font-weight: bold;
        }
        
        .form-btn.primary {
            background-color: #3aa856;
            color: white;
        }
        
        .form-btn.secondary {
            background-color: #666;
            color: white;
        }
    </style>
</head>
<body>
    <div id="home-screen">
        <div class="header">
            <button class="settings-btn" onclick="showPasswordScreen()">
                <i class="fas fa-cog"></i>
            </button>
            <div class="panda-logo">
                <img id="home-logo" src="https://i.imgur.com/3QZqJYt.png" alt="Panda Head">
                <div class="panda-title">PANDA</div>
                <div id="custom-content" class="custom-content-box">
                    Welcome to Panda Community!
                </div>
            </div>
        </div>
        
        <div class="box-container">
            <div class="box" onclick="window.open('https://t.me/pandacommuni', '_blank')">
                <div class="box-title">Join our community</div>
            </div>
            <div class="box" onclick="window.open('https://x.com/pandacommunityy?t=jtIyizD2bjBCbCjvB3yUrg&s=09', '_blank')">
                <div class="box-title">Join our X community</div>
            </div>
        </div>
    </div>
    
    <div id="earn-screen" class="hidden">
        <div class="task-grid" id="tasks-container">
            <!-- Tasks will be loaded here -->
        </div>
    </div>
    
    <div id="balance-screen" class="hidden">
        <div class="balance-info-text">
            ALL YOUR INFORMATION IS HERE, FROM WHERE YOU HAVE EARNED, HOW MUCH YOU HAVE EARNED AND HOW MANY TASKS YOU HAVE COMPLETED
        </div>
        
        <div class="balance-container">
            <div class="balance-box">
                <div class="balance-label">Total balance</div>
                <div class="balance-amount" id="total-balance">0 PANDA</div>
            </div>
            
            <div class="balance-box">
                <div class="balance-label">Earned from tasks</div>
                <div class="balance-amount" id="task-balance">0 PANDA</div>
            </div>
            
            <div class="balance-box">
                <div class="balance-label">Earned from referrals</div>
                <div class="balance-amount" id="referral-balance">0 PANDA</div>
            </div>
            
            <div class="completed-tasks-box">
                <div class="completed-tasks-label">Completed Tasks</div>
                <div class="completed-tasks-amount" id="completed-tasks">0</div>
            </div>
        </div>
    </div>
    
    <div id="friends-screen" class="hidden">
        <div class="invite-container">
            <div class="invite-header">INVITE FRIENDS & EARN</div>
            <div class="invite-text">
                Share your referral link with friends and earn 30 PANDA tokens for each successful referral!
            </div>
            
            <div class="invite-reward">
                You earn: 30 PANDA per referral
            </div>
            
            <div class="invite-stats">
                <div class="invite-stat">
                    <div class="invite-stat-value" id="invited-count">0</div>
                    <div class="invite-stat-label">Friends Invited</div>
                </div>
                <div class="invite-stat">
                    <div class="invite-stat-value" id="earned-tokens">0</div>
                    <div class="invite-stat-label">Tokens Earned</div>
                </div>
            </div>
            
            <div class="invite-link-box">
                <div>Your unique referral link:</div>
                <div class="invite-link" id="referral-link">https://t.me/Pandacm_bot?start=loading...</div>
                <button class="copy-btn" onclick="copyInviteLink()">
                    <i class="fas fa-copy"></i> COPY LINK
                </button>
                <div class="copied-message" id="copied-message">Link copied to clipboard!</div>
            </div>
            
            <button class="share-btn" onclick="showShareOptions()">
                <i class="fas fa-share-alt"></i> SHARE LINK
            </button>
        </div>
        
        <div class="referral-list">
            <div class="referral-list-title">YOUR REFERRALS</div>
            <div id="referrals-container">
                <!-- Referrals will be listed here -->
            </div>
        </div>
    </div>
    
    <!-- Share Options Modal -->
    <div class="share-options" id="share-options">
        <div class="share-option" onclick="shareViaTelegram()">
            <i class="fab fa-telegram"></i>
            <span>Share via Telegram</span>
        </div>
        <div class="share-option" onclick="shareViaWhatsApp()">
            <i class="fab fa-whatsapp"></i>
            <span>Share via WhatsApp</span>
        </div>
        <div class="share-option" onclick="shareViaOther()">
            <i class="fas fa-share"></i>
            <span>Other sharing options</span>
        </div>
        <div class="share-close" onclick="hideShareOptions()">
            Close
        </div>
    </div>
    
    <div class="bottom-nav">
        <a href="#" class="nav-btn active" onclick="showScreen('home')">
            <span class="nav-icon"><i class="fas fa-home"></i></span>
            <span>Home</span>
        </a>
        <a href="#" class="nav-btn" onclick="showScreen('earn')">
            <span class="nav-icon"><i class="fas fa-coins"></i></span>
            <span>Earn</span>
        </a>
        <a href="#" class="nav-btn" onclick="showScreen('balance')">
            <span class="nav-icon"><i class="fas fa-wallet"></i></span>
            <span>Balance</span>
        </a>
        <a href="#" class="nav-btn" onclick="showScreen('friends')">
            <span class="nav-icon"><i class="fas fa-user-friends"></i></span>
            <span>Friends</span>
        </a>
    </div>
    
    <div id="password-screen" class="hidden password-screen">
        <div class="password-box">
            <button class="close-settings" onclick="closeSettings()">
                <i class="fas fa-times"></i>
            </button>
            
            <h3>Settings</h3>
            
            <div class="box" onclick="toggleSettingsOptions()">
                <div class="box-title">Admin Panel</div>
            </div>
            
            <div id="settings-options" class="settings-options">
                <input type="password" class="password-input" id="admin-password" placeholder="Enter Admin Password">
                <button class="submit-btn" onclick="checkPassword()">Submit</button>
            </div>
            
            <button class="delete-account-btn" onclick="confirmDeleteAccount()">
                Delete Account
            </button>
        </div>
    </div>
    
    <div id="admin-controls" class="hidden">
        <div class="admin-controls">
            <button class="close-settings" onclick="closeAdminPanel()">
                <i class="fas fa-times"></i>
            </button>
            
            <h3>Admin Panel</h3>
            
            <h4>Customize Home Screen</h4>
            <label class="file-input-label">
                Upload Logo Image
                <input type="file" class="file-input" id="logo-upload" accept="image/*">
            </label>
            <small id="logo-file-name">No file selected</small>
            
            <textarea class="admin-input" id="custom-content-input" placeholder="Enter custom content for home screen"></textarea>
            <button class="submit-btn" onclick="updateCustomContent()">Update Content</button>
            
            <div class="task-management">
                <h4>Task Management</h4>
                
                <div class="add-task-form" id="task-form">
                    <div class="form-group">
                        <label class="form-label">Task Name</label>
                        <input type="text" class="form-input" id="task-name" placeholder="Enter task name">
                    </div>
                    
                    <div class="form-group">
                        <label class="form-label">Reward Amount</label>
                        <input type="number" class="form-input" id="task-reward" placeholder="Enter reward amount" min="0">
                    </div>
                    
                    <div class="form-group">
                        <label class="form-label">Task Link</label>
                        <input type="text" class="form-input" id="task-link" placeholder="Enter URL for the task">
                    </div>
                    
                    <div class="form-group">
                        <label class="form-label">Action Text</label>
                        <input type="text" class="form-input" id="task-action" placeholder="Enter button text (e.g. 'Start', 'Join')" value="Start">
                    </div>
                    
                    <div class="form-actions">
                        <button class="form-btn primary" id="save-task-btn" onclick="saveTask()">Save Task</button>
                        <button class="form-btn secondary" id="cancel-task-btn" onclick="cancelTaskEdit()" style="display: none;">Cancel</button>
                    </div>
                </div>
                
                <div class="task-list" id="admin-tasks-list">
                    <!-- Admin task list will be loaded here -->
                </div>
            </div>
            
            <button class="delete-account-btn" onclick="closeAdminPanel()">
                Close Admin Panel
            </button>
        </div>
    </div>

    <!-- Firebase SDK -->
    <script src="https://www.gstatic.com/firebasejs/9.6.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.6.0/firebase-database-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.6.0/firebase-auth-compat.js"></script>

    <script>
        // Firebase configuration and initialization
        const firebaseConfig = {
            apiKey: "AIzaSyA9whBdHuH9yuwuFQVuYVJ1nmd8sM1yX4M",
            authDomain: "panda-mini-app-9857b.firebaseapp.com",
            databaseURL: "https://panda-mini-app-9857b-default-rtdb.firebaseio.com",
            projectId: "panda-mini-app-9857b",
            storageBucket: "panda-mini-app-9857b.appspot.com",
            messagingSenderId: "120018184012",
            appId: "1:120018184012:web:a7ff5b0e45a7ddfd6611e9",
            measurementId: "G-W9P3D2ZMJQ"
        };

        // Initialize Firebase
        firebase.initializeApp(firebaseConfig);
        const database = firebase.database();

        // Initialize Telegram WebApp
        const tg = window.Telegram.WebApp;
        if (tg) {
            tg.expand();
        }

        // Generate a unique user ID
        function getUserId() {
            if (tg && tg.initDataUnsafe && tg.initDataUnsafe.user) {
                return tg.initDataUnsafe.user.id.toString();
            }
            
            let userId = localStorage.getItem('panda_user_id');
            if (!userId) {
                userId = 'user-' + Math.random().toString(36).substr(2, 9);
                localStorage.setItem('panda_user_id', userId);
            }
            return userId;
        }

        const userId = getUserId();
        const inviteLink = `https://t.me/Pandacm_bot?start=${userId}`;

        let userData = {
            totalBalance: 0,
            taskBalance: 0,
            referralBalance: 0,
            invitedFriends: 0,
            completedTasks: [],
            pendingTasks: {},
            referrals: []
        };

        let tasks = [];
        let currentEditingTaskId = null;

        // Load user data from Firebase
        async function loadUserData() {
            try {
                const snapshot = await firebase.database().ref('users/' + userId).once('value');
                if (snapshot.exists()) {
                    userData = snapshot.val();
                    localStorage.setItem('pandaUserData', JSON.stringify(userData));
                } else {
                    // New user - save default data
                    await saveUserData();
                }
                return userData;
            } catch (error) {
                console.error("Error loading user data:", error);
                // Try to load from local storage
                const localData = localStorage.getItem('pandaUserData');
                if (localData) {
                    userData = JSON.parse(localData);
                }
                return userData;
            }
        }

        // Save user data to Firebase
        async function saveUserData() {
            try {
                await firebase.database().ref('users/' + userId).set(userData);
                localStorage.setItem('pandaUserData', JSON.stringify(userData));
                return true;
            } catch (error) {
                console.error("Error saving user data:", error);
                return false;
            }
        }

        // Load tasks from Firebase
        async function loadTasks() {
            try {
                const snapshot = await firebase.database().ref('tasks').once('value');
                if (snapshot.exists()) {
                    tasks = snapshot.val();
                } else {
                    // Initialize with default tasks if none exist
                    tasks = [
                        {
                            id: 1,
                            name: "Join our Telegram community",
                            reward: 100,
                            rewardType: "PANDA",
                            link: "https://t.me/pandacommuni",
                            action: "Start"
                        },
                        {
                            id: 2,
                            name: "Join our X community",
                            reward: 100,
                            rewardType: "PANDA",
                            link: "https://x.com/pandacommunityy?t=jtIyizD2bjBCbCjvB3yUrg&s=09",
                            action: "Start"
                        }
                    ];
                    await firebase.database().ref('tasks').set(tasks);
                }
                return tasks;
            } catch (error) {
                console.error("Error loading tasks:", error);
                return [];
            }
        }

        // Check for referral
        async function checkReferral() {
            const urlParams = new URLSearchParams(window.location.search);
            const referrerId = urlParams.get('ref');
            
            if (referrerId && referrerId !== userId) {
                try {
                    const referrerData = await firebase.database().ref('users/' + referrerId).once('value')
                        .then(snapshot => snapshot.val() || {
                            referrals: [],
                            referralBalance: 0,
                            invitedFriends: 0,
                            totalBalance: 0
                        });
                    
                    // Get username
                    let username = "Telegram User";
                    if (tg && tg.initDataUnsafe && tg.initDataUnsafe.user) {
                        username = "@" + (tg.initDataUnsafe.user.username || 
                                        tg.initDataUnsafe.user.first_name + 
                                        (tg.initDataUnsafe.user.last_name ? " " + tg.initDataUnsafe.user.last_name : ""));
                    }
                    
                    // Update referrer data
                    referrerData.referrals.push({
                        username: username,
                        earned: 30,
                        date: new Date().toISOString()
                    });
                    referrerData.referralBalance += 30;
                    referrerData.invitedFriends += 1;
                    referrerData.totalBalance += 30;
                    
                    // Save referrer data
                    await firebase.database().ref('users/' + referrerId).set(referrerData);
                    
                    // Show welcome message
                    if (tg && tg.showAlert) {
                        tg.showAlert(`Welcome! You were referred by ${referrerId}. You'll both earn rewards!`);
                    } else {
                        alert(`Welcome! You were referred by ${referrerId}. You'll both earn rewards!`);
                    }
                } catch (error) {
                    console.error("Error processing referral:", error);
                }
            }
        }

        // Initialize the app
        async function initializeApp() {
            await checkReferral();
            await loadUserData();
            await loadTasks();
            
            // Update UI
            updateBalanceDisplay();
            renderTasks();
            updateInviteStats();
            renderReferrals();
            
            // Set referral link
            document.getElementById('referral-link').textContent = inviteLink;
            
            // Load custom content
            const customContent = await firebase.database().ref('customContent').once('value')
                .then(snapshot => snapshot.val());
            if (customContent) {
                document.getElementById('custom-content').innerHTML = customContent;
            }
            
            // Load logo
            const logoUrl = await firebase.database().ref('logo').once('value')
                .then(snapshot => snapshot.val());
            if (logoUrl) {
                document.getElementById('home-logo').src = logoUrl;
            }
        }

        // Update balance display
        function updateBalanceDisplay() {
            document.getElementById('total-balance').textContent = `${userData.totalBalance} PANDA`;
            document.getElementById('task-balance').textContent = `${userData.taskBalance} PANDA`;
            document.getElementById('referral-balance').textContent = `${userData.referralBalance} PANDA`;
            document.getElementById('completed-tasks').textContent = userData.completedTasks.length;
        }

        // Update invite statistics
        function updateInviteStats() {
            document.getElementById('invited-count').textContent = userData.invitedFriends;
            document.getElementById('earned-tokens').textContent = userData.referralBalance;
        }

        // Render tasks
        function renderTasks() {
            const container = document.getElementById('tasks-container');
            container.innerHTML = '';
            
            const availableTasks = tasks.filter(task => !userData.completedTasks.includes(task.id));
            
            if (availableTasks.length === 0) {
                container.innerHTML = '<div class="no-tasks-message">No tasks available at the moment. Check back later!</div>';
                return;
            }
            
            availableTasks.forEach(task => {
                const isPending = userData.pendingTasks && userData.pendingTasks[task.id];
                const isCompleted = userData.completedTasks && userData.completedTasks.includes(task.id);
                
                const taskElement = document.createElement('div');
                taskElement.className = `task-box ${isCompleted ? 'completed' : ''}`;
                
                const rewardText = task.reward > 0 ? `+${task.reward} ${task.rewardType}` : '';
                
                if (isPending) {
                    taskElement.innerHTML = `
                        <div class="task-content">
                            <div class="task-box-name">${task.name}</div>
                            <div class="task-box-reward">${rewardText}</div>
                            <button class="task-box-btn complete-btn task-action-btn" onclick="completeTask(${task.id})">
                                ${task.action}
                            </button>
                        </div>
                    `;
                } else if (isCompleted) {
                    taskElement.innerHTML = `
                        <div class="task-content">
                            <div class="task-box-name">${task.name}</div>
                            <div class="task-box-reward">${rewardText}</div>
                            <button class="task-box-btn completed-btn task-action-btn" disabled>
                                Completed
                            </button>
                        </div>
                    `;
                } else {
                    taskElement.innerHTML = `
                        <div class="task-content">
                            <div class="task-box-name">${task.name}</div>
                            <div class="task-box-reward">${rewardText}</div>
                            <button class="task-box-btn task-action-btn" onclick="startTask(${task.id})">
                                ${task.action}
                            </button>
                        </div>
                    `;
                }
                container.appendChild(taskElement);
            });
        }

        // Render referrals
        function renderReferrals() {
            const container = document.getElementById('referrals-container');
            container.innerHTML = '';
            
            if (!userData.referrals || userData.referrals.length === 0) {
                container.innerHTML = '<div class="no-referrals">No referrals yet</div>';
                return;
            }
            
            userData.referrals.forEach(referral => {
                const referralElement = document.createElement('div');
                referralElement.className = 'referral-item';
                referralElement.innerHTML = `
                    <span class="referral-username">${referral.username}</span>
                    <span class="referral-earned">+${referral.earned} PANDA</span>
                `;
                container.appendChild(referralElement);
            });
        }

        // Start a task
        async function startTask(taskId) {
            const task = tasks.find(t => t.id === taskId);
            if (task && !userData.completedTasks.includes(taskId)) {
                userData.pendingTasks = userData.pendingTasks || {};
                userData.pendingTasks[taskId] = true;
                await saveUserData();
                renderTasks();
                
                if (task.link && task.link !== "#") {
                    window.open(task.link, '_blank');
                }
                
                // Simulate task completion after 3 seconds
                setTimeout(() => {
                    completeTask(taskId);
                }, 3000);
            }
        }

        // Complete a task
        async function completeTask(taskId) {
            const task = tasks.find(t => t.id === taskId);
            if (task && userData.pendingTasks && userData.pendingTasks[taskId] && 
                !(userData.completedTasks && userData.completedTasks.includes(taskId))) {
                
                delete userData.pendingTasks[taskId];
                userData.completedTasks = userData.completedTasks || [];
                userData.completedTasks.push(taskId);
                userData.taskBalance = (userData.taskBalance || 0) + task.reward;
                userData.totalBalance = (userData.totalBalance || 0) + task.reward;
                
                const success = await saveUserData();
                if (success) {
                    renderTasks();
                    updateBalanceDisplay();
                    
                    const message = `Task completed! You earned ${task.reward} ${task.rewardType}.`;
                    if (tg && tg.showAlert) {
                        tg.showAlert(message);
                    } else {
                        alert(message);
                    }
                }
            }
        }

        // Copy invite link
        function copyInviteLink() {
            if (navigator.clipboard) {
                navigator.clipboard.writeText(inviteLink).then(() => {
                    const msg = document.getElementById('copied-message');
                    msg.style.display = 'block';
                    setTimeout(() => {
                        msg.style.display = 'none';
                    }, 2000);
                });
            } else {
                // Fallback for browsers without Clipboard API
                const textarea = document.createElement('textarea');
                textarea.value = inviteLink;
                document.body.appendChild(textarea);
                textarea.select();
                document.execCommand('copy');
                document.body.removeChild(textarea);
                
                const msg = document.getElementById('copied-message');
                msg.style.display = 'block';
                setTimeout(() => {
                    msg.style.display = 'none';
                }, 2000);
            }
        }

        // Show share options
        function showShareOptions() {
            document.getElementById('share-options').classList.add('show');
        }

        // Hide share options
        function hideShareOptions() {
            document.getElementById('share-options').classList.remove('show');
        }

        // Share via Telegram
        function shareViaTelegram() {
            hideShareOptions();
            const shareText = `馃惣鉂わ笍 Welcome to Panda Community! We are excited to say that we are a community of crypto enthusiasts helping each other grow. Join us now and start earning rewards!\n\nUse my referral link: ${inviteLink}`;
            
            if (tg && tg.platform) {
                tg.share(shareText, (success) => {
                    if (success && tg.showAlert) {
                        tg.showAlert("Invite shared successfully!");
                    }
                }, (error) => {
                    if (tg.showAlert) {
                        tg.showAlert("Couldn't share: " + error);
                    }
                });
            } else {
                window.open(`https://t.me/share/url?url=${encodeURIComponent(inviteLink)}&text=${encodeURIComponent(shareText)}`, '_blank');
            }
        }

        // Share via WhatsApp
        function shareViaWhatsApp() {
            hideShareOptions();
            const shareText = `馃惣鉂わ笍 Welcome to Panda Community! Use my referral link: ${inviteLink}`;
            window.open(`https://wa.me/?text=${encodeURIComponent(shareText)}`, '_blank');
        }

        // Share via other options
        function shareViaOther() {
            hideShareOptions();
            if (navigator.share) {
                navigator.share({
                    title: 'Join Panda Community',
                    text: '馃惣鉂わ笍 Welcome to Panda Community!',
                    url: inviteLink
                }).catch(err => {
                    console.log('Error sharing:', err);
                    copyInviteLink();
                });
            } else {
                copyInviteLink();
                alert("Link copied to clipboard! You can now paste it anywhere.");
            }
        }

        // Show screen
        function showScreen(screenName) {
            document.getElementById('home-screen').classList.add('hidden');
            document.getElementById('earn-screen').classList.add('hidden');
            document.getElementById('balance-screen').classList.add('hidden');
            document.getElementById('friends-screen').classList.add('hidden');
            
            document.getElementById(`${screenName}-screen`).classList.remove('hidden');
            
            const navButtons = document.querySelectorAll('.nav-btn');
            navButtons.forEach(btn => {
                btn.classList.remove('active');
            });
            
            const activeBtnIndex = 
                screenName === 'home' ? 1 : 
                screenName === 'earn' ? 2 : 
                screenName === 'balance' ? 3 : 4;
            
            document.querySelector(`.nav-btn:nth-child(${activeBtnIndex})`).classList.add('active');
            
            if (screenName === 'earn') {
                renderTasks();
            }
            
            if (screenName === 'balance') {
                updateBalanceDisplay();
            }
            
            if (screenName === 'friends') {
                renderReferrals();
            }
        }

        // Show password screen
        function showPasswordScreen() {
            document.getElementById('password-screen').classList.remove('hidden');
        }

        // Close settings
        function closeSettings() {
            document.getElementById('password-screen').classList.add('hidden');
            document.getElementById('settings-options').classList.remove('show');
        }

        // Toggle settings options
        function toggleSettingsOptions() {
            const options = document.getElementById('settings-options');
            options.classList.toggle('show');
        }

        // Check admin password
        function checkPassword() {
            const password = document.getElementById('admin-password').value;
            if (password === '1477653897') {
                document.getElementById('password-screen').classList.add('hidden');
                document.getElementById('admin-controls').classList.remove('hidden');
                document.getElementById('settings-options').classList.remove('show');
                showScreen('home');
                
                // Load admin tasks
                renderAdminTasks();
            } else {
                const message = "Wrong password!";
                if (tg && tg.showAlert) {
                    tg.showAlert(message);
                } else {
                    alert(message);
                }
            }
        }

        // Close admin panel
        function closeAdminPanel() {
            document.getElementById('admin-controls').classList.add('hidden');
            currentEditingTaskId = null;
            resetTaskForm();
        }

        // Render admin tasks
        async function renderAdminTasks() {
            const container = document.getElementById('admin-tasks-list');
            container.innerHTML = '';
            
            const tasks = await loadTasks();
            
            if (tasks.length === 0) {
                container.innerHTML = '<div style="text-align: center; color: #aaa; padding: 15px;">No tasks created yet</div>';
                return;
            }
            
            tasks.forEach(task => {
                const taskElement = document.createElement('div');
                taskElement.className = 'task-item';
                taskElement.innerHTML = `
                    <div class="task-item-info">
                        <div class="task-item-name">${task.name}</div>
                        <div class="task-item-reward">Reward: ${task.reward} PANDA</div>
                    </div>
                    <div class="task-item-actions">
                        <button class="task-action edit" onclick="editTask(${task.id})">
                            <i class="fas fa-edit"></i>
                        </button>
                        <button class="task-action delete" onclick="deleteTask(${task.id})">
                            <i class="fas fa-trash"></i>
                        </button>
                    </div>
                `;
                container.appendChild(taskElement);
            });
        }

        // Save task (admin)
        async function saveTask() {
            const name = document.getElementById('task-name').value.trim();
            const reward = parseInt(document.getElementById('task-reward').value);
            const link = document.getElementById('task-link').value.trim();
            const action = document.getElementById('task-action').value.trim() || "Start";
            
            if (!name) {
                const message = "Please enter a task name";
                if (tg && tg.showAlert) {
                    tg.showAlert(message);
                } else {
                    alert(message);
                }
                return;
            }
            
            if (isNaN(reward)) {
                const message = "Please enter a valid reward amount";
                if (tg && tg.showAlert) {
                    tg.showAlert(message);
                } else {
                    alert(message);
                }
                return;
            }
            
            const tasks = await loadTasks();
            
            if (currentEditingTaskId) {
                // Update existing task
                const taskIndex = tasks.findIndex(t => t.id === currentEditingTaskId);
                if (taskIndex !== -1) {
                    tasks[taskIndex] = {
                        ...tasks[taskIndex],
                        name: name,
                        reward: reward,
                        link: link,
                        action: action
                    };
                    
                    await firebase.database().ref('tasks').set(tasks);
                    
                    const message = "Task updated successfully!";
                    if (tg && tg.showAlert) {
                        tg.showAlert(message);
                    } else {
                        alert(message);
                    }
                }
            } else {
                // Create new task
                const newId = tasks.length > 0 ? Math.max(...tasks.map(t => t.id)) + 1 : 1;
                tasks.push({
                    id: newId,
                    name: name,
                    reward: reward,
                    rewardType: "PANDA",
                    link: link,
                    action: action
                });
                
                await firebase.database().ref('tasks').set(tasks);
                
                const message = "Task created successfully!";
                if (tg && tg.showAlert) {
                    tg.showAlert(message);
                } else {
                    alert(message);
                }
            }
            
            renderAdminTasks();
            resetTaskForm();
        }

        // Edit task (admin)
        function editTask(taskId) {
            const task = tasks.find(t => t.id === taskId);
            if (task) {
                currentEditingTaskId = taskId;
                document.getElementById('task-name').value = task.name;
                document.getElementById('task-reward').value = task.reward;
                document.getElementById('task-link').value = task.link;
                document.getElementById('task-action').value = task.action;
                
                document.getElementById('save-task-btn').textContent = "Update Task";
                document.getElementById('cancel-task-btn').style.display = "block";
                
                // Scroll to form
                document.getElementById('task-form').scrollIntoView({ behavior: 'smooth' });
            }
        }

        // Delete task (admin)
        async function deleteTask(taskId) {
            if (confirm("Are you sure you want to delete this task?")) {
                const tasks = await loadTasks();
                const updatedTasks = tasks.filter(t => t.id !== taskId);
                
                await firebase.database().ref('tasks').set(updatedTasks);
                
                renderAdminTasks();
                const message = "Task deleted successfully!";
                if (tg && tg.showAlert) {
                    tg.showAlert(message);
                } else {
                    alert(message);
                }
            }
        }

        // Cancel task edit (admin)
        function cancelTaskEdit() {
            resetTaskForm();
        }

        // Reset task form (admin)
        function resetTaskForm() {
            currentEditingTaskId = null;
            document.getElementById('task-name').value = "";
            document.getElementById('task-reward').value = "";
            document.getElementById('task-link').value = "";
            document.getElementById('task-action').value = "Start";
            
            document.getElementById('save-task-btn').textContent = "Save Task";
            document.getElementById('cancel-task-btn').style.display = "none";
        }

        // Update custom content (admin)
        async function updateCustomContent() {
            const content = document.getElementById('custom-content-input').value;
            document.getElementById('custom-content').innerHTML = content;
            
            await firebase.database().ref('customContent').set(content);
            
            const message = "Home content updated successfully!";
            if (tg && tg.showAlert) {
                tg.showAlert(message);
            } else {
                alert(message);
            }
        }

        // Confirm account deletion
        function confirmDeleteAccount() {
            if (confirm("Are you sure you want to delete your account? This cannot be undone!")) {
                deleteAccount();
            }
        }

        // Delete account
        async function deleteAccount() {
            try {
                await firebase.database().ref('users/' + userId).remove();
                
                // Reset local data
                userData = {
                    totalBalance: 0,
                    taskBalance: 0,
                    referralBalance: 0,
                    invitedFriends: 0,
                    completedTasks: [],
                    pendingTasks: {},
                    referrals: []
                };
                
                localStorage.removeItem('pandaUserData');
                
                updateBalanceDisplay();
                renderTasks();
                updateInviteStats();
                renderReferrals();
                
                const message = "Your account has been reset. All data cleared.";
                if (tg && tg.showAlert) {
                    tg.showAlert(message);
                } else {
                    alert(message);
                }
            } catch (error) {
                console.error("Error deleting account:", error);
            }
        }

        // Handle logo upload
        document.getElementById('logo-upload').addEventListener('change', function(e) {
            const file = e.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = async function(event) {
                    // Save to Firebase
                    await firebase.database().ref('logo').set(event.target.result);
                    document.getElementById('home-logo').src = event.target.result;
                    document.getElementById('logo-file-name').textContent = file.name;
                };
                reader.readAsDataURL(file);
            }
        });

        // Initialize the app when DOM is loaded
        document.addEventListener('DOMContentLoaded', initializeApp);
    </script>
</body>
</html>
