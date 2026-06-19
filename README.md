# dokter-gyigi
game ini untuk membantu merawat gigi dengan baik dan benar
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Dokter Gigi</title>
    <style>
        /* ===== RESET & GLOBAL ===== */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(145deg, #e0f0ff 0%, #b5d9f7 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
            margin: 0;
        }

        /* ===== GAME CONTAINER ===== */
        .game-container {
            max-width: 800px;
            width: 100%;
            background: linear-gradient(170deg, #ffffff 0%, #f5faff 100%);
            border-radius: 60px 60px 40px 40px;
            box-shadow:
                0 25px 50px -8px rgba(0, 40, 80, 0.35),
                inset 0 2px 4px rgba(255, 255, 255, 0.7);
            padding: 30px 30px 40px;
            position: relative;
            border: 2px solid rgba(255, 255, 255, 0.6);
            transition: all 0.3s;
        }

        /* ===== HEADER ===== */
        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 16px;
            margin-bottom: 18px;
            padding-bottom: 14px;
            border-bottom: 3px dashed #b8d4f0;
        }

        .title-section {
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .title-section .icon {
            font-size: 38px;
            line-height: 1;
            filter: drop-shadow(0 4px 6px rgba(0, 0, 0, 0.1));
            animation: float-icon 3s ease-in-out infinite;
        }

        @keyframes float-icon {
            0%,
            100% {
                transform: translateY(0) rotate(-2deg);
            }
            50% {
                transform: translateY(-6px) rotate(2deg);
            }
        }

        .title-section h1 {
            font-size: 32px;
            font-weight: 800;
            background: linear-gradient(135deg, #1a5f8a, #0d3b5c);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            letter-spacing: 1px;
            text-shadow: 0 2px 12px rgba(26, 95, 138, 0.15);
        }

        .title-section h1 span {
            background: linear-gradient(135deg, #f9a825, #f57f17);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .score-board {
            background: linear-gradient(135deg, #1a5f8a, #0d3b5c);
            padding: 10px 24px;
            border-radius: 50px;
            box-shadow: 0 6px 14px rgba(13, 59, 92, 0.35);
            display: flex;
            align-items: center;
            gap: 14px;
            color: white;
            font-weight: 600;
            border: 2px solid rgba(255, 255, 255, 0.2);
        }

        .score-board .label {
            font-size: 14px;
            text-transform: uppercase;
            letter-spacing: 1px;
            opacity: 0.8;
        }

        .score-board .value {
            font-size: 30px;
            font-weight: 800;
            background: white;
            color: #0d3b5c;
            padding: 0 12px;
            border-radius: 30px;
            min-width: 48px;
            text-align: center;
            line-height: 1.4;
        }

        /* ===== PATIENT INFO ===== */
        .patient-info {
            display: flex;
            align-items: center;
            justify-content: space-between;
            background: rgba(255, 255, 255, 0.6);
            backdrop-filter: blur(6px);
            border-radius: 40px;
            padding: 8px 20px 8px 8px;
            margin-bottom: 16px;
            border: 2px solid rgba(255, 255, 255, 0.8);
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.04);
        }

        .patient-avatar {
            display: flex;
            align-items: center;
            gap: 14px;
        }

        .patient-avatar .face {
            font-size: 50px;
            line-height: 1;
            filter: drop-shadow(0 4px 8px rgba(0, 0, 0, 0.08));
            transition: transform 0.3s;
        }

        .patient-avatar .face.happy {
            animation: happy-face 0.6s ease;
        }

        @keyframes happy-face {
            0%,
            100% {
                transform: scale(1);
            }
            50% {
                transform: scale(1.2) rotate(-6deg);
            }
        }

        .patient-avatar .name {
            font-size: 20px;
            font-weight: 700;
            color: #1a3b4f;
        }

        .patient-avatar .name small {
            font-weight: 400;
            font-size: 14px;
            color: #5a7a8a;
            display: block;
            margin-top: -2px;
        }

        .patient-status {
            display: flex;
            align-items: center;
            gap: 12px;
            background: white;
            padding: 6px 18px 6px 14px;
            border-radius: 30px;
            box-shadow: inset 0 2px 6px rgba(0, 0, 0, 0.04);
        }

        .patient-status .label {
            font-size: 13px;
            color: #5a7a8a;
            font-weight: 500;
        }

        .patient-status .tooth-count {
            font-size: 22px;
            font-weight: 700;
            color: #0d3b5c;
            background: #eaf3fa;
            padding: 0 12px;
            border-radius: 20px;
            line-height: 1.6;
        }

        /* ===== TOOTH GRID ===== */
        .mouth-container {
            background: radial-gradient(ellipse at center, #fde8d0 0%, #f5d4b8 100%);
            border-radius: 120px 120px 60px 60px;
            padding: 30px 40px 28px;
            margin: 8px 0 14px;
            position: relative;
            border: 4px solid #f0c4a0;
            box-shadow:
                inset 0 -8px 20px rgba(180, 100, 60, 0.15),
                0 12px 30px rgba(0, 0, 0, 0.08);
            min-height: 200px;
        }

        .mouth-container::before {
            content: '👄';
            position: absolute;
            top: -18px;
            left: 50%;
            transform: translateX(-50%);
            font-size: 32px;
            filter: drop-shadow(0 4px 8px rgba(0, 0, 0, 0.06));
        }

        .tooth-row {
            display: flex;
            justify-content: center;
            gap: 10px;
            margin-bottom: 12px;
            flex-wrap: wrap;
        }

        .tooth-row:last-child {
            margin-bottom: 0;
        }

        .tooth {
            width: 52px;
            height: 60px;
            border-radius: 8px 8px 16px 16px;
            background: #f8f4f0;
            border: 3px solid #d4c8bc;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 22px;
            cursor: pointer;
            transition: all 0.2s cubic-bezier(0.34, 1.56, 0.64, 1);
            box-shadow:
                0 4px 0 #b8aa9c,
                0 6px 12px rgba(0, 0, 0, 0.06);
            position: relative;
            user-select: none;
        }

        .tooth:hover {
            transform: translateY(-3px) scale(1.04);
            box-shadow: 0 8px 0 #b8aa9c, 0 12px 24px rgba(0, 0, 0, 0.12);
        }

        .tooth:active {
            transform: translateY(4px) scale(0.96);
            box-shadow: 0 2px 0 #b8aa9c, 0 6px 12px rgba(0, 0, 0, 0.06);
        }

        /* Tooth states */
        .tooth.clean {
            background: linear-gradient(145deg, #ffffff, #f0ece8);
            border-color: #d4c8bc;
            box-shadow: 0 4px 0 #b8aa9c, 0 6px 12px rgba(0, 0, 0, 0.04);
        }

        .tooth.clean::after {
            content: '✨';
            position: absolute;
            top: -12px;
            right: -10px;
            font-size: 16px;
            animation: sparkle 2s ease-in-out infinite;
        }

        @keyframes sparkle {
            0%,
            100% {
                transform: scale(1) rotate(0deg);
                opacity: 0.7;
            }
            50% {
                transform: scale(1.3) rotate(20deg);
                opacity: 1;
            }
        }

        .tooth.dirty {
            background: linear-gradient(145deg, #e8d5b0, #d4b88a);
            border-color: #b8956a;
            box-shadow: 0 4px 0 #a0805a, 0 6px 12px rgba(0, 0, 0, 0.08);
        }

        .tooth.dirty::before {
            content: '🦷';
            opacity: 0.3;
            font-size: 28px;
        }

        .tooth.dirty .stain {
            position: absolute;
            width: 14px;
            height: 14px;
            background: radial-gradient(circle, #7a5a3a, #5a3a1a);
            border-radius: 50%;
            opacity: 0.5;
            top: 30%;
            left: 20%;
            filter: blur(2px);
        }

        .tooth.dirty .stain:nth-child(2) {
            top: 50%;
            left: 55%;
            width: 10px;
            height: 10px;
            opacity: 0.4;
        }

        .tooth.cavity {
            background: linear-gradient(145deg, #d4b8a0, #b8957a);
            border-color: #8a6a52;
            box-shadow: 0 4px 0 #6a4e3a, 0 6px 12px rgba(0, 0, 0, 0.1);
        }

        .tooth.cavity::before {
            content: '🕳️';
            font-size: 20px;
            filter: drop-shadow(0 2px 4px rgba(0, 0, 0, 0.2));
        }

        .tooth.fixed {
            background: linear-gradient(145deg, #ffffff, #e8f0e8);
            border-color: #8aba8a;
            box-shadow: 0 4px 0 #6a9a6a, 0 6px 12px rgba(0, 0, 0, 0.04);
        }

        .tooth.fixed::after {
            content: '🦷';
            font-size: 20px;
            opacity: 0.6;
        }

        /* ===== TOOLS ===== */
        .tools-section {
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 16px;
            flex-wrap: wrap;
            margin: 16px 0 10px;
            padding: 14px 20px;
            background: rgba(255, 255, 255, 0.5);
            backdrop-filter: blur(4px);
            border-radius: 60px;
            border: 2px solid rgba(255, 255, 255, 0.8);
        }

        .tools-section .label {
            font-size: 14px;
            font-weight: 600;
            color: #1a3b4f;
            letter-spacing: 0.5px;
            margin-right: 4px;
        }

        .tool-btn {
            padding: 10px 20px;
            border: none;
            border-radius: 40px;
            font-size: 15px;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.2s cubic-bezier(0.34, 1.56, 0.64, 1);
            display: flex;
            align-items: center;
            gap: 8px;
            background: white;
            color: #1a3b4f;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.06);
            border: 2px solid transparent;
        }

        .tool-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.08);
        }

        .tool-btn:active {
            transform: translateY(2px) scale(0.96);
        }

        .tool-btn .emoji {
            font-size: 22px;
        }

        .tool-btn.active {
            border-color: #1a5f8a;
            background: linear-gradient(135deg, #e8f4fd, #d0e8f8);
            box-shadow: 0 4px 16px rgba(26, 95, 138, 0.2);
            transform: scale(1.04);
        }

        .tool-btn.active .emoji {
            animation: tool-bounce 1s ease-in-out infinite;
        }

        @keyframes tool-bounce {
            0%,
            100% {
                transform: rotate(-4deg);
            }
            50% {
                transform: rotate(4deg);
            }
        }

        .tool-btn.toothbrush.active {
            border-color: #43a047;
            background: linear-gradient(135deg, #e8f5e9, #c8e6c9);
        }

        .tool-btn.scraper.active {
            border-color: #f57c00;
            background: linear-gradient(135deg, #fff3e0, #ffe0b2);
        }

        .tool-btn.drill.active {
            border-color: #e53935;
            background: linear-gradient(135deg, #ffebee, #ffcdd2);
        }

        /* ===== INFO BAR ===== */
        .info-bar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 12px;
            margin-top: 14px;
            padding: 10px 16px;
            background: rgba(255, 255, 255, 0.4);
            border-radius: 30px;
            backdrop-filter: blur(4px);
        }

        .message-box {
            font-size: 16px;
            font-weight: 500;
            color: #1a3b4f;
            padding: 6px 16px;
            background: white;
            border-radius: 30px;
            box-shadow: inset 0 2px 6px rgba(0, 0, 0, 0.02);
            flex: 1;
            min-width: 120px;
        }

        .message-box .highlight {
            color: #1a5f8a;
            font-weight: 700;
        }

        .btn-reset {
            padding: 8px 22px;
            border: none;
            border-radius: 30px;
            background: linear-gradient(135deg, #ff8a65, #e64a19);
            color: white;
            font-weight: 700;
            font-size: 15px;
            cursor: pointer;
            transition: all 0.2s;
            box-shadow: 0 4px 12px rgba(230, 74, 25, 0.25);
            display: flex;
            align-items: center;
            gap: 6px;
        }

        .btn-reset:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 20px rgba(230, 74, 25, 0.3);
        }

        .btn-reset:active {
            transform: translateY(2px) scale(0.96);
        }

        /* ===== RESPONSIVE ===== */
        @media (max-width: 640px) {
            .game-container {
                padding: 20px 16px 30px;
                border-radius: 40px;
            }

            .title-section h1 {
                font-size: 24px;
            }
            .title-section .icon {
                font-size: 28px;
            }

            .score-board {
                padding: 6px 16px;
            }
            .score-board .value {
                font-size: 22px;
                min-width: 36px;
            }

            .mouth-container {
                padding: 20px 16px 18px;
                border-radius: 80px 80px 40px 40px;
            }

            .tooth {
                width: 38px;
                height: 46px;
                font-size: 16px;
                border-radius: 6px 6px 12px 12px;
            }

            .tooth-row {
                gap: 6px;
            }

            .tools-section {
                padding: 10px 14px;
                gap: 10px;
                border-radius: 40px;
            }

            .tool-btn {
                padding: 8px 14px;
                font-size: 13px;
            }
            .tool-btn .emoji {
                font-size: 18px;
            }

            .patient-avatar .face {
                font-size: 38px;
            }
            .patient-avatar .name {
                font-size: 16px;
            }

            .info-bar {
                flex-direction: column;
                align-items: stretch;
                text-align: center;
            }

            .btn-reset {
                justify-content: center;
            }
        }

        @media (max-width: 420px) {
            .tooth {
                width: 30px;
                height: 38px;
                font-size: 12px;
                border-width: 2px;
            }
            .tooth-row {
                gap: 4px;
            }
            .mouth-container {
                padding: 14px 8px 12px;
            }
            .tools-section .label {
                font-size: 12px;
                width: 100%;
                text-align: center;
            }
        }

        /* ===== CELEBRATION ===== */
        .celebration {
            position: fixed;
            pointer-events: none;
            font-size: 40px;
            animation: celeb-fly 1.8s ease-out forwards;
            z-index: 999;
        }

        @keyframes celeb-fly {
            0% {
                opacity: 1;
                transform: translateY(0) scale(1) rotate(0deg);
            }
            100% {
                opacity: 0;
                transform: translateY(-180px) scale(0.4) rotate(40deg);
            }
        }

        /* pulse for dirty teeth */
        .tooth.dirty.pulse {
            animation: pulse-dirty 1s ease-in-out 2;
        }

        @keyframes pulse-dirty {
            0%,
            100% {
                transform: scale(1);
            }
            50% {
                transform: scale(1.08);
                border-color: #ffab00;
                box-shadow: 0 0 20px rgba(255, 171, 0, 0.3);
            }
        }

        .tooth.cavity.pulse {
            animation: pulse-cavity 0.8s ease-in-out 2;
        }

        @keyframes pulse-cavity {
            0%,
            100% {
                transform: scale(1);
            }
            50% {
                transform: scale(1.06);
                border-color: #d32f2f;
                box-shadow: 0 0 20px rgba(211, 47, 47, 0.25);
            }
        }

        /* Tooth cleaned animation */
        .tooth.cleaning {
            animation: clean-pop 0.5s cubic-bezier(0.34, 1.56, 0.64, 1);
        }

        @keyframes clean-pop {
            0% {
                transform: scale(1);
            }
            30% {
                transform: scale(1.2) rotate(-6deg);
                box-shadow: 0 0 30px rgba(255, 215, 0, 0.4);
            }
            70% {
                transform: scale(0.9) rotate(4deg);
            }
            100% {
                transform: scale(1) rotate(0deg);
            }
        }

        /* ===== SCROLL BAR ===== */
        ::-webkit-scrollbar {
            width: 6px;
        }
        ::-webkit-scrollbar-track {
            background: transparent;
        }
        ::-webkit-scrollbar-thumb {
            background: #b8d4f0;
            border-radius: 10px;
        }
    </style>
</head>
<body>

    <div class="game-container" id="app">
        <!-- HEADER -->
        <div class="header">
            <div class="title-section">
                <span class="icon">🦷</span>
                <h1>Dokter <span>Gigi</span></h1>
            </div>
            <div class="score-board">
                <span class="label">⭐ Skor</span>
                <span class="value" id="scoreDisplay">0</span>
            </div>
        </div>

        <!-- PATIENT -->
        <div class="patient-info">
            <div class="patient-avatar">
                <span class="face" id="patientFace">😁</span>
                <div class="name">
                    <span id="patientName">Pasien</span>
                    <small id="patientStatusLabel">• Perawatan</small>
                </div>
            </div>
            <div class="patient-status">
                <span class="label">🦷 Gigi</span>
                <span class="tooth-count" id="toothCount">0/0</span>
            </div>
        </div>

        <!-- MOUTH -->
        <div class="mouth-container" id="mouthContainer">
            <div class="tooth-row" id="upperRow"></div>
            <div class="tooth-row" id="lowerRow"></div>
        </div>

        <!-- TOOLS -->
        <div class="tools-section">
            <span class="label">🧰 Alat:</span>
            <button class="tool-btn toothbrush active" data-tool="brush" id="toolBrush">
                <span class="emoji">🪥</span> Sikat
            </button>
            <button class="tool-btn scraper" data-tool="scraper" id="toolScraper">
                <span class="emoji">🔧</span> Scraper
            </button>
            <button class="tool-btn drill" data-tool="drill" id="toolDrill">
                <span class="emoji">🦷</span> Bor
            </button>
        </div>

        <!-- INFO BAR -->
        <div class="info-bar">
            <div class="message-box" id="messageBox">
                🪥 Klik gigi kotor untuk membersihkan!
            </div>
            <button class="btn-reset" id="resetBtn">🔄 Pasien Baru</button>
        </div>
    </div>

    <script>
        // ============================================================
        //  DATA
        // ============================================================
        const PATIENT_NAMES = [
            'Andi', 'Budi', 'Cinta', 'Dewi', 'Eko', 'Fajar',
            'Gita', 'Hana', 'Irfan', 'Joko', 'Kiki', 'Lina',
            'Maya', 'Niko', 'Oki', 'Putri', 'Rizky', 'Sari',
            'Tono', 'Umi', 'Vino', 'Wati', 'Yudi', 'Zara'
        ];

        const PATIENT_FACES = ['😁', '😊', '😃', '😄', '😆', '😅', '🙂', '😉', '😌', '😏'];

        const TOOTH_EMOJIS = ['🦷', '🦷', '🦷', '🦷', '🦷', '🦷', '🦷', '🦷'];

        // ============================================================
        //  STATE
        // ============================================================
        let state = {
            teeth: [], // array of { id, row, col, state: 'clean'|'dirty'|'cavity'|'fixed' }
            selectedTool: 'brush',
            score: 0,
            patientIndex: 0,
            patientName: 'Pasien',
            patientFace: '😁',
            totalTeeth: 0,
            cleanCount: 0,
            isAnimating: false,
            patientCount: 0,
        };

        const ROWS = 2;
        const COLS = 8;

        // ============================================================
        //  DOM REFS
        // ============================================================
        const upperRow = document.getElementById('upperRow');
        const lowerRow = document.getElementById('lowerRow');
        const scoreDisplay = document.getElementById('scoreDisplay');
        const toothCount = document.getElementById('toothCount');
        const messageBox = document.getElementById('messageBox');
        const patientName = document.getElementById('patientName');
        const patientFace = document.getElementById('patientFace');
        const patientStatusLabel = document.getElementById('patientStatusLabel');

        const toolBtns = document.querySelectorAll('.tool-btn');
        const resetBtn = document.getElementById('resetBtn');

        // ============================================================
        //  HELPERS
        // ============================================================
        function randomInt(min, max) {
            return Math.floor(Math.random() * (max - min + 1)) + min;
        }

        function pick(arr) {
            return arr[Math.floor(Math.random() * arr.length)];
        }

        function shuffleArray(arr) {
            for (let i = arr.length - 1; i > 0; i--) {
                const j = randomInt(0, i);
                [arr[i], arr[j]] = [arr[j], arr[i]];
            }
            return arr;
        }

        // ============================================================
        //  GENERATE TEETH
        // ============================================================
        function generateTeeth(difficulty = 1) {
            const teeth = [];
            const total = ROWS * COLS;

            // Base dirty count depends on difficulty
            const dirtyBase = Math.min(6 + difficulty * 2, total - 2);
            const cavityBase = Math.min(1 + Math.floor(difficulty / 2), 4);

            let dirtyCount = Math.min(dirtyBase, total - 2);
            let cavityCount = Math.min(cavityBase, Math.floor(dirtyCount / 3));

            // Ensure we have at least some clean teeth
            let cleanCount = total - dirtyCount - cavityCount;
            if (cleanCount < 2) {
                // reduce dirty/cavity
                const excess = 2 - cleanCount;
                dirtyCount = Math.max(0, dirtyCount - excess);
                cleanCount = total - dirtyCount - cavityCount;
            }

            // Build state array
            const states = [];
            for (let i = 0; i < cleanCount; i++) states.push('clean');
            for (let i = 0; i < dirtyCount; i++) states.push('dirty');
            for (let i = 0; i < cavityCount; i++) states.push('cavity');

            shuffleArray(states);

            let idx = 0;
            for (let r = 0; r < ROWS; r++) {
                for (let c = 0; c < COLS; c++) {
                    teeth.push({
                        id: `t-${r}-${c}`,
                        row: r,
                        col: c,
                        state: states[idx] || 'clean',
                    });
                    idx++;
                }
            }

            return teeth;
        }

        // ============================================================
        //  RENDER
        // ============================================================
        function renderTooth(toothData) {
            const div = document.createElement('div');
            div.className = `tooth ${toothData.state}`;
            div.dataset.id = toothData.id;
            div.dataset.row = toothData.row;
            div.dataset.col = toothData.col;
            div.dataset.state = toothData.state;

            // Add stain dots for dirty
            if (toothData.state === 'dirty') {
                const s1 = document.createElement('span');
                s1.className = 'stain';
                const s2 = document.createElement('span');
                s2.className = 'stain';
                div.appendChild(s1);
                div.appendChild(s2);
            }

            // Add click handler
            div.addEventListener('click', () => handleToothClick(toothData.id));

            return div;
        }

        function renderAll() {
            upperRow.innerHTML = '';
            lowerRow.innerHTML = '';

            const upperTeeth = state.teeth.filter(t => t.row === 0);
            const lowerTeeth = state.teeth.filter(t => t.row === 1);

            // Sort by col
            upperTeeth.sort((a, b) => a.col - b.col);
            lowerTeeth.sort((a, b) => a.col - b.col);

            upperTeeth.forEach(t => {
                upperRow.appendChild(renderTooth(t));
            });
            lowerTeeth.forEach(t => {
                lowerRow.appendChild(renderTooth(t));
            });

            // Update counts
            const total = state.teeth.length;
            const clean = state.teeth.filter(t => t.state === 'clean' || t.state === 'fixed').length;
            state.totalTeeth = total;
            state.cleanCount = clean;
            toothCount.textContent = `${clean}/${total}`;

            // Update patient status
            if (clean === total) {
                patientStatusLabel.textContent = '✅ Selesai!';
                patientFace.textContent = '😄';
                patientFace.className = 'face happy';
                setTimeout(() => { patientFace.className = 'face'; }, 700);
                messageBox.innerHTML = '🎉 Semua gigi bersih! Klik "Pasien Baru" untuk lanjut!';
                // Celebrate
                if (!state.isAnimating) {
                    celebrate();
                }
            } else {
                patientStatusLabel.textContent = `🦷 ${total - clean} gigi tersisa`;
                // Face based on progress
                const ratio = clean / total;
                if (ratio > 0.7) patientFace.textContent = '😊';
                else if (ratio > 0.4) patientFace.textContent = '😐';
                else patientFace.textContent = '😣';
                patientFace.className = 'face';
            }

            // Update score
            scoreDisplay.textContent = state.score;

            // Update tool active state
            toolBtns.forEach(btn => {
                btn.classList.toggle('active', btn.dataset.tool === state.selectedTool);
            });
        }

        // ============================================================
        //  GAME LOGIC
        // ============================================================
        function handleToothClick(toothId) {
            if (state.isAnimating) return;

            const tooth = state.teeth.find(t => t.id === toothId);
            if (!tooth) return;

            const tool = state.selectedTool;

            // Already clean / fixed
            if (tooth.state === 'clean' || tooth.state === 'fixed') {
                messageBox.innerHTML = '✨ Gigi ini sudah bersih!';
                return;
            }

            // Tool-specific actions
            if (tool === 'brush') {
                if (tooth.state === 'dirty') {
                    // Clean it!
                    tooth.state = 'clean';
                    state.score += 10;
                    messageBox.innerHTML = '🪥 Gigi berhasil dibersihkan! +10 poin ✨';
                    animateTooth(toothId, 'cleaning');
                    celebrateMini();
                    renderAll();
                    checkPatientComplete();
                } else if (tooth.state === 'cavity') {
                    messageBox.innerHTML = '⚠️ Sikat tidak cukup! Gunakan Bor untuk lubang.';
                    toothPulse(toothId, 'cavity');
                } else {
                    messageBox.innerHTML = '🤔 Gigi ini sudah bersih.';
                }
            } else if (tool === 'scraper') {
                if (tooth.state === 'dirty') {
                    tooth.state = 'clean';
                    state.score += 15;
                    messageBox.innerHTML = '🔧 Plak berhasil dikikis! +15 poin ✨';
                    animateTooth(toothId, 'cleaning');
                    celebrateMini();
                    renderAll();
                    checkPatientComplete();
                } else if (tooth.state === 'cavity') {
                    messageBox.innerHTML = '⚠️ Scraper tidak bisa menambal lubang. Pakai Bor!';
                    toothPulse(toothId, 'cavity');
                } else {
                    messageBox.innerHTML = '🧹 Gigi ini sudah bersih.';
                }
            } else if (tool === 'drill') {
                if (tooth.state === 'cavity') {
                    tooth.state = 'fixed';
                    state.score += 25;
                    messageBox.innerHTML = '🦷 Lubang berhasil ditambal! +25 poin ⭐';
                    animateTooth(toothId, 'cleaning');
                    celebrateMini();
                    renderAll();
                    checkPatientComplete();
                } else if (tooth.state === 'dirty') {
                    messageBox.innerHTML = '⚠️ Bor tidak untuk membersihkan! Pakai Sikat atau Scraper.';
                    toothPulse(toothId, 'dirty');
                } else {
                    messageBox.innerHTML = '✨ Gigi ini sudah sehat.';
                }
            }

            renderAll();
        }

        function animateTooth(toothId, className) {
            const el = document.querySelector(`.tooth[data-id="${toothId}"]`);
            if (el) {
                el.classList.add(className);
                setTimeout(() => el.classList.remove(className), 600);
            }
        }

        function toothPulse(toothId, type) {
            const el = document.querySelector(`.tooth[data-id="${toothId}"]`);
            if (el) {
                el.classList.add('pulse');
                setTimeout(() => el.classList.remove('pulse'), 1200);
            }
        }

        function checkPatientComplete() {
            const total = state.teeth.length;
            const clean = state.teeth.filter(t => t.state === 'clean' || t.state === 'fixed').length;
            if (clean === total) {
                // All teeth are clean!
                state.score += 50;
                messageBox.innerHTML = '🎉 Pasien sembuh total! +50 poin bonus! 🎉';
                celebrate();
                renderAll();
            }
        }

        // ============================================================
        //  CELEBRATIONS
        // ============================================================
        function celebrate() {
            state.isAnimating = true;
            const emojis = ['🎉', '⭐', '🦷', '✨', '🌟', '💫', '🎊', '❤️'];
            for (let i = 0; i < 18; i++) {
                setTimeout(() => {
                    const el = document.createElement('div');
                    el.className = 'celebration';
                    el.textContent = pick(emojis);
                    el.style.left = randomInt(10, 90) + '%';
                    el.style.top = randomInt(10, 70) + '%';
                    el.style.fontSize = randomInt(28, 56) + 'px';
                    document.body.appendChild(el);
                    setTimeout(() => el.remove(), 2000);
                }, i * 100);
            }
            setTimeout(() => {
                state.isAnimating = false;
            }, 2200);
        }

        function celebrateMini() {
            const emojis = ['✨', '⭐', '🦷', '🌟'];
            for (let i = 0; i < 5; i++) {
                setTimeout(() => {
                    const el = document.createElement('div');
                    el.className = 'celebration';
                    el.textContent = pick(emojis);
                    el.style.left = randomInt(20, 80) + '%';
                    el.style.top = randomInt(20, 60) + '%';
                    el.style.fontSize = randomInt(20, 36) + 'px';
                    document.body.appendChild(el);
                    setTimeout(() => el.remove(), 1500);
                }, i * 80);
            }
        }

        // ============================================================
        //  NEW PATIENT
        // ============================================================
        function newPatient() {
            // Increase difficulty with each patient
            state.patientCount++;
            const difficulty = Math.min(1 + Math.floor(state.patientCount / 2), 5);

            state.teeth = generateTeeth(difficulty);
            state.patientName = pick(PATIENT_NAMES);
            state.patientFace = pick(PATIENT_FACES);

            // Reset some state
            patientName.textContent = state.patientName;
            patientFace.textContent = state.patientFace;
            patientFace.className = 'face';

            // Random message
            const msgs = [
                '🪥 Ayo bersihkan gigi pasien!',
                '🦷 Gigi kotor menunggu perawatan!',
                '🧼 Saatnya membersihkan plak!',
                '⭐ Jadilah dokter gigi terbaik!',
                '🔧 Periksa gigi pasien dengan teliti!',
            ];
            messageBox.innerHTML = pick(msgs);

            renderAll();
        }

        // ============================================================
        //  TOOL SELECTION
        // ============================================================
        toolBtns.forEach(btn => {
            btn.addEventListener('click', () => {
                state.selectedTool = btn.dataset.tool;
                toolBtns.forEach(b => b.classList.remove('active'));
                btn.classList.add('active');

                const toolName = {
                    brush: 'Sikat Gigi 🪥',
                    scraper: 'Scraper 🔧',
                    drill: 'Bor Gigi 🦷'
                } [state.selectedTool] || 'Alat';

                messageBox.innerHTML = `🔧 Menggunakan: <strong>${toolName}</strong>`;
                renderAll();
            });
        });

        // ============================================================
        //  RESET
        // ============================================================
        resetBtn.addEventListener('click', () => {
            newPatient();
        });

        // ============================================================
        //  INIT
        // ============================================================
        function init() {
            state.score = 0;
            state.patientCount = 0;
            state.selectedTool = 'brush';
            state.isAnimating = false;

            // Set default tool active
            toolBtns.forEach(b => b.classList.remove('active'));
            document.querySelector('.tool-btn.toothbrush').classList.add('active');

            newPatient();
            renderAll();
        }

        // ============================================================
        //  KEYBOARD SHORTCUTS
        // ============================================================
        document.addEventListener('keydown', (e) => {
            if (e.key === '1') {
                document.querySelector('.tool-btn.toothbrush')?.click();
            } else if (e.key === '2') {
                document.querySelector('.tool-btn.scraper')?.click();
            } else if (e.key === '3') {
                document.querySelector('.tool-btn.drill')?.click();
            } else if (e.key === 'r' || e.key === 'R') {
                resetBtn.click();
            }
        });

        // ============================================================
        //  START
        // ============================================================
        init();

        console.log('🦷 Dokter Gigi — Game siap!');
        console.log('📌 Gunakan tombol 1, 2, 3 untuk ganti alat.');
        console.log('📌 Tekan R untuk pasien baru.');
    </script>

</body>
</html>
