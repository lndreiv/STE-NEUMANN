
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>STE NEUMANN ANONYMOUS MESSAGE BOX</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap');
        
        body {
            font-family: 'Poppins', sans-serif;
            background: linear-gradient(135deg, #ff416c 0%, #ff4b2b 100%);
            min-height: 100vh;
        }
        
        .message-card {
            transition: all 0.3s ease;
        }
        
        .message-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(0,0,0,0.2);
        }
        
        .image-preview {
            max-height: 200px;
            object-fit: contain;
        }
        
        .custom-file-upload {
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .custom-file-upload:hover {
            background-color: #e02d1b;
        }
        
        .notification-badge {
            animation: pulse 2s infinite;
        }
        
        @keyframes pulse {
            0% {
                transform: scale(0.95);
                box-shadow: 0 0 0 0 rgba(255, 255, 255, 0.7);
            }
            
            70% {
                transform: scale(1);
                box-shadow: 0 0 0 10px rgba(255, 255, 255, 0);
            }
            
            100% {
                transform: scale(0.95);
                box-shadow: 0 0 0 0 rgba(255, 255, 255, 0);
            }
        }
        
        .admin-access {
            opacity: 0.05;
            transition: opacity 0.3s ease;
        }
        
        .admin-access:hover {
            opacity: 0.3;
        }
        
        .gradient-button {
            background: linear-gradient(135deg, #ff416c 0%, #ff4b2b 100%);
            transition: all 0.3s ease;
        }
        
        .gradient-button:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(255, 75, 43, 0.4);
        }
        
        .card-shadow {
            box-shadow: 0 10px 30px rgba(255, 75, 43, 0.2);
        }
        
        .header-text-shadow {
            text-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
        }
    </style>
</head>
<body class="p-4">
    <div id="landing-page" class="container mx-auto max-w-4xl">
        <!-- Header -->
        <header class="text-center py-8">
            <h1 class="text-4xl font-bold text-white mb-2 header-text-shadow">STE NEUMANN ANONYMOUS MESSAGE BOX</h1>
            <p class="text-white text-opacity-80">Share your thoughts anonymously</p>
        </header>
        
        <!-- Main Content -->
        <div class="bg-white rounded-xl shadow-xl overflow-hidden card-shadow">
            <div class="p-6">
                <div class="mb-6">
                    <label for="message" class="block text-sm font-medium text-gray-700 mb-2">Your Message</label>
                    <textarea id="message" rows="6" class="w-full px-4 py-3 rounded-lg border border-gray-300 focus:outline-none focus:ring-2 focus:ring-red-500 resize-none" placeholder="Type your anonymous message here..."></textarea>
                </div>
                
                <div class="mb-6">
                    <div class="flex items-center space-x-4">
                        <label class="custom-file-upload flex items-center px-4 py-2 gradient-button text-white rounded-lg transition">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-6-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z" />
                            </svg>
                            Add Image
                            <input type="file" id="image-upload" accept="image/*" class="hidden" />
                        </label>
                        <span id="file-name" class="text-sm text-gray-500"></span>
                    </div>
                    <div id="image-preview-container" class="mt-4 hidden">
                        <img id="image-preview" class="image-preview rounded-lg border border-gray-200" src="" alt="Preview">
                        <button id="remove-image" class="mt-2 text-sm text-red-500 hover:text-red-700">Remove image</button>
                    </div>
                </div>
                
                <button id="send-button" class="w-full gradient-button text-white py-3 px-6 rounded-lg font-medium transition flex items-center justify-center">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 19l9 2-9-18-9 18 9-2zm0 0v-8" />
                    </svg>
                    Send Message
                </button>
            </div>
        </div>
        
        <!-- Footer with Hidden Admin Access -->
        <footer class="text-center mt-8 text-white text-opacity-70 text-sm">
            <p>All messages are stored securely.</p>
            <div class="mt-8 admin-access">
                <button id="admin-access-btn" class="text-white text-opacity-50 text-xs">Admin Access</button>
            </div>
        </footer>
    </div>
    
    <!-- Admin Page -->
    <div id="admin-page" class="container mx-auto max-w-4xl hidden">
        <!-- Header -->
        <header class="text-center py-8">
            <h1 class="text-4xl font-bold text-white mb-2 header-text-shadow">STE NEUMANN ANONYMOUS MESSAGE BOX</h1>
            <p class="text-white text-opacity-80">Admin Portal</p>
        </header>
        
        <!-- Main Content -->
        <div class="bg-white rounded-xl shadow-xl overflow-hidden card-shadow">
            <div class="p-6">
                <div class="flex justify-between items-center mb-6">
                    <h2 class="text-xl font-semibold text-gray-800">Your Messages</h2>
                    <div class="flex space-x-4">
                        <button id="refresh-messages" class="text-sm text-red-600 hover:text-red-800">Refresh</button>
                        <button id="mark-all-read" class="text-sm text-red-600 hover:text-red-800">Mark all as read</button>
                        <button id="back-to-home" class="text-red-600 hover:text-red-800 flex items-center">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 19l-7-7m0 0l7-7m-7 7h18" />
                            </svg>
                            Back
                        </button>
                    </div>
                </div>
                
                <div id="messages-container" class="space-y-4">
                    <div class="text-center text-gray-500 py-8">
                        No messages yet. When people send you messages, they'll appear here.
                    </div>
                </div>
            </div>
        </div>
        
        <!-- Admin Controls -->
        <div class="bg-white rounded-xl shadow-xl overflow-hidden mt-6 p-6 card-shadow">
            <h3 class="text-lg font-semibold text-gray-800 mb-4">Admin Controls</h3>
            <div class="flex flex-wrap gap-4">
                <button id="clear-all-messages" class="px-4 py-2 bg-red-600 text-white rounded-lg hover:bg-red-700 transition">
                    Clear All Messages
                </button>
                <button id="export-messages" class="px-4 py-2 gradient-button text-white rounded-lg transition">
                    Export Messages
                </button>
                <button id="debug-messages" class="px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition">
                    Debug Messages
                </button>
            </div>
        </div>
    </div>
    
    <!-- Success Modal -->
    <div id="success-modal" class="fixed inset-0 flex items-center justify-center z-50 bg-black bg-opacity-50 hidden">
        <div class="bg-white rounded-xl p-6 max-w-md w-full mx-4 shadow-2xl">
            <div class="text-center">
                <div class="mx-auto flex items-center justify-center h-12 w-12 rounded-full bg-green-100 mb-4">
                    <svg class="h-8 w-8 text-green-500" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path>
                    </svg>
                </div>
                <h3 class="text-lg font-medium text-gray-900 mb-2">Message Sent!</h3>
                <p class="text-gray-600 mb-6">Your anonymous message has been delivered successfully.</p>
                <button id="close-modal" class="w-full gradient-button text-white py-2 px-4 rounded-lg font-medium transition">
                    Close
                </button>
            </div>
        </div>
    </div>
    
    <!-- Admin Password Modal -->
    <div id="password-modal" class="fixed inset-0 flex items-center justify-center z-50 bg-black bg-opacity-50 hidden">
        <div class="bg-white rounded-xl p-6 max-w-md w-full mx-4 shadow-2xl">
            <div class="text-center">
                <div class="mx-auto flex items-center justify-center h-12 w-12 rounded-full bg-red-100 mb-4">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8 text-red-500" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z" />
                    </svg>
                </div>
                <h3 class="text-lg font-medium text-gray-900 mb-2">Admin Access</h3>
                <p class="text-gray-600 mb-4">Enter your admin password to continue.</p>
                <input type="password" id="admin-password" class="w-full px-4 py-2 rounded-lg border border-gray-300 focus:outline-none focus:ring-2 focus:ring-red-500 mb-4" placeholder="Password">
                <div class="flex space-x-4">
                    <button id="cancel-password" class="flex-1 bg-gray-200 text-gray-800 py-2 px-4 rounded-lg font-medium hover:bg-gray-300 transition">
                        Cancel
                    </button>
                    <button id="submit-password" class="flex-1 gradient-button text-white py-2 px-4 rounded-lg font-medium transition">
                        Login
                    </button>
                </div>
            </div>
        </div>
    </div>
    
    <!-- Debug Modal -->
    <div id="debug-modal" class="fixed inset-0 flex items-center justify-center z-50 bg-black bg-opacity-50 hidden">
        <div class="bg-white rounded-xl p-6 max-w-4xl w-full mx-4 shadow-2xl max-h-[80vh] overflow-auto">
            <div class="text-left">
                <h3 class="text-lg font-medium text-gray-900 mb-2">Debug Information</h3>
                <pre id="debug-content" class="bg-gray-100 p-4 rounded-lg overflow-auto max-h-[60vh] text-xs"></pre>
                <div class="mt-4 flex justify-end">
                    <button id="close-debug" class="gradient-button text-white py-2 px-4 rounded-lg font-medium transition">
                        Close
                    </button>
                </div>
            </div>
        </div>
    </div>
    
    <script>
        // DOM Elements - Pages
        const landingPage = document.getElementById('landing-page');
        const adminPage = document.getElementById('admin-page');
        
        // DOM Elements - Landing Page
        const messageInput = document.getElementById('message');
        const imageUpload = document.getElementById('image-upload');
        const fileName = document.getElementById('file-name');
        const imagePreviewContainer = document.getElementById('image-preview-container');
        const imagePreview = document.getElementById('image-preview');
        const removeImageBtn = document.getElementById('remove-image');
        const sendButton = document.getElementById('send-button');
        const adminAccessBtn = document.getElementById('admin-access-btn');
        
        // DOM Elements - Admin Page
        const messagesContainer = document.getElementById('messages-container');
        const refreshMessagesBtn = document.getElementById('refresh-messages');
        const markAllReadBtn = document.getElementById('mark-all-read');
        const backToHome = document.getElementById('back-to-home');
        const clearAllMessagesBtn = document.getElementById('clear-all-messages');
        const exportMessagesBtn = document.getElementById('export-messages');
        const debugMessagesBtn = document.getElementById('debug-messages');
        
        // DOM Elements - Modals
        const successModal = document.getElementById('success-modal');
        const closeModalBtn = document.getElementById('close-modal');
        const passwordModal = document.getElementById('password-modal');
        const adminPassword = document.getElementById('admin-password');
        const submitPassword = document.getElementById('submit-password');
        const cancelPassword = document.getElementById('cancel-password');
        const debugModal = document.getElementById('debug-modal');
        const debugContent = document.getElementById('debug-content');
        const closeDebug = document.getElementById('close-debug');
        
        // Admin password - Change this to your desired password
        const ADMIN_PASSWORD = "admin123"; // You should change this!
        
        // Storage key constant
        const STORAGE_KEY = 'anonymousMessages';
        
        // Load messages from localStorage
        function loadMessages() {
            try {
                const storedMessages = localStorage.getItem(STORAGE_KEY);
                console.log("Raw stored messages:", storedMessages);
                
                if (storedMessages) {
                    const parsedMessages = JSON.parse(storedMessages);
                    console.log("Parsed messages:", parsedMessages);
                    return Array.isArray(parsedMessages) ? parsedMessages : [];
                }
            } catch (error) {
                console.error("Error loading messages:", error);
                // Try to recover by clearing the corrupted data
                localStorage.removeItem(STORAGE_KEY);
            }
            return [];
        }
        
        // Save messages to localStorage
        function saveMessages(messages) {
            try {
                const jsonString = JSON.stringify(messages);
                localStorage.setItem(STORAGE_KEY, jsonString);
                console.log("Messages saved successfully:", messages.length);
                return true;
            } catch (error) {
                console.error("Error saving messages:", error);
                
                // If the error is likely due to storage limits, try to save without images
                if (error.name === 'QuotaExceededError' || error.name === 'NS_ERROR_DOM_QUOTA_REACHED') {
                    try {
                        // Create a copy with smaller images or no images
                        const reducedMessages = messages.map(msg => {
                            // If message has an image, either remove it or reduce its size
                            if (msg.image) {
                                return {
                                    ...msg,
                                    image: null, // Remove image to save space
                                    hadImage: true // Flag that it had an image
                                };
                            }
                            return msg;
                        });
                        
                        localStorage.setItem(STORAGE_KEY, JSON.stringify(reducedMessages));
                        console.log("Saved messages without images due to storage limits");
                        return true;
                    } catch (innerError) {
                        console.error("Failed to save even with reduced data:", innerError);
                    }
                }
                return false;
            }
        }
        
        // State
        let messages = loadMessages();
        let unreadCount = messages.filter(msg => !msg.read).length;
        let currentImageData = null;
        
        // Navigation Functions
        function showAdminPage() {
            landingPage.classList.add('hidden');
            adminPage.classList.remove('hidden');
            renderMessages();
        }
        
        function showLandingPage() {
            adminPage.classList.add('hidden');
            landingPage.classList.remove('hidden');
        }
        
        // Event Listeners - Navigation
        adminAccessBtn.addEventListener('click', () => {
            passwordModal.classList.remove('hidden');
        });
        
        backToHome.addEventListener('click', showLandingPage);
        
        // Password handling
        submitPassword.addEventListener('click', () => {
            if (adminPassword.value === ADMIN_PASSWORD) {
                passwordModal.classList.add('hidden');
                adminPassword.value = '';
                showAdminPage();
            } else {
                alert('Incorrect password');
            }
        });
        
        // Allow Enter key to submit password
        adminPassword.addEventListener('keyup', (e) => {
            if (e.key === 'Enter') {
                submitPassword.click();
            }
        });
        
        cancelPassword.addEventListener('click', () => {
            passwordModal.classList.add('hidden');
            adminPassword.value = '';
        });
        
        // Image upload handling
        imageUpload.addEventListener('change', (e) => {
            const file = e.target.files[0];
            if (file) {
                fileName.textContent = file.name;
                
                // Check file size before processing
                if (file.size > 1024 * 1024) { // 1MB
                    alert('Warning: Large images may not save properly. Consider using a smaller image.');
                }
                
                const reader = new FileReader();
                reader.onload = (event) => {
                    currentImageData = event.target.result;
                    imagePreview.src = currentImageData;
                    imagePreviewContainer.classList.remove('hidden');
                };
                reader.readAsDataURL(file);
            }
        });
        
        removeImageBtn.addEventListener('click', () => {
            imageUpload.value = '';
            fileName.textContent = '';
            currentImageData = null;
            imagePreviewContainer.classList.add('hidden');
        });
        
        // Send message
        sendButton.addEventListener('click', () => {
            const messageText = messageInput.value.trim();
            
            if (!messageText && !currentImageData) {
                alert('Please enter a message or add an image.');
                return;
            }
            
            const newMessage = {
                id: Date.now(),
                text: messageText,
                image: currentImageData,
                timestamp: new Date().toISOString(),
                read: false
            };
            
            // Add to messages array
            messages.unshift(newMessage);
            const saved = saveMessages(messages);
            
            if (saved) {
                // Update unread count
                unreadCount++;
                
                // Reset form
                messageInput.value = '';
                imageUpload.value = '';
                fileName.textContent = '';
                currentImageData = null;
                imagePreviewContainer.classList.add('hidden');
                
                // Show success modal
                successModal.classList.remove('hidden');
            } else {
                alert('There was an error saving your message. The file might be too large.');
            }
        });
        
        closeModalBtn.addEventListener('click', () => {
            successModal.classList.add('hidden');
        });
        
        // Refresh messages
        refreshMessagesBtn.addEventListener('click', () => {
            messages = loadMessages();
            renderMessages();
        });
        
        // Mark all as read
        markAllReadBtn.addEventListener('click', () => {
            messages = messages.map(msg => ({...msg, read: true}));
            saveMessages(messages);
            unreadCount = 0;
            renderMessages();
        });
        
        // Clear all messages
        clearAllMessagesBtn.addEventListener('click', () => {
            if (confirm('Are you sure you want to delete all messages? This cannot be undone.')) {
                messages = [];
                saveMessages(messages);
                unreadCount = 0;
                renderMessages();
            }
        });
        
        // Export messages
        exportMessagesBtn.addEventListener('click', () => {
            const dataStr = JSON.stringify(messages, null, 2);
            const dataUri = 'data:application/json;charset=utf-8,'+ encodeURIComponent(dataStr);
            
            const exportFileDefaultName = 'anonymous-messages.json';
            
            const linkElement = document.createElement('a');
            linkElement.setAttribute('href', dataUri);
            linkElement.setAttribute('download', exportFileDefaultName);
            linkElement.click();
        });
        
        // Debug messages
        debugMessagesBtn.addEventListener('click', () => {
            const allLocalStorage = {};
            for (let i = 0; i < localStorage.length; i++) {
                const key = localStorage.key(i);
                try {
                    const value = localStorage.getItem(key);
                    allLocalStorage[key] = value.length > 100 ? 
                        value.substring(0, 100) + '... [truncated, total length: ' + value.length + ']' : 
                        value;
                } catch (e) {
                    allLocalStorage[key] = '[Error reading value]';
                }
            }
            
            const debugInfo = {
                messagesCount: messages.length,
                unreadCount: messages.filter(msg => !msg.read).length,
                localStorageAvailable: isLocalStorageAvailable(),
                localStorageSize: getLocalStorageSize(),
                localStorageKeys: Object.keys(localStorage),
                localStorageContents: allLocalStorage,
                anonymousMessagesRaw: localStorage.getItem(STORAGE_KEY) ? 
                    localStorage.getItem(STORAGE_KEY).substring(0, 100) + '... [truncated]' : 
                    'null or empty',
                messages: messages.map(msg => ({
                    ...msg,
                    image: msg.image ? '[Image data exists]' : null
                }))
            };
            
            debugContent.textContent = JSON.stringify(debugInfo, null, 2);
            debugModal.classList.remove('hidden');
        });
        
        closeDebug.addEventListener('click', () => {
            debugModal.classList.add('hidden');
        });
        
        // Check if localStorage is available
        function isLocalStorageAvailable() {
            try {
                const test = 'test';
                localStorage.setItem(test, test);
                localStorage.removeItem(test);
                return true;
            } catch(e) {
                return false;
            }
        }
        
        // Get localStorage size
        function getLocalStorageSize() {
            let total = 0;
            for (let key in localStorage) {
                if (localStorage.hasOwnProperty(key)) {
                    total += (localStorage[key].length * 2) / 1024 / 1024;
                }
            }
            return total.toFixed(2) + " MB / ~5MB limit";
        }
        
        // Render messages
        function renderMessages() {
            // Reload messages from localStorage to ensure we have the latest
            messages = loadMessages();
            
            if (messages.length === 0) {
                messagesContainer.innerHTML = `
                    <div class="text-center text-gray-500 py-8">
                        No messages yet. When people send you messages, they'll appear here.
                    </div>
                `;
                return;
            }
            
            messagesContainer.innerHTML = '';
            
            messages.forEach(message => {
                const messageCard = document.createElement('div');
                messageCard.className = `message-card bg-white border ${message.read ? 'border-gray-200' : 'border-red-300'} rounded-lg shadow-sm p-4 relative`;
                
                let messageContent = '';
                
                if (message.text) {
                    messageContent += `<p class="text-gray-700 mb-3">${message.text}</p>`;
                }
                
                if (message.image) {
                    messageContent += `
                        <div class="mt-3 mb-3">
                            <img src="${message.image}" alt="Attached image" class="rounded-lg max-h-48 max-w-full">
                        </div>
                    `;
                } else if (message.hadImage) {
                    messageContent += `
                        <div class="mt-3 mb-3 p-4 bg-gray-100 rounded-lg text-gray-500 text-center">
                            [Image was removed to save storage space]
                        </div>
                    `;
                }
                
                const date = new Date(message.timestamp);
                const formattedDate = date.toLocaleString();
                
                messageCard.innerHTML = `
                    ${!message.read ? '<div class="absolute top-4 right-4 h-3 w-3 bg-red-500 rounded-full"></div>' : ''}
                    ${messageContent}
                    <div class="flex justify-between items-center mt-2">
                        <span class="text-xs text-gray-500">${formattedDate}</span>
                        <button class="delete-btn text-red-500 hover:text-red-700" data-id="${message.id}">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16" />
                            </svg>
                        </button>
                    </div>
                `;
                
                messagesContainer.appendChild(messageCard);
                
                // Mark as read when viewed
                if (!message.read) {
                    message.read = true;
                }
            });
            
            // Save the updated read status
            saveMessages(messages);
            
            // Add delete functionality
            document.querySelectorAll('.delete-btn').forEach(btn => {
                btn.addEventListener('click', (e) => {
                    const id = parseInt(e.currentTarget.dataset.id);
                    messages = messages.filter(msg => msg.id !== id);
                    saveMessages(messages);
                    renderMessages();
                });
            });
        }
        
        // Keyboard shortcut for admin access (Ctrl+Shift+A)
        document.addEventListener('keydown', (e) => {
            if (e.ctrlKey && e.shiftKey && e.key === 'A') {
                passwordModal.classList.remove('hidden');
            }
        });
        
        // Initialize
        document.addEventListener('DOMContentLoaded', () => {
            console.log("Page loaded, messages count:", messages.length);
            
            // Check if localStorage is working
            if (!isLocalStorageAvailable()) {
                alert("Warning: Local storage is not available. Messages won't be saved between sessions.");
            }
            
            // Check if we're close to storage limits
            const storageSize = parseFloat(getLocalStorageSize());
            if (storageSize > 4) {
                alert("Warning: Local storage is almost full. Some messages may not save properly.");
            }
        });
    </script>
<script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'9649b0f9c6054ccb',t:'MTc1MzQyNTg5My4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
