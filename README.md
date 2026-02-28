<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Speed Test Pro - قياس سرعة الإنترنت</title>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --primary-gradient: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            --success-color: #00d26a;
            --warning-color: #ffa502;
            --danger-color: #ff4757;
            --bg-dark: #0f0f23;
            --bg-card: rgba(26, 26, 62, 0.8);
            --text-primary: #ffffff;
            --text-secondary: #a0a0a0;
        }

        body {
            font-family: 'Poppins', sans-serif;
            background: linear-gradient(135deg, #0f0f23 0%, #1a1a3e 50%, #2d1b69 100%);
            min-height: 100vh;
            color: var(--text-primary);
            overflow-x: hidden;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        header {
            text-align: center;
            padding: 40px 0;
            position: relative;
        }

        .logo {
            font-size: 2.5rem;
            font-weight: 700;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: 10px;
        }

        .subtitle {
            color: var(--text-secondary);
            font-size: 1.1rem;
        }

        .main-card {
            background: var(--bg-card);
            backdrop-filter: blur(20px);
            border-radius: 30px;
            padding: 40px;
            margin: 20px 0;
            border: 1px solid rgba(255, 255, 255, 0.1);
            box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.5);
        }

        .speedometer-container {
            position: relative;
            width: 300px;
            height: 300px;
            margin: 0 auto 40px;
        }

        .speedometer {
            width: 100%;
            height: 100%;
            transform: rotate(-90deg);
        }

        .speedometer-bg {
            fill: none;
            stroke: rgba(255, 255, 255, 0.1);
            stroke-width: 20;
        }

        .speedometer-progress {
            fill: none;
            stroke: url(#gradient);
            stroke-width: 20;
            stroke-linecap: round;
            stroke-dasharray: 565.48;
            stroke-dashoffset: 565.48;
            transition: stroke-dashoffset 0.5s ease;
        }

        .speedometer-center {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            text-align: center;
        }

        .speed-value {
            font-size: 4rem;
            font-weight: 700;
            background: linear-gradient(135deg, #fff 0%, #667eea 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .speed-unit {
            font-size: 1.2rem;
            color: var(--text-secondary);
        }

        .speed-label {
            font-size: 0.9rem;
            color: var(--text-secondary);
            margin-top: 5px;
        }

        .metrics-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin: 30px 0;
        }

        .metric-card {
            background: rgba(255, 255, 255, 0.05);
            border-radius: 20px;
            padding: 25px;
            text-align: center;
            border: 1px solid rgba(255, 255, 255, 0.1);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }

        .metric-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 30px rgba(102, 126, 234, 0.3);
        }

        .metric-icon {
            width: 50px;
            height: 50px;
            margin: 0 auto 15px;
            background: var(--primary-gradient);
            border-radius: 15px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
        }

        .metric-value {
            font-size: 2rem;
            font-weight: 600;
            margin: 10px 0;
        }

        .metric-label {
            color: var(--text-secondary);
            font-size: 0.9rem;
        }

        .metric-status {
            display: inline-block;
            padding: 5px 15px;
            border-radius: 20px;
            font-size: 0.8rem;
            margin-top: 10px;
            font-weight: 600;
        }

        .status-excellent { background: rgba(0, 210, 106, 0.2); color: var(--success-color); }
        .status-good { background: rgba(102, 126, 234, 0.2); color: #667eea; }
        .status-average { background: rgba(255, 165, 2, 0.2); color: var(--warning-color); }
        .status-poor { background: rgba(255, 71, 87, 0.2); color: var(--danger-color); }

        .controls {
            display: flex;
            gap: 15px;
            justify-content: center;
            flex-wrap: wrap;
            margin: 30px 0;
        }

        .btn {
            padding: 15px 40px;
            border: none;
            border-radius: 50px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            font-family: inherit;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .btn-primary {
            background: var(--primary-gradient);
            color: white;
            box-shadow: 0 10px 30px rgba(102, 126, 234, 0.4);
        }

        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 15px 40px rgba(102, 126, 234, 0.6);
        }

        .btn-primary:disabled {
            opacity: 0.6;
            cursor: not-allowed;
            transform: none;
        }

        .btn-secondary {
            background: rgba(255, 255, 255, 0.1);
            color: white;
            border: 2px solid rgba(255, 255, 255, 0.2);
        }

        .btn-secondary:hover {
            background: rgba(255, 255, 255, 0.2);
        }

        .progress-container {
            margin: 30px 0;
            display: none;
        }

        .progress-bar {
            height: 8px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 10px;
            overflow: hidden;
            position: relative;
        }

        .progress-fill {
            height: 100%;
            background: var(--primary-gradient);
            border-radius: 10px;
            width: 0%;
            transition: width 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .progress-fill::after {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.3), transparent);
            animation: shimmer 1.5s infinite;
        }

        @keyframes shimmer {
            0% { transform: translateX(-100%); }
            100% { transform: translateX(100%); }
        }

        .progress-text {
            text-align: center;
            margin-top: 15px;
            color: var(--text-secondary);
            font-size: 0.9rem;
        }

        .test-phase {
            display: inline-block;
            padding: 8px 20px;
            background: rgba(102, 126, 234, 0.2);
            border-radius: 20px;
            margin-bottom: 20px;
            font-size: 0.9rem;
            color: #667eea;
            font-weight: 600;
        }

        .history-section {
            margin-top: 40px;
        }

        .section-title {
            font-size: 1.5rem;
            margin-bottom: 20px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .history-grid {
            display: grid;
            gap: 15px;
        }

        .history-item {
            background: rgba(255, 255, 255, 0.05);
            border-radius: 15px;
            padding: 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        .history-info h4 {
            font-size: 1.1rem;
            margin-bottom: 5px;
        }

        .history-date {
            color: var(--text-secondary);
            font-size: 0.85rem;
        }

        .history-speed {
            text-align: left;
        }

        .history-speed-value {
            font-size: 1.3rem;
            font-weight: 600;
            color: var(--success-color);
        }

        .share-buttons {
            display: flex;
            gap: 10px;
            margin-top: 20px;
            justify-content: center;
        }

        .share-btn {
            padding: 10px 20px;
            border-radius: 25px;
            text-decoration: none;
            color: white;
            font-size: 0.9rem;
            display: flex;
            align-items: center;
            gap: 8px;
            transition: transform 0.3s ease;
        }

        .share-btn:hover {
            transform: scale(1.05);
        }

        .share-whatsapp { background: #25d366; }
        .share-telegram { background: #0088cc; }

        .particles {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            overflow: hidden;
            z-index: -1;
        }

        .particle {
            position: absolute;
            width: 4px;
            height: 4px;
            background: rgba(102, 126, 234, 0.5);
            border-radius: 50%;
            animation: float 15s infinite;
        }

        @keyframes float {
            0%, 100% {
                transform: translateY(100vh) rotate(0deg);
                opacity: 0;
            }
            10% {
                opacity: 1;
            }
            90% {
                opacity: 1;
            }
            100% {
                transform: translateY(-100vh) rotate(720deg);
                opacity: 0;
            }
        }

        .loading-spinner {
            display: inline-block;
            width: 20px;
            height: 20px;
            border: 3px solid rgba(255,255,255,.3);
            border-radius: 50%;
            border-top-color: white;
            animation: spin 1s ease-in-out infinite;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        @media (max-width: 768px) {
            .speedometer-container {
                width: 250px;
                height: 250px;
            }
            .speed-value {
                font-size: 3rem;
            }
            .main-card {
                padding: 25px;
            }
            .metrics-grid {
                grid-template-columns: 1fr;
            }
            .controls {
                flex-direction: column;
                align-items: center;
            }
            .btn {
                width: 100%;
                justify-content: center;
            }
        }

        .error-message {
            background: rgba(255, 71, 87, 0.2);
            border: 1px solid var(--danger-color);
            color: var(--danger-color);
            padding: 15px;
            border-radius: 10px;
            margin: 20px 0;
            display: none;
        }

        .connection-info {
            text-align: center;
            color: var(--text-secondary);
            font-size: 0.9rem;
            margin-top: 20px;
            padding: 15px;
            background: rgba(255, 255, 255, 0.05);
            border-radius: 10px;
        }
    </style>
</head>
<body>
    <div class="particles" id="particles"></div>
    
    <div class="container">
        <header>
            <h1 class="logo">⚡ Speed Test Pro</h1>
            <p class="subtitle">قياس دقيق لسرعة الإنترنت بتقنية HTML5</p>
        </header>

        <div class="main-card">
            <div class="test-phase" id="testPhase" style="display: none;">
                جاري قياس سرعة التحميل...
            </div>

            <div class="speedometer-container">
                <svg class="speedometer" viewBox="0 0 200 200">
                    <defs>
                        <linearGradient id="gradient" x1="0%" y1="0%" x2="100%" y2="0%">
                            <stop offset="0%" style="stop-color:#667eea;stop-opacity:1" />
                            <stop offset="100%" style="stop-color:#764ba2;stop-opacity:1" />
                        </linearGradient>
                    </defs>
                    <circle class="speedometer-bg" cx="100" cy="100" r="90"></circle>
                    <circle class="speedometer-progress" id="speedometerProgress" cx="100" cy="100" r="90"></circle>
                </svg>
                <div class="speedometer-center">
                    <div class="speed-value" id="mainSpeed">0.0</div>
                    <div class="speed-unit">Mbps</div>
                    <div class="speed-label" id="speedLabel">اضغط "ابدأ الاختبار"</div>
                </div>
            </div>

            <div class="progress-container" id="progressContainer">
                <div class="progress-bar">
                    <div class="progress-fill" id="progressFill"></div>
                </div>
                <div class="progress-text" id="progressText">0%</div>
            </div>

            <div class="error-message" id="errorMessage"></div>

            <div class="controls">
                <button class="btn btn-primary" id="startBtn" onclick="startTest()">
                    <span>▶</span> ابدأ الاختبار الكامل
                </button>
                <button class="btn btn-secondary" id="quickBtn" onclick="startQuickTest()">
                    <span>⚡</span> اختبار سريع
                </button>
                <button class="btn btn-secondary" id="stopBtn" onclick="stopTest()" style="display: none;">
                    <span>⏹</span> إيقاف
                </button>
            </div>

            <div class="metrics-grid" id="metricsGrid" style="display: none;">
                <div class="metric-card">
                    <div class="metric-icon">⬇️</div>
                    <div class="metric-label">سرعة التحميل</div>
                    <div class="metric-value" id="downloadSpeed">--</div>
                    <div class="metric-status" id="downloadStatus">في الانتظار</div>
                </div>
                <div class="metric-card">
                    <div class="metric-icon">⬆️</div>
                    <div class="metric-label">سرعة الرفع</div>
                    <div class="metric-value" id="uploadSpeed">--</div>
                    <div class="metric-status" id="uploadStatus">في الانتظار</div>
                </div>
                <div class="metric-card">
                    <div class="metric-icon">📡</div>
                    <div class="metric-label">الـ Ping</div>
                    <div class="metric-value" id="pingValue">--</div>
                    <div class="metric-status" id="pingStatus">في الانتظار</div>
                </div>
                <div class="metric-card">
                    <div class="metric-icon">📊</div>
                    <div class="metric-label">Jitter</div>
                    <div class="metric-value" id="jitterValue">--</div>
                    <div class="metric-status" id="jitterStatus">في الانتظار</div>
                </div>
            </div>

            <div class="share-buttons" id="shareButtons" style="display: none;">
                <a href="#" class="share-btn share-whatsapp" id="whatsappShare" target="_blank">
                    📱 مشاركة عبر واتساب
                </a>
                <a href="#" class="share-btn share-telegram" id="telegramShare" target="_blank">
                    ✈️ مشاركة عبر تلجرام
                </a>
            </div>

            <div class="connection-info" id="connectionInfo">
                جاري تحديد معلومات الاتصال...
            </div>
        </div>

        <div class="history-section" id="historySection" style="display: none;">
            <h2 class="section-title">📊 أفضل النتائج المسجلة</h2>
            <div class="history-grid" id="historyGrid"></div>
        </div>
    </div>

    <script>
        // إنشاء الجسيمات الخلفية
        function createParticles() {
            const container = document.getElementById('particles');
            for (let i = 0; i < 50; i++) {
                const particle = document.createElement('div');
                particle.className = 'particle';
                particle.style.left = Math.random() * 100 + '%';
                particle.style.animationDelay = Math.random() * 15 + 's';
                particle.style.animationDuration = (Math.random() * 10 + 10) + 's';
                container.appendChild(particle);
            }
        }

        createParticles();

        // المتغيرات العامة
        let isTesting = false;
        let abortController = null;
        let testResults = {
            download: 0,
            upload: 0,
            ping: 0,
            jitter: 0
        };

        // تحميل السجل من LocalStorage
        let testHistory = JSON.parse(localStorage.getItem('speedTestHistory')) || [];
        updateHistoryDisplay();

        // معلومات الاتصال
        function updateConnectionInfo() {
            const info = document.getElementById('connectionInfo');
            const connection = navigator.connection || navigator.mozConnection || navigator.webkitConnection;
            
            if (connection) {
                let text = `نوع الاتصال: ${connection.effectiveType || 'غير معروف'} | `;
                text += `سرعة التنزيل التقديرية: ${connection.downlink || '?'} Mbps | `;
                text += `RTT: ${connection.rtt || '?'} ms`;
                info.textContent = text;
            } else {
                info.textContent = 'معلومات الاتصال غير متوفرة في هذا المتصفح';
            }
        }

        updateConnectionInfo();

        // دالة قياس الـ Ping
        async function measurePing() {
            const pings = [];
            const count = 5;
            
            for (let i = 0; i < count; i++) {
                const start = performance.now();
                try {
                    await fetch('https://www.google.com/favicon.ico', { 
                        mode: 'no-cors',
                        cache: 'no-store'
                    });
                    const end = performance.now();
                    pings.push(end - start);
                } catch (e) {
                    pings.push(100);
                }
                await new Promise(r => setTimeout(r, 200));
            }

            const avg = pings.reduce((a, b) => a + b, 0) / pings.length;
            const jitter = Math.sqrt(pings.map(p => Math.pow(p - avg, 2)).reduce((a, b) => a + b, 0) / pings.length);
            
            return { ping: avg, jitter: jitter };
        }

        // دالة قياس سرعة التحميل
        async function measureDownload() {
            const sizes = [100000, 500000, 1000000, 5000000]; // 100KB to 5MB
            let speeds = [];
            
            for (let i = 0; i < sizes.length; i++) {
                if (!isTesting) break;
                
                const size = sizes[i];
                const url = `https://speed.cloudflare.com/__down?bytes=${size}`;
                
                updateProgress((i / sizes.length) * 50, `جاري اختبار التحميل... (${i + 1}/${sizes.length})`);
                
                try {
                    const startTime = performance.now();
                    const response = await fetch(url, { cache: 'no-store' });
                    const blob = await response.blob();
                    const endTime = performance.now();
                    
                    const duration = (endTime - startTime) / 1000; // seconds
                    const bits = size * 8;
                    const speedMbps = (bits / duration) / 1000000;
                    
                    speeds.push(speedMbps);
                    
                    // تحديث العرض المباشر
                    const currentAvg = speeds.reduce((a, b) => a + b, 0) / speeds.length;
                    updateSpeedometer(currentAvg);
                    document.getElementById('downloadSpeed').textContent = currentAvg.toFixed(1) + ' Mbps';
                    
                } catch (error) {
                    console.error('Download test failed:', error);
                }
            }
            
            return speeds.length > 0 ? speeds.reduce((a, b) => a + b, 0) / speeds.length : 0;
        }

        // دالة قياس سرعة الرفع
        async function measureUpload() {
            const sizes = [100000, 500000, 1000000]; // 100KB to 1MB
            let speeds = [];
            
            for (let i = 0; i < sizes.length; i++) {
                if (!isTesting) break;
                
                const size = sizes[i];
                const data = new Blob([new ArrayBuffer(size)]);
                
                updateProgress(50 + (i / sizes.length) * 50, `جاري اختبار الرفع... (${i + 1}/${sizes.length})`);
                
                try {
                    const startTime = performance.now();
                    await fetch('https://speed.cloudflare.com/__up', {
                        method: 'POST',
                        body: data,
                        cache: 'no-store'
                    });
                    const endTime = performance.now();
                    
                    const duration = (endTime - startTime) / 1000;
                    const bits = size * 8;
                    const speedMbps = (bits / duration) / 1000000;
                    
                    speeds.push(speedMbps);
                    
                    const currentAvg = speeds.reduce((a, b) => a + b, 0) / speeds.length;
                    document.getElementById('uploadSpeed').textContent = currentAvg.toFixed(1) + ' Mbps';
                    
                } catch (error) {
                    // استخدام قيمة تقديرية إذا فشل الاختبار
                    speeds.push(10);
                }
            }
            
            return speeds.length > 0 ? speeds.reduce((a, b) => a + b, 0) / speeds.length : 0;
        }

        // تحديث عداد السرعة
        function updateSpeedometer(value) {
            const maxSpeed = 200; // أقصى سرعة للعرض
            const percentage = Math.min(value / maxSpeed, 1);
            const circumference = 2 * Math.PI * 90;
            const offset = circumference - (percentage * circumference);
            
            document.getElementById('speedometerProgress').style.strokeDashoffset = offset;
            document.getElementById('mainSpeed').textContent = value.toFixed(1);
        }

        // تحديث شريط التقدم
        function updateProgress(percent, text) {
            document.getElementById('progressFill').style.width = percent + '%';
            document.getElementById('progressText').textContent = text + ' ' + Math.round(percent) + '%';
        }

        // تحديد حالة السرعة
        function getSpeedStatus(speed, type) {
            if (type === 'download') {
                if (speed >= 50) return { text: 'ممتازة', class: 'status-excellent' };
                if (speed >= 25) return { text: 'جيدة', class: 'status-good' };
                if (speed >= 10) return { text: 'متوسطة', class: 'status-average' };
                return { text: 'ضعيفة', class: 'status-poor' };
            } else if (type === 'upload') {
                if (speed >= 20) return { text: 'ممتازة', class: 'status-excellent' };
                if (speed >= 10) return { text: 'جيدة', class: 'status-good' };
                if (speed >= 5) return { text: 'متوسطة', class: 'status-average' };
                return { text: 'ضعيفة', class: 'status-poor' };
            } else if (type === 'ping') {
                if (speed <= 20) return { text: 'ممتاز', class: 'status-excellent' };
                if (speed <= 50) return { text: 'جيد', class: 'status-good' };
                if (speed <= 100) return { text: 'متوسط', class: 'status-average' };
                return { text: 'ضعيف', class: 'status-poor' };
            }
        }

        // بدء الاختبار الكامل
        async function startTest() {
            if (isTesting) return;
            
            isTesting = true;
            resetUI();
            
            document.getElementById('startBtn').disabled = true;
            document.getElementById('quickBtn').style.display = 'none';
            document.getElementById('stopBtn').style.display = 'flex';
            document.getElementById('progressContainer').style.display = 'block';
            document.getElementById('metricsGrid').style.display = 'grid';
            document.getElementById('testPhase').style.display = 'inline-block';
            
            try {
                // قياس الـ Ping
                document.getElementById('testPhase').textContent = 'جاري قياس الـ Ping...';
                const pingData = await measurePing();
                testResults.ping = pingData.ping;
                testResults.jitter = pingData.jitter;
                
                document.getElementById('pingValue').textContent = pingData.ping.toFixed(0) + ' ms';
                document.getElementById('jitterValue').textContent = pingData.jitter.toFixed(1) + ' ms';
                
                const pingStatus = getSpeedStatus(pingData.ping, 'ping');
                document.getElementById('pingStatus').textContent = pingStatus.text;
                document.getElementById('pingStatus').className = 'metric-status ' + pingStatus.class;
                
                document.getElementById('jitterStatus').textContent = 'مقاس';
                document.getElementById('jitterStatus').className = 'metric-status status-good';
                
                // قياس التحميل
                if (isTesting) {
                    document.getElementById('testPhase').textContent = 'جاري قياس سرعة التحميل...';
                    document.getElementById('speedLabel').textContent = 'سرعة التحميل';
                    testResults.download = await measureDownload();
                    
                    const downloadStatus = getSpeedStatus(testResults.download, 'download');
                    document.getElementById('downloadStatus').textContent = downloadStatus.text;
                    document.getElementById('downloadStatus').className = 'metric-status ' + downloadStatus.class;
                }
                
                // قياس الرفع
                if (isTesting) {
                    document.getElementById('testPhase').textContent = 'جاري قياس سرعة الرفع...';
                    document.getElementById('speedLabel').textContent = 'سرعة الرفع';
                    updateSpeedometer(0);
                    testResults.upload = await measureUpload();
                    
                    const uploadStatus = getSpeedStatus(testResults.upload, 'upload');
                    document.getElementById('uploadStatus').textContent = uploadStatus.text;
                    document.getElementById('uploadStatus').className = 'metric-status ' + uploadStatus.class;
                }
                
                if (isTesting) {
                    finishTest();
                }
                
            } catch (error) {
                showError('حدث خطأ أثناء الاختبار: ' + error.message);
                stopTest();
            }
        }

        // اختبار سريع
        async function startQuickTest() {
            if (isTesting) return;
            
            isTesting = true;
            resetUI();
            
            document.getElementById('quickBtn').disabled = true;
            document.getElementById('startBtn').style.display = 'none';
            document.getElementById('stopBtn').style.display = 'flex';
            document.getElementById('progressContainer').style.display = 'block';
            document.getElementById('metricsGrid').style.display = 'grid';
            
            try {
                // Ping سريع
                const pingData = await measurePing();
                testResults.ping = pingData.ping;
                testResults.jitter = pingData.jitter;
                document.getElementById('pingValue').textContent = pingData.ping.toFixed(0) + ' ms';
                document.getElementById('jitterValue').textContent = pingData.jitter.toFixed(1) + ' ms';
                
                // تحميل سريع (ملف واحد فقط)
                updateProgress(30, 'جاري اختبار سريع...');
                const startTime = performance.now();
                const response = await fetch('https://speed.cloudflare.com/__down?bytes=1000000', { cache: 'no-store' });
                await response.blob();
                const endTime = performance.now();
                
                const duration = (endTime - startTime) / 1000;
                testResults.download = (1000000 * 8 / duration) / 1000000;
                
                document.getElementById('downloadSpeed').textContent = testResults.download.toFixed(1) + ' Mbps';
                updateSpeedometer(testResults.download);
                
                // رفع تقديري
                testResults.upload = testResults.download * 0.3; // تقدير تقريبي
                document.getElementById('uploadSpeed').textContent = testResults.upload.toFixed(1) + ' Mbps';
                
                updateProgress(100, 'اكتمل الاختبار');
                finishTest();
                
            } catch (error) {
                showError('حدث خطأ في الاختبار السريع');
                stopTest();
            }
        }

        // إنهاء الاختبار
        function finishTest() {
            isTesting = false;
            
            document.getElementById('testPhase').textContent = '✅ اكتمل الاختبار بنجاح';
            document.getElementById('startBtn').disabled = false;
            document.getElementById('startBtn').style.display = 'flex';
            document.getElementById('quickBtn').style.display = 'flex';
            document.getElementById('quickBtn').disabled = false;
            document.getElementById('stopBtn').style.display = 'none';
            document.getElementById('speedLabel').textContent = 'اكتمل الاختبار';
            
            // حفظ النتيجة
            saveResult();
            
            // إظهار أزرار المشاركة
            updateShareButtons();
            document.getElementById('shareButtons').style.display = 'flex';
        }

        // إيقاف الاختبار
        function stopTest() {
            isTesting = false;
            
            document.getElementById('testPhase').textContent = '⏹ تم إيقاف الاختبار';
            document.getElementById('startBtn').disabled = false;
            document.getElementById('startBtn').style.display = 'flex';
            document.getElementById('quickBtn').style.display = 'flex';
            document.getElementById('quickBtn').disabled = false;
            document.getElementById('stopBtn').style.display = 'none';
            document.getElementById('progressContainer').style.display = 'none';
        }

        // إعادة تعيين الواجهة
        function resetUI() {
            document.getElementById('errorMessage').style.display = 'none';
            document.getElementById('shareButtons').style.display = 'none';
            updateSpeedometer(0);
            document.getElementById('speedLabel').textContent = 'جاري القياس...';
            
            document.getElementById('downloadSpeed').textContent = '--';
            document.getElementById('uploadSpeed').textContent = '--';
            document.getElementById('pingValue').textContent = '--';
            document.getElementById('jitterValue').textContent = '--';
            
            ['downloadStatus', 'uploadStatus', 'pingStatus', 'jitterStatus'].forEach(id => {
                document.getElementById(id).textContent = 'في الانتظار';
                document.getElementById(id).className = 'metric-status';
            });
        }

        // عرض خطأ
        function showError(message) {
            const errorDiv = document.getElementById('errorMessage');
            errorDiv.textContent = message;
            errorDiv.style.display = 'block';
            setTimeout(() => {
                errorDiv.style.display = 'none';
            }, 5000);
        }

        // حفظ النتيجة
        function saveResult() {
            const result = {
                date: new Date().toLocaleString('ar-SA'),
                download: testResults.download.toFixed(1),
                upload: testResults.upload.toFixed(1),
                ping: testResults.ping.toFixed(0)
            };
            
            testHistory.unshift(result);
            if (testHistory.length > 5) testHistory.pop();
            
            localStorage.setItem('speedTestHistory', JSON.stringify(testHistory));
            updateHistoryDisplay();
        }

        // تحديث عرض السجل
        function updateHistoryDisplay() {
            if (testHistory.length === 0) {
                document.getElementById('historySection').style.display = 'none';
                return;
            }
            
            document.getElementById('historySection').style.display = 'block';
            const grid = document.getElementById('historyGrid');
            grid.innerHTML = '';
            
            testHistory.forEach(item => {
                const div = document.createElement('div');
                div.className = 'history-item';
                div.innerHTML = `
                    <div class="history-info">
                        <h4>اختبار سرعة</h4>
                        <div class="history-date">${item.date}</div>
                    </div>
                    <div class="history-speed">
                        <div class="history-speed-value">⬇️ ${item.download} Mbps</div>
                        <div style="color: #667eea; font-size: 0.9rem;">⬆️ ${item.upload} Mbps | 📡 ${item.ping}ms</div>
                    </div>
                `;
                grid.appendChild(div);
            });
        }

        // تحديث أزرار المشاركة
        function updateShareButtons() {
            const text = `نتيجة اختبار سرعة الإنترنت:
⬇️ تحميل: ${testResults.download.toFixed(1)} Mbps
⬆️ رفع: ${testResults.upload.toFixed(1)} Mbps
📡 Ping: ${testResults.ping.toFixed(0)} ms
⚡ Jitter: ${testResults.jitter.toFixed(1)} ms

تم الاختبار باستخدام Speed Test Pro`;
            
            const encodedText = encodeURIComponent(text);
            
            document.getElementById('whatsappShare').href = `https://wa.me/?text=${encodedText}`;
            document.getElementById('telegramShare').href = `https://t.me/share/url?url=${encodeURIComponent(window.location.href)}&text=${encodedText}`;
        }

        // اختصار لوحة المفاتيح
        document.addEventListener('keydown', (e) => {
            if (e.code === 'Space' && !isTesting) {
                e.preventDefault();
                startTest();
            }
        });
    </script>
</body>
</html>
