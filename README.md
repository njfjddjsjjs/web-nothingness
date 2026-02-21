<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <title>NOHINGNESS</title>
    <style>
        :root { --red: #800000; --bright: #ff0000; --void: #000; }
        * { -webkit-user-select: none; user-select: none; cursor: crosshair; box-sizing: border-box; }
        
        body { 
            margin: 0; background: var(--void); color: var(--red);
            font-family: 'Courier New', monospace; height: 100vh;
            display: flex; overflow: hidden;
            animation: vhs 0.1s infinite;
        }

        /* Scanlines */
        body::before {
            content: " "; position: absolute; inset: 0; z-index: 5000;
            background: linear-gradient(rgba(18, 16, 16, 0) 50%, rgba(0, 0, 0, 0.1) 50%);
            background-size: 100% 4px; pointer-events: none;
        }

        .sidebar {
            width: 280px; border-left: 1px solid var(--red);
            background: #000; display: flex; flex-direction: column;
            padding: 50px 20px; z-index: 100;
        }

        .header {
            font-size: 1.5rem; text-align: center; border: 1px solid var(--red);
            padding: 10px; margin-bottom: 60px; letter-spacing: 5px; color: var(--bright);
            box-shadow: 0 0 10px #400;
        }

        .node {
            padding: 15px; margin-bottom: 10px; border: 1px solid #100;
            cursor: pointer; font-size: 0.8rem; transition: 0.1s; text-align: center;
        }
        .node:hover { color: var(--bright); border-color: var(--bright); background: #100; }

        .viewer { flex-grow: 1; display: flex; justify-content: center; align-items: center; padding: 50px; }

        .panel {
            border: 1px solid var(--red); padding: 50px; background: rgba(5, 0, 0, 0.9);
            width: 100%; max-width: 700px; display: none; text-align: center;
        }
        .panel.active { display: block; animation: flicker 0.2s ease; }

        .trigger { margin-top: auto; }
        .btn {
            display: block; width: 100%; padding: 20px; background: transparent;
            color: var(--red); border: 1px solid var(--red); text-decoration: none;
            font-weight: bold; font-size: 0.9rem; letter-spacing: 4px; text-align: center;
        }
        .btn:hover { background: var(--red); color: #000; box-shadow: 0 0 20px var(--red); }

        @keyframes vhs { 0% { opacity: 0.98; } 50% { opacity: 1; } 100% { opacity: 0.99; } }
        @keyframes flicker { from { opacity: 0; } to { opacity: 1; } }
    </style>
</head>
<body onclick="document.getElementById('amb').play()" oncontextmenu="return false;">

    <audio id="amb" loop src="https://www.soundjay.com/communication/sounds/radio-static-1.mp3"></audio>
    <audio id="tap" src="https://www.soundjay.com/buttons/sounds/beep-24.mp3"></audio>

    <aside class="sidebar">
        <div class="header">NOHINGNESS</div>
        <div class="node" onclick="view('p1')">SIGNAL</div>
        <div class="node" onclick="view('p2')">ENTITY</div>
        <div class="node" onclick="view('p3')">VAULT</div>
        <div class="trigger">
            <a href="DATA" id="act" class="btn" download>EXTRACT</a>
        </div>
    </aside>

    <main class="viewer">
        <div id="p1" class="panel active">
            <h2 style="font-size: 0.9rem;">> 00:00</h2>
            <p style="color: #400;">لا توجد استجابة.</p>
        </div>
        <div id="p2" class="panel">
            <h2 style="font-size: 0.9rem;">> الكيان</h2>
            <p style="color: #400;">يراقب.</p>
        </div>
        <div id="p3" class="panel">
            <h2 style="font-size: 0.9rem; color: var(--bright);">> الحقيقة</h2>
            <p style="color: #400;">السحب سيؤدي إلى كشف موقعك الفيزيائي.</p>
        </div>
    </main>

    <script>
        function view(id) {
            document.getElementById('tap').play();
            document.querySelectorAll('.panel').forEach(p => p.classList.remove('active'));
            document.getElementById(id).classList.add('active');
        }
        
        // تغيير حالة الزر عند الضغط للغموض
        document.getElementById('act').onclick = function() {
            this.innerText = "TRANSFERRING...";
            setTimeout(() => { this.innerText = "DONE"; }, 1500);
        };
    </script>
</body>
</html>
