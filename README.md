<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Aplikasi Chatting</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f0f0f0;
            color: #333;
            display: flex;
            height: 100vh;
        }
        .container {
            display: flex;
            width: 100%;
        }
        .contacts {
            width: 300px;
            background-color: #fff;
            border-right: 1px solid #ddd;
            overflow-y: auto;
        }
        .chat {
            flex: 1;
            display: flex;
            flex-direction: column;
            background-color: #fff;
        }
        .chat-header {
            padding: 10px;
            border-bottom: 1px solid #ddd;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .chat-messages {
            flex: 1;
            padding: 10px;
            overflow-y: auto;
            display: flex;
            flex-direction: column;
        }
        .message {
            margin: 5px 0;
            padding: 10px;
            border-radius: 5px;
            max-width: 70%;
        }
        .message.sent {
            background-color: #dcf8c6;
            align-self: flex-end;
        }
        .message.received {
            background-color: #fff;
            align-self: flex-start;
        }
        .input-area {
            padding: 10px;
            border-top: 1px solid #ddd;
            display: flex;
            align-items: center;
        }
        .input-area input {
            flex: 1;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 5px;
            margin-right: 10px;
        }
        .input-area button {
            padding: 10px;
            border: none;
            background-color: #007bff;
            color: white;
            border-radius: 5px;
            cursor: pointer;
        }
        .input-area button:disabled {
            background-color: #ccc;
        }
        .typing-indicator {
            font-size: 0.9em;
            color: #999;
            margin: 5px 0;
        }
        .dark-mode {
            background-color: #333;
            color: #fff;
        }
        .dark-mode .contacts, .dark-mode .chat {
            background-color: #444;
            border-color: #555;
        }
        .dark-mode .message.sent {
            background-color: #555;
        }
        .dark-mode .message.received {
            background-color: #666;
        }
        @media (max-width: 600px) {
            .contacts {
                display: none;
            }
            .chat {
                width: 100%;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="contacts" id="contacts">
            <h3>Kontak</h3>
            <ul id="contact-list">
                <li onclick="selectContact('John Doe')">John Doe</li>
                <li onclick="selectContact('Jane Smith')">Jane Smith</li>
                <li onclick="selectContact('Alice Johnson')">Alice Johnson</li>
            </ul>
        </div>
        <div class="chat" id="chat">
            <div class="chat-header">
                <h3 id="chat-title">Pilih Kontak</h3>
            </div>
            <div class="chat-messages" id="chat-messages"></div>
            <div class="typing-indicator" id="typing-indicator" style="display: none;"></div>
            <div class="input-area">
                <input type="text" id="message-input" placeholder="Ketik pesan..." oninput="typing()" />
                <input type="file" id="file-input" accept="image/*" style="display: none;" onchange="sendFile()" />
                <button onclick="sendMessage()">Kirim</button>
                <button onclick="document.getElementById('file-input').click()">📎</button>
            </div>
        </div>
    </div>

    <script>
       
