<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>数字排毒神谕 | Digital Detox Oracle</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700&family=Noto+Sans+SC:wght@300;400;700&display=swap');

        :root {
            --neon-blue: #00f3ff;
            --neon-purple: #bc13fe;
            --neon-green: #0aff0a;
            --bg-dark: #050510;
        }

        body {
            background-color: var(--bg-dark);
            font-family: 'Noto Sans SC', sans-serif;
            overflow: hidden; /* Prevent scrolling, keep it app-like */
            color: white;
            height: 100vh;
            margin: 0;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        #canvas-bg {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 0;
        }

        .glass-panel {
            background: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(16px);
            -webkit-backdrop-filter: blur(16px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.37);
            z-index: 10;
            transition: all 0.5s ease;
        }

        .glitch-text {
            font-family: 'Orbitron', sans-serif;
            position: relative;
            color: white;
            text-shadow: 2px 2px var(--neon-purple), -2px -2px var(--neon-blue);
            animation: glitch-anim 2s infinite linear alternate-reverse;
        }

        @keyframes glitch-anim {
            0% { text-shadow: 2px 2px var(--neon-purple), -2px -2px var(--neon-blue); }
            25% { text-shadow: -2px 2px var(--neon-blue), 2px -2px var(--neon-purple); }
            50% { text-shadow: 2px -2px var(--neon-purple), -2px 2px var(--neon-blue); }
            75% { text-shadow: -2px -2px var(--neon-blue), 2px 2px var(--neon-purple); }
            100% { text-shadow: 2px 2px var(--neon-purple), -2px -2px var(--neon-blue); }
        }

        .btn-neon {
            background: transparent;
            border: 2px solid var(--neon-blue);
            color: var(--neon-blue);
            text-shadow: 0 0 5px var(--neon-blue);
            box-shadow: 0 0 5px var(--neon-blue), inset 0 0 5px var(--neon-blue);
            transition: 0.3s;
            position: relative;
            overflow: hidden;
        }

        .btn-neon:hover {
            background: var(--neon-blue);
            color: var(--bg-dark);
            box-shadow: 0 0 20px var(--neon-blue), inset 0 0 10px var(--neon-blue);
            transform: scale(1.05);
        }

        .btn-neon::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.4), transparent);
            transition: 0.5s;
        }

        .btn-neon:hover::before {
            left: 100%;
        }

        .card-reveal {
            animation: flipIn 0.8s cubic-bezier(0.175, 0.885, 0.32, 1.275) forwards;
            transform-style: preserve-3d;
        }

        @keyframes flipIn {
            from { opacity: 0; transform: rotateX(-90deg) translateZ(-50px); }
            to { opacity: 1; transform: rotateX(0) translateZ(0); }
        }

        .scan-line {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 4px;
            background: var(--neon-green);
            box-shadow: 0 0 10px var(--neon-green);
            animation: scan 1.5s ease-in-out infinite;
            opacity: 0;
        }

        @keyframes scan {
            0% { top: 0%; opacity: 0; }
            10% { opacity: 1; }
            90% { opacity: 1; }
            100% { top: 100%; opacity: 0; }
        }

        .breathing-circle {
            animation: breathe 4s infinite ease-in-out;
        }

        @keyframes breathe {
            0%, 100% { transform: scale(1); opacity: 0.3; }
            50% { transform: scale(1.2); opacity: 0.6; }
        }

        /* Utility specific for the detox mode */
        .detox-mode-active .glass-panel,
        .detox-mode-active h1,
        .detox-mode-active .particles {
            opacity: 0.1;
            filter: blur(5px);
            pointer-events: none;
        }
        
        .detox-overlay {
            opacity: 0;
            pointer-events: none;
            transition: opacity 1s ease;
        }

        .detox-mode-active .detox-overlay {
            opacity: 1;
            pointer-events: auto;
        }

    </style>
