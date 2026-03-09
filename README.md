<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>AI Chat Tool</title>
<style>
body {
    margin:0;
    font-family: 'Courier New', monospace;
    background-color: #0d0d0d;
    color: #00ff00;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
}
.container {
    width: 90%;
    max-width: 700px;
    background: #111;
    border: 2px solid #00ff00;
    border-radius: 10px;
    display: flex;
    flex-direction: column;
    overflow: hidden;
    box-shadow: 0 0 20px #00ff00;
}
header {
    background: #000;
    padding: 10px;
    text-align: center;
    font-weight: bold;
    font-size: 1.5rem;
    border-bottom: 1px solid #00ff00;
}
.chat-window {
    flex: 1;
    padding: 10px;
    overflow-y: auto;
}
.chat-msg {
    margin: 5px 0;
}
.user { color: #0ff; }
.ai { color: #0f0; }
input, button {
    padding: 10px;
    margin: 5px;
    border-radius: 5px;
    border: 2px solid #00ff00;
    background: #000;
    color: #0f0;
}
input { flex: 1; }
#inputContainer { display: flex; border-top: 1px solid #00ff00; }
button:hover { cursor: pointer; background: #0f0; color: #000; }
</style>
</head>
<body>
<div class="container">
<header>AI Chat Tool</header>
<div id="chatWindow" class="chat-window"></div>
<div id="inputContainer">
<input type="text" id="userInput" placeholder="Type your message here">
<button onclick="sendMessage()">Send</button>
<button onclick="downloadChat()">Download</button>
</div>
</div>

<script>
const chatWindow = document.getElementById('chatWindow');

function addMessage(sender, text) {
    const msg = document.createElement('div');
    msg.classList.add('chat-msg', sender);
    msg.innerText = text;
    chatWindow.appendChild(msg);
    chatWindow.scrollTop = chatWindow.scrollHeight;
}

async function sendMessage() {
    const input = document.getElementById('userInput');
    const userText = input.value.trim();
    if(!userText) return;
    addMessage('user', 'You: ' + userText);
    input.value = '';

    // Show AI "thinking" effect
    addMessage('ai', 'AI: ...');

    // Example AI API call placeholder (replace with real API)
    setTimeout(() => {
        chatWindow.lastChild.innerText = 'AI: ' + 'This is a sample AI response for "' + userText + '"';
    }, 1000);
}

// Download chat log
function downloadChat() {
    let chatText = '';
    document.querySelectorAll('.chat-msg').forEach(msg => {
        chatText += msg.innerText + '\n';
    });
    const blob = new Blob([chatText], {type: "text/plain"});
    const link = document.createElement('a');
    link.href = URL.createObjectURL(blob);
    link.download = "chat_log.txt";
    link.click();
}
</script>
</body>
</html>
