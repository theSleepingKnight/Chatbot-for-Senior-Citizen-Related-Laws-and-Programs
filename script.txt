document.addEventListener('DOMContentLoaded', () => {

    const chatWindow = document.getElementById('chat-window');
    const chatToggle = document.getElementById('chat-toggle');
    const chatMessages = document.getElementById('chat-messages');
    const chatInput = document.getElementById('chat-input');
    const sendBtn = document.getElementById('send-btn');
    const closeChatBtn = document.getElementById('close-chat');

    // --- Event Listeners ---

    // Toggle chat window open/closed
    chatToggle.addEventListener('click', () => {
        chatWindow.classList.toggle('hidden');
        chatToggle.classList.toggle('chat-open');
        if (!chatWindow.classList.contains('hidden')) {
            chatInput.focus();
        }
    });

    // Close chat window
    closeChatBtn.addEventListener('click', () => {
        chatWindow.classList.add('hidden');
        chatToggle.classList.remove('chat-open');
    });

    // Send message on button click
    sendBtn.addEventListener('click', sendMessage);

    // Send message on 'Enter' key press
    chatInput.addEventListener('keydown', (event) => {
        if (event.key === 'Enter') {
            event.preventDefault(); 
            sendMessage();
        }
    });

    // --- Main Functions ---

    /**
     * Handles the user sending a message.
     */
    function sendMessage() {
        const messageText = chatInput.value.trim();
        if (messageText === '') return; 

        addMessage(messageText, 'user');
        chatInput.value = '';

        // Show typing indicator
        showTypingIndicator();

        // Simulate bot "thinking" and get response
        setTimeout(() => {
            const botReplyText = getBotResponse(messageText);
            hideTypingIndicator();
            sendBotResponse(botReplyText); // New function to handle replies
        }, 1500 + Math.random() * 500); // Simulate 1.5 - 2s thinking time
    }

    /**
     * NEW: Handles sending the bot's response.
     * Splits messages that contain "|" into multiple bubbles.
     * @param {string} text - The full response text from the knowledge base.
     */
    function sendBotResponse(text) {
        // Split the text by the "|" character
        const messages = text.split('|');
        
        // Send each message with a delay
        messages.forEach((msg, index) => {
            setTimeout(() => {
                addMessage(msg, 'bot');
            }, index * 900); // Send each bubble 0.9s after the last
        });
    }

    /**
     * Creates a new message element (user, bot, or typing) and adds it to the chat.
     * @param {string} text - The content of the message.
     * @param {string} type - 'user', 'bot', or 'typing-indicator'.
     */
    function addMessage(text, type) {
        const messageElement = document.createElement('div');
        messageElement.classList.add('message', type);

        if (type === 'typing-indicator') {
            messageElement.innerHTML = "<span></span><span></span><span></span>";
        } else {
            messageElement.textContent = text;
        }
        
        chatMessages.appendChild(messageElement);
        scrollToBottom();
    }

    /**
     * NEW: Shows the "Lola Yan is typing..." bubble.
     */
    function showTypingIndicator() {
        addMessage('', 'typing-indicator');
    }

    /**
     * NEW: Hides the "Lola Yan is typing..." bubble.
     */
    function hideTypingIndicator() {
        const typingIndicator = chatMessages.querySelector('.typing-indicator');
        if (typingIndicator) {
            typingIndicator.remove();
        }
    }

    /**
     * Utility to scroll the chat to the newest message.
     */
    function scrollToBottom() {
        chatMessages.scrollTop = chatMessages.scrollHeight;
    }

    /**
* The "brain" of the bot. Searches KNOWLEDGE_BASE.
     * (This function is unchanged from the previous step)
     */
    function getBotResponse(userInput) {
        const input = userInput.toLowerCase();
        let bestMatch = null;
        let highestScore = 0;

        for (const entry of KNOWLEDGE_BASE) {
            let currentScore = 0;
            for (const keyword of entry.keywords) {
                if (input.includes(keyword.toLowerCase())) {
                    currentScore++;
                }
            }
            if (currentScore > highestScore) {
                highestScore = currentScore;
                bestMatch = entry;
            }
        }

        return bestMatch ? bestMatch.answer : DEFAULT_ANSWER;
    }
});