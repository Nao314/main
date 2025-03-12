<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AIゲームポータル</title>
    <style>
        :root {
            --primary-color: #6200ea;
            --secondary-color: #03dac6;
            --bg-color: #121212;
            --text-color: #ffffff;
            --card-bg: #1e1e1e;
            --hover-color: #bb86fc;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: var(--bg-color);
            color: var(--text-color);
            line-height: 1.6;
            background-image: 
                radial-gradient(circle at 10% 20%, rgba(98, 0, 234, 0.1) 0%, transparent 20%),
                radial-gradient(circle at 90% 60%, rgba(3, 218, 198, 0.1) 0%, transparent 20%);
            min-height: 100vh;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px;
        }
        
        header {
            padding: 2rem 0;
            text-align: center;
            position: relative;
            overflow: hidden;
        }
        
        .header-content {
            position: relative;
            z-index: 2;
        }
        
        .header-bg {
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: linear-gradient(45deg, var(--primary-color), var(--secondary-color));
            opacity: 0.1;
            transform: rotate(-10deg);
            z-index: 1;
        }
        
        h1 {
            font-size: 3.5rem;
            margin-bottom: 1rem;
            background: linear-gradient(90deg, var(--primary-color), var(--secondary-color));
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            text-shadow: 0 0 10px rgba(98, 0, 234, 0.3);
        }
        
        .subtitle {
            font-size: 1.5rem;
            margin-bottom: 2rem;
            opacity: 0.9;
        }
        
        .games-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 2rem;
            margin: 3rem 0;
        }
        
        .game-card {
            background-color: var(--card-bg);
            border-radius: 15px;
            overflow: hidden;
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
            display: flex;
            flex-direction: column;
        }
        
        .game-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 15px 30px rgba(98, 0, 234, 0.3);
        }
        
        .game-image {
            height: 200px;
            background-size: cover;
            background-position: center;
            position: relative;
        }
        
        .invader-image {
            background: linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)), url('/api/placeholder/400/320') center/cover;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        
        .tower-image {
            background: linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)), url('/api/placeholder/400/320') center/cover;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        
        /* 競馬ゲーム用の画像。Unsplashの競馬関連イメージを利用 */
        .horse-image {
            background: linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)), url('https://source.unsplash.com/400x320/?horse,racing') center/cover;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        
        .game-content {
            padding: 1.5rem;
            flex-grow: 1;
            display: flex;
            flex-direction: column;
        }
        
        h2 {
            font-size: 1.8rem;
            margin-bottom: 1rem;
            color: var(--secondary-color);
        }
        
        .game-description {
            margin-bottom: 1.5rem;
            flex-grow: 1;
        }
        
        .play-button {
            display: inline-block;
            background: linear-gradient(45deg, var(--primary-color), #9d4edd);
            color: white;
            padding: 0.8rem 1.5rem;
            border-radius: 30px;
            text-decoration: none;
            font-weight: bold;
            text-align: center;
            transition: transform 0.2s, box-shadow 0.2s;
            border: none;
            cursor: pointer;
            font-size: 1.1rem;
            box-shadow: 0 4px 10px rgba(98, 0, 234, 0.3);
        }
        
        .play-button:hover {
            transform: scale(1.05);
            box-shadow: 0 7px 15px rgba(98, 0, 234, 0.5);
        }
        
        .play-button:active {
            transform: scale(0.98);
        }
        
        .game-icon {
            font-size: 4rem;
            color: var(--text-color);
            text-shadow: 0 0 10px var(--primary-color);
        }
        
        footer {
            text-align: center;
            padding: 2rem 0;
            margin-top: 3rem;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .pixel-art {
            font-family: monospace;
            color: var(--secondary-color);
            font-size: 1rem;
            white-space: pre;
            line-height: 1.2;
            text-shadow: 0 0 5px var(--secondary-color);
        }
        
        .floating {
            animation: floating 3s ease-in-out infinite;
        }
        
        @keyframes floating {
            0% { transform: translateY(0px); }
            50% { transform: translateY(-15px); }
            100% { transform: translateY(0px); }
        }
        
        .glow {
            animation: glow 2s ease-in-out infinite alternate;
        }
        
        @keyframes glow {
            from { text-shadow: 0 0 5px var(--secondary-color); }
            to { text-shadow: 0 0 15px var(--hover-color), 0 0 20px var(--primary-color); }
        }
        
        @media (max-width: 768px) {
            h1 {
                font-size: 2.5rem;
            }
            
            .subtitle {
                font-size: 1.2rem;
            }
            
            .games-grid {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <div class="header-bg"></div>
            <div class="header-content">
                <h1 class="glow">AIゲームポータル</h1>
                <p class="subtitle">AIに作ってもらったゲームが置いてあります</p>
            </div>
        </header>
        
        <main>
            <div class="games-grid">
                <div class="game-card">
                    <div class="game-image invader-image">
                        <div class="pixel-art floating">
 ███
█████
███████
█ █   █ █
                        </div>
                    </div>
                    <div class="game-content">
                        <h2>インベーダーゲーム</h2>
                        <p class="game-description">
                            普通っぽいインベーダーゲームです
                        </p>
                        <a href="https://nao314.github.io/Invader" class="play-button">今すぐプレイ</a>
                    </div>
                </div>
                
                <div class="game-card">
                    <div class="game-image tower-image">
                        <div class="pixel-art floating">
╱┃╲
╱ ┃ ╲
╱__┃__╲
   ┃
 ▀███▀
                        </div>
                    </div>
                    <div class="game-content">
                        <h2>タワーディフェンス</h2>
                        <p class="game-description">
                            割と普通のタワーディフェンス
                        </p>
                        <a href="https://nao314.github.io/tower" class="play-button">今すぐプレイ</a>
                    </div>
                </div>
                
                <!-- 競馬ゲームのカード追加 -->
                <div class="game-card">
                    <div class="game-image horse-image">
                        <div class="pixel-art floating">
   __/| 
  /  o\____
 /       o )
|  o       |
 \________/
                        </div>
                    </div>
                    <div class="game-content">
                        <h2>競馬ゲーム</h2>
                        <p class="game-description">
                            見るだけ競馬ゲーム（？）
                        </p>
                        <a href="https://nao314.github.io/keiba/" class="play-button">今すぐプレイ</a>
                    </div>
                </div>
            </div>
        </main>
        
        <footer>
            <p>© 2025 AIゲームポータル　</p>
        </footer>
    </div>
</body>
</html>