</head>
<body>

    <!-- Dynamic Background -->
    <canvas id="canvas-bg"></canvas>

    <!-- Main Container -->
    <div id="main-interface" class="relative z-20 w-full max-w-md p-6 mx-auto transition-all duration-500">
        
        <!-- Header -->
        <div class="text-center mb-8">
            <i class="fas fa-microchip text-4xl mb-4 text-cyan-400 opacity-80 animate-pulse"></i>
            <h1 class="text-4xl font-bold glitch-text mb-2 tracking-wider">OFFLINE<br>ORACLE</h1>
            <p class="text-gray-400 text-sm tracking-widest uppercase">脱离矩阵 · 回归现实</p>
        </div>

        <!-- Glass Panel Content -->
        <div class="glass-panel rounded-2xl p-8 relative overflow-hidden min-h-[400px] flex flex-col justify-center items-center">
            
            <!-- Scene 1: Initial State -->
            <div id="scene-intro" class="text-center w-full">
                <p class="text-gray-300 mb-8 leading-relaxed">
                    感觉被屏幕吞噬了？<br>
                    你的数字灵魂已经过载。<br>
                    <span class="text-cyan-300">点击下方，获取你的“现实处方”。</span>
                </p>
                <button onclick="startConsultation()" class="btn-neon w-full py-4 text-lg font-bold tracking-widest uppercase rounded-lg">
                    <i class="fas fa-search-location mr-2"></i> 接入现实接口
                </button>
            </div>

            <!-- Scene 2: Scanning/Loading -->
            <div id="scene-scan" class="hidden absolute inset-0 bg-black/80 flex flex-col items-center justify-center z-20">
                <div class="scan-line z-30"></div>
                <div class="w-16 h-16 border-4 border-cyan-500 border-t-transparent rounded-full animate-spin mb-4"></div>
                <p class="text-green-400 font-mono text-sm blinking-cursor">正在分析视网膜疲劳度...</p>
                <p class="text-green-400 font-mono text-sm mt-1 blinking-cursor" style="animation-delay: 0.5s">检测到社交媒体焦虑...</p>
                <p class="text-green-400 font-mono text-sm mt-1 blinking-cursor" style="animation-delay: 1s">正在生成物理世界连接...</p>
            </div>

            <!-- Scene 3: Result Card -->
            <div id="scene-result" class="hidden text-center w-full">
                <div class="mb-6">
                    <div class="text-6xl mb-4" id="result-icon">🌿</div>
                    <h2 class="text-2xl font-bold text-white mb-2" id="result-title">任务生成中...</h2>
                    <div class="h-1 w-20 bg-gradient-to-r from-purple-500 to-cyan-500 mx-auto rounded-full mb-4"></div>
                    <p class="text-gray-200 text-lg leading-relaxed font-light" id="result-desc">
                        ...
                    </p>
                </div>
                
                <div class="grid grid-cols-1 gap-3">
                    <button onclick="activateDetoxMode()" class="bg-gradient-to-r from-purple-600 to-indigo-600 hover:from-purple-500 hover:to-indigo-500 text-white py-3 rounded-lg shadow-lg transform transition active:scale-95 flex items-center justify-center">
                        <i class="fas fa-hourglass-start mr-2"></i> 开启5分钟专注模式
                    </button>
                    <button onclick="resetApp()" class="text-gray-400 hover:text-white text-sm py-2">
                        重新诊断
                    </button>
                </div>
            </div>

        </div>

        <div class="text-center mt-6 opacity-50 text-xs text-gray-500">
            SYSTEM VERSION 2.5.4 // DISCONNECT READY
        </div>
    </div>

    <!-- Detox Overlay (The "Offline" Experience) -->
    <div id="detox-overlay" class="detox-overlay fixed inset-0 z-50 bg-black flex flex-col items-center justify-center text-center p-6">
        <div class="absolute inset-0 bg-gradient-to-b from-blue-900/20 to-black pointer-events-none"></div>
        
        <div class="w-64 h-64 rounded-full border border-gray-800 flex items-center justify-center relative mb-8">
            <div class="absolute inset-0 rounded-full bg-cyan-500 blur-2xl opacity-10 breathing-circle"></div>
            <div class="text-6xl font-thin text-gray-100 font-mono" id="timer-display">05:00</div>
        </div>

        <h2 class="text-2xl text-cyan-100 font-light mb-4">放下手机</h2>
        <p class="text-gray-400 max-w-xs mx-auto mb-12" id="detox-instruction">
            现在，去执行你的任务。<br>不要操作屏幕，直到倒计时结束。
        </p>

        <button onclick="exitDetoxMode()" class="border border-gray-700 text-gray-500 hover:text-white hover:border-white px-6 py-2 rounded-full text-sm transition-colors">
            我放弃，我要回数字世界
        </button>
    </div>

    <script>
        // --- Database of "Real World" Tasks ---
        const prescriptions = [
            {
                icon: "☁️",
                title: "云端漫步",
                desc: "走到阳台或窗边，寻找一朵形状最奇怪的云。盯着它看直到它变形或消失。不要拍照，只用眼睛记录。"
            },
            {
                icon: "💧",
                title: "水的形态",
                desc: "去喝一杯水。不是匆忙灌下，而是感受水流过喉咙的温度和触感。数着你的吞咽动作，数到十。"
            },
            {
                icon: "📖",
                title: "纸质触感",
                desc: "拿起离你最近的一本纸质书或杂志。翻到第 42 页，阅读第一段话。用手指感受纸张的纹理。"
            },
            {
                icon: "🖊️",
                title: "神经连接",
                desc: "找一支笔和一张纸。不要思考，随意在纸上画圆圈或线条，持续一分钟。感受笔尖与纸面的摩擦。"
            },
            {
                icon: "👂",
                title: "声波捕获",
                desc: "闭上眼睛，只用听觉。试着捕捉房间里最微小的三种声音（电流声？风声？远处的车声？）。"
            },
            {
                icon: "🧘",
                title: "物理扫描",
                desc: "坐在椅子上，从脚趾开始，感受身体每一个部分接触地面的感觉。感受重力如何将你固定在地球上。"
            },
            {
                icon: "🌿",
                title: "叶绿素",
                desc: "如果你身边有植物，去观察它的叶脉走向。如果没有，看看窗外的树。数一数你能看到多少种不同的绿色。"
            }
        ];

        // --- App Logic ---

        function startConsultation() {
            document.getElementById('scene-intro').classList.add('hidden');
            const scanScreen = document.getElementById('scene-scan');
            scanScreen.classList.remove('hidden');
            scanScreen.style.opacity = '1';

            // Simulate "Processing" time
            setTimeout(() => {
                scanScreen.classList.add('hidden');
                showResult();
            }, 2500);
        }

        function showResult() {
            const resultScene = document.getElementById('scene-result');
            resultScene.classList.remove('hidden');
            resultScene.classList.add('card-reveal');

            // Pick random prescription
            const randomTask = prescriptions[Math.floor(Math.random() * prescriptions.length)];
            
            document.getElementById('result-icon').innerText = randomTask.icon;
            document.getElementById('result-title').innerText = randomTask.title;
            document.getElementById('result-desc').innerText = randomTask.desc;
            
            // Update detox instruction text too
            document.getElementById('detox-instruction').innerHTML = `现在的任务是：<span class="text-cyan-300">${randomTask.title}</span><br>请放下手机，专心体验。`;
        }

        function resetApp() {
            document.getElementById('scene-result').classList.add('hidden');
            document.getElementById('scene-result').classList.remove('card-reveal');
            document.getElementById('scene-intro').classList.remove('hidden');
        }

        // --- Timer Logic ---
        let timerInterval;
        let timeLeft = 300; // 5 minutes in seconds

        function activateDetoxMode() {
            document.body.classList.add('detox-mode-active');
            timeLeft = 300; 
            updateTimerDisplay();
            
            // Start countdown
            timerInterval = setInterval(() => {
                timeLeft--;
                updateTimerDisplay();
                if (timeLeft <= 0) {
                    clearInterval(timerInterval);
                    timerComplete();
                }
            }, 1000);
        }

        function exitDetoxMode() {
            clearInterval(timerInterval);
            document.body.classList.remove('detox-mode-active');
        }

        function updateTimerDisplay() {
            const m = Math.floor(timeLeft / 60);
            const s = timeLeft % 60;
            document.getElementById('timer-display').innerText = 
                `${m.toString().padStart(2, '0')}:${s.toString().padStart(2, '0')}`;
        }

        function timerComplete() {
            document.getElementById('timer-display').innerText = "完成";
            document.getElementById('detox-instruction').innerText = "你做到了。现在感觉如何？";
            // Optional sound or visual cue could go here
        }

        // --- Particle System (Canvas) ---
        const canvas = document.getElementById('canvas-bg');
        const ctx = canvas.getContext('2d');
        let particles = [];

        function resizeCanvas() {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        }
        window.addEventListener('resize', resizeCanvas);
        resizeCanvas();

        class Particle {
            constructor() {
                this.x = Math.random() * canvas.width;
                this.y = Math.random() * canvas.height;
                this.vx = (Math.random() - 0.5) * 0.5;
                this.vy = (Math.random() - 0.5) * 0.5;
                this.size = Math.random() * 2 + 1;
                
                // Color palette: Cyan, Purple, Dark Blue
                const colors = ['rgba(0, 243, 255, ', 'rgba(188, 19, 254, ', 'rgba(50, 50, 150, '];
                this.colorBase = colors[Math.floor(Math.random() * colors.length)];
                this.opacity = Math.random() * 0.5 + 0.1;
            }

            update() {
                this.x += this.vx;
                this.y += this.vy;

                // Bounce off edges
                if (this.x < 0 || this.x > canvas.width) this.vx *= -1;
                if (this.y < 0 || this.y > canvas.height) this.vy *= -1;
            }

            draw() {
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
                ctx.fillStyle = this.colorBase + this.opacity + ')';
                ctx.fill();
            }
        }

        function initParticles() {
            particles = [];
            const particleCount = window.innerWidth < 768 ? 50 : 100; // Fewer on mobile
            for (let i = 0; i < particleCount; i++) {
                particles.push(new Particle());
            }
        }

        function animate() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            
            // Draw connections
            for (let i = 0; i < particles.length; i++) {
                particles[i].update();
                particles[i].draw();

                for (let j = i; j < particles.length; j++) {
                    const dx = particles[i].x - particles[j].x;
                    const dy = particles[i].y - particles[j].y;
                    const distance = Math.sqrt(dx * dx + dy * dy);

                    if (distance < 100) {
                        ctx.beginPath();
                        ctx.strokeStyle = `rgba(0, 243, 255, ${0.1 - distance/1000})`;
                        ctx.lineWidth = 0.5;
                        ctx.moveTo(particles[i].x, particles[i].y);
                        ctx.lineTo(particles[j].x, particles[j].y);
                        ctx.stroke();
                    }
                }
            }
            requestAnimationFrame(animate);
        }

        initParticles();
        animate();

    </script>
</body>
</html>
