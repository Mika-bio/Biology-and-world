<!DOCTYPE html>
<html lang="kk">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BioExplorer 7 - Webhook Орнату</title>
    <link rel="stylesheet" href="../style.css">
    <style>
        .webhook-container {
            max-width: 900px;
            margin: 2rem auto;
            padding: 2rem;
            background: white;
            border-radius: 15px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.1);
        }
        
        .webhook-card {
            border: 1px solid #ddd;
            border-radius: 10px;
            padding: 1.5rem;
            margin: 1rem 0;
            background: #f9f9f9;
        }
        
        .url-display {
            background: #2E7D32;
            color: white;
            padding: 1rem;
            border-radius: 5px;
            font-family: monospace;
            word-break: break-all;
            margin: 1rem 0;
        }
        
        .copy-btn {
            background: #4CAF50;
            color: white;
            border: none;
            padding: 0.5rem 1rem;
            border-radius: 5px;
            cursor: pointer;
            margin-left: 1rem;
        }
        
        .test-btn {
            background: #2196F3;
            color: white;
            border: none;
            padding: 0.5rem 1rem;
            border-radius: 5px;
            cursor: pointer;
            margin-left: 1rem;
        }
        
        .logs-container {
            background: #333;
            color: #0f0;
            padding: 1rem;
            border-radius: 5px;
            font-family: monospace;
            height: 300px;
            overflow-y: auto;
            margin: 1rem 0;
        }
        
        .secret-input {
            width: 100%;
            padding: 0.5rem;
            margin: 0.5rem 0;
            border: 1px solid #ddd;
            border-radius: 5px;
        }
        
        .platform-icons {
            font-size: 2rem;
            margin-right: 1rem;
        }
    </style>
</head>
<body>
    <!-- Навигация -->
    <nav class="navbar">
        <div class="nav-container">
            <a href="../index.html" class="logo">
                <i class="fas fa-leaf"></i>
                BioExplorer 7
            </a>
        </div>
    </nav>

    <!-- Негізгі контент -->
    <div class="webhook-container">
        <h1><i class="fas fa-link"></i> Webhook URL Орнату</h1>
        <p class="subtitle">Қосымшаны басқа қызметтермен байланыстыру</p>
        
        <!-- GitHub Webhook -->
        <div class="webhook-card">
            <h3><i class="fab fa-github platform-icons"></i> GitHub Webhook</h3>
            <p>GitHub-тағы өзгерістерді қадағалау үшін</p>
            
            <div class="url-display" id="github-webhook-url">
                https://[username].github.io/bioexplorer-7/webhook/github
            </div>
            
            <button class="copy-btn" onclick="copyToClipboard('github-webhook-url')">
                <i class="fas fa-copy"></i> Көшіру
            </button>
            <button class="test-btn" onclick="testWebhook('github')">
                <i class="fas fa-play"></i> Тестілеу
            </button>
            
            <h4>GitHub-та орнату:</h4>
            <ol>
                <li>GitHub репозиторийінде Settings → Webhooks өтіңіз</li>
                <li>"Add webhook" басыңыз</li>
                <li>Жоғарыдағы URL-ді қойыңыз</li>
                <li>Content type: "application/json" таңдаңыз</li>
                <li>Secret кодын енгізіңіз: <input type="text" class="secret-input" id="github-secret" placeholder="secret_key_123"></li>
                <li>"Add webhook" басыңыз</li>
            </ol>
        </div>
        
        <!-- Discord Webhook -->
        <div class="webhook-card">
            <h3><i class="fab fa-discord platform-icons"></i> Discord Webhook</h3>
            <p>Discord каналына хабарламалар жіберу үшін</p>
            
            <div class="url-display" id="discord-webhook-url">
                https://[username].github.io/bioexplorer-7/webhook/discord
            </div>
            
            <button class="copy-btn" onclick="copyToClipboard('discord-webhook-url')">
                <i class="fas fa-copy"></i> Көшіру
            </button>
            <button class="test-btn" onclick="testWebhook('discord')">
                <i class="fas fa-play"></i> Тестілеу
            </button>
            
            <h4>Discord-та орнату:</h4>
            <ol>
                <li>Discord серверінде каналды ашыңыз</li>
                <li>Канал настройкалары → Integrations → Webhooks</li>
                <li>"New Webhook" басыңыз</li>
                <li>Жоғарыдағы URL-ді қойыңыз</li>
            </ol>
        </div>
        
        <!-- Telegram Webhook -->
        <div class="webhook-card">
            <h3><i class="fab fa-telegram platform-icons"></i> Telegram Webhook</h3>
            <p>Telegram ботпен жұмыс істеу үшін</p>
            
            <div class="url-display" id="telegram-webhook-url">
                https://[username].github.io/bioexplorer-7/webhook/telegram
            </div>
            
            <button class="copy-btn" onclick="copyToClipboard('telegram-webhook-url')">
                <i class="fas fa-copy"></i> Көшіру
            </button>
            <button class="test-btn" onclick="testWebhook('telegram')">
                <i class="fas fa-play"></i> Тестілеу
            </button>
            
            <h4>Telegram Bot орнату:</h4>
            <ol>
                <li>@BotFather-ге хабарласыңыз</li>
                <li>Жаңа бот жасаңыз</li>
                <li>Бот токенін алыңыз</li>
                <li>API арқылы webhook орнатыңыз</li>
            </ol>
        </div>
        
        <!-- Webhook логтары -->
        <div class="webhook-card">
            <h3><i class="fas fa-history"></i> Webhook Логтары</h3>
            <p>Соңғы webhook шақырулары:</p>
            
            <div class="logs-container" id="webhook-logs">
                [Журнал осында пайда болады]
            </div>
            
            <button class="test-btn" onclick="clearLogs()">
                <i class="fas fa-trash"></i> Логтарды тазарту
            </button>
        </div>
        
        <!-- Тест деректері -->
        <div class="webhook-card">
            <h3><i class="fas fa-vial"></i> Webhook Тестілеу</h3>
            
            <textarea id="test-payload" rows="6" style="width: 100%;" placeholder='{
  "action": "test",
  "message": "Тест хабарламасы",
  "timestamp": "2024-01-15T10:30:00Z"
}'>{
  "action": "test",
  "message": "Тест хабарламасы",
  "timestamp": "2024-01-15T10:30:00Z"
}</textarea>
            
            <button class="test-btn" onclick="sendTestWebhook()">
                <i class="fas fa-paper-plane"></i> Webhook жіберу
            </button>
        </div>
    </div>

    <script src="../script.js"></script>
    <script>
        // Webhook логтары
        let webhookLogs = [];
        
        // URL көшіру
        function copyToClipboard(elementId) {
            const text = document.getElementById(elementId).textContent;
            navigator.clipboard.writeText(text).then(() => {
                alert('URL көшірілді!');
            });
        }
        
        // Webhook тестілеу
        function testWebhook(platform) {
            const payloads = {
                github: {
                    action: "test",
                    repository: {
                        name: "bioexplorer-7",
                        full_name: "[username]/bioexplorer-7"
                    },
                    sender: {
                        login: "testuser"
                    }
                },
                discord: {
                    content: "Тест хабарламасы BioExplorer 7-ден",
                    username: "BioExplorer Bot",
                    embeds: [{
                        title: "Тестілеу",
                        description: "Бұл тест webhook хабарламасы",
                        color: 0x2E7D32
                    }]
                },
                telegram: {
                    update_id: 123456,
                    message: {
                       
