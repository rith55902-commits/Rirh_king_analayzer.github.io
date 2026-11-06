<!DOCTYPE html>
<html lang="km">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>RITH KING ANALYZER PRO - ULTIMATE EDITION</title>
    <style>
        :root {
            --bg-dark: #090d16;
            --panel-bg: #111827;
            --card-bg: #1f2937;
            --accent-primary: #fbbf24;
            --accent-cyan: #06b6d4;
            --green-signal: #22c55e;
            --red-signal: #ef4444;
            --text-main: #f9fafb;
            --text-sub: #9ca3af;
            --border-color: #374151;
        }

        body.theme-cyan { --accent-primary: #06b6d4; --panel-bg: #0f172a; --card-bg: #1e293b; }
        body.theme-matrix { --accent-primary: #22c55e; --panel-bg: #051407; --card-bg: #0d2612; }
        body.theme-purple { --accent-primary: #a855f7; --panel-bg: #180d29; --card-bg: #281745; }

        * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; }

        body {
            background-color: var(--bg-dark);
            color: var(--text-main);
            height: 100vh;
            overflow: hidden;
            display: flex;
            flex-direction: column;
            transition: all 0.3s ease;
        }

        #authOverlay {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(9, 13, 22, 0.96);
            z-index: 9999;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        .auth-box {
            background: var(--panel-bg);
            border: 1px solid var(--border-color);
            padding: 30px 25px;
            border-radius: 16px;
            width: 380px;
            text-align: center;
            box-shadow: 0 20px 40px rgba(0,0,0,0.7);
        }
        .auth-box h2 { color: var(--accent-primary); font-size: 22px; margin-bottom: 6px; }
        .auth-box p { font-size: 12px; color: var(--text-sub); margin-bottom: 20px; }

        .auth-btn {
            width: 100%;
            padding: 12px;
            margin-bottom: 10px;
            border: 1px solid var(--border-color);
            border-radius: 8px;
            font-size: 13px;
            font-weight: 600;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            transition: 0.2s;
        }

        .btn-google { background-color: #ffffff; color: #1f2937; border-color: #d1d5db; }
        .btn-google:hover { background-color: #f3f4f6; }

        .btn-facebook { background-color: #1877f2; color: #ffffff; border-color: #1877f2; }
        .btn-facebook:hover { background-color: #166fe5; }

        .btn-apple { background-color: #000000; color: #ffffff; border-color: #000000; }
        .btn-apple:hover { background-color: #111827; }

        .vip-key-box { margin-top: 15px; border-top: 1px solid var(--border-color); padding-top: 15px; }
        .vip-key-box input {
            width: 100%;
            background: #0d1117;
            border: 1px solid var(--accent-primary);
            color: var(--text-main);
            padding: 8px;
            border-radius: 6px;
            font-size: 11px;
            text-align: center;
            margin-bottom: 8px;
        }
        .btn-vip {
            width: 100%;
            background: linear-gradient(135deg, #f59e0b, #d97706);
            color: #000;
            font-weight: bold;
            padding: 8px;
            border: none;
            border-radius: 6px;
            font-size: 11px;
            cursor: pointer;
            text-transform: uppercase;
        }

        .top-navbar {
            background-color: var(--panel-bg);
            border-bottom: 1px solid var(--border-color);
            padding: 10px 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            height: 60px;
        }

        .brand-logo { display: flex; align-items: center; gap: 10px; }
        .brand-logo h1 { font-size: 18px; color: var(--accent-primary); letter-spacing: 1px; text-transform: uppercase; }

        .system-status { display: flex; align-items: center; gap: 8px; font-size: 11px; color: var(--text-sub); }
        .nav-select {
            background-color: var(--card-bg);
            color: var(--text-main);
            border: 1px solid var(--border-color);
            padding: 4px 6px;
            border-radius: 4px;
            font-size: 10px;
            cursor: pointer;
        }

        .status-badge {
            background-color: rgba(34, 197, 94, 0.15);
            color: var(--green-signal);
            padding: 3px 8px;
            border-radius: 20px;
            border: 1px solid var(--green-signal);
            font-weight: bold;
        }

        .terminal-container {
            display: grid;
            grid-template-columns: 22% 36% 42%;
            height: calc(100vh - 60px);
            width: 100%;
        }

        @media(max-width: 1200px) {
            .terminal-container { grid-template-columns: 40% 60%; }
            .watchlist-pane { display: none; }
        }

        .watchlist-pane {
            background-color: var(--panel-bg);
            border-right: 1px solid var(--border-color);
            padding: 10px;
            overflow-y: auto;
            display: flex;
            flex-direction: column;
            gap: 8px;
        }

        .watch-item {
            background-color: var(--card-bg);
            border: 1px solid var(--border-color);
            padding: 10px;
            border-radius: 6px;
            cursor: pointer;
            transition: 0.2s;
        }
        .watch-item:hover { border-color: var(--accent-primary); background: #263548; }
        .watch-top { display: flex; justify-content: space-between; font-weight: bold; font-size: 11px; margin-bottom: 3px; }
        .watch-price { font-size: 12px; color: var(--accent-cyan); }
        .watch-chg { font-size: 10px; font-weight: bold; }
        .chg-pos { color: var(--green-signal); }
        .chg-neg { color: var(--red-signal); }

        .chart-pane {
            border-right: 1px solid var(--border-color);
            display: flex;
            flex-direction: column;
            background-color: #0d1117;
        }

        .chart-toolbar {
            background-color: var(--panel-bg);
            padding: 8px 15px;
            display: flex;
            gap: 12px;
            align-items: center;
            border-bottom: 1px solid var(--border-color);
        }

        .asset-select {
            background-color: var(--card-bg);
            color: var(--text-main);
            border: 1px solid var(--border-color);
            padding: 6px 12px;
            border-radius: 6px;
            font-size: 13px;
            cursor: pointer;
        }

        .chart-container { flex: 1; width: 100%; height: 100%; display: grid; grid-template-columns: 1fr; }
        .chart-container.split-2 { grid-template-columns: 1fr 1fr; }

        .side-pane {
            background-color: var(--panel-bg);
            padding: 10px;
            overflow-y: auto;
            display: flex;
            flex-direction: column;
            gap: 8px;
        }

        .panel-card {
            background-color: var(--card-bg);
            border: 1px solid var(--border-color);
            border-radius: 8px;
            padding: 8px 10px;
        }

        .panel-header {
            font-size: 11px;
            font-weight: bold;
            color: var(--accent-primary);
            margin-bottom: 6px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .support-box {
            background: rgba(6, 182, 212, 0.08);
            border: 1px solid rgba(6, 182, 212, 0.3);
            padding: 6px 8px;
            border-radius: 6px;
            font-size: 10px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .support-box a { color: var(--accent-cyan); text-decoration: none; font-weight: bold; }

        .news-live-box {
            background: linear-gradient(135deg, rgba(239, 68, 68, 0.15), rgba(15, 23, 42, 0.6));
            border: 1px solid rgba(239, 68, 68, 0.4);
            padding: 6px 8px;
            border-radius: 6px;
            font-size: 10px;
            display: flex;
            flex-direction: column;
            gap: 3px;
        }
        .news-item-row { display: flex; justify-content: space-between; align-items: center; border-bottom: 1px solid rgba(255,255,255,0.05); padding-bottom: 2px; }
        .news-time { font-family: monospace; color: var(--accent-primary); font-weight: bold; }

        .sessions-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 4px; }
        .session-item {
            background-color: rgba(0,0,0,0.3);
            border: 1px solid var(--border-color);
            padding: 4px;
            border-radius: 4px;
            text-align: center;
            font-size: 9px;
        }
        .session-item.active { border-color: var(--green-signal); background-color: rgba(34, 197, 94, 0.1); }
        .session-name { font-weight: bold; color: var(--text-main); }
        .session-status { font-size: 8px; margin-top: 1px; }

        .confluence-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 4px; margin-bottom: 6px; font-size: 9px; text-align: center; }
        .conf-box { background: rgba(0,0,0,0.3); border: 1px solid var(--border-color); padding: 4px; border-radius: 4px; }
        .conf-box.bull { color: var(--green-signal); border-color: var(--green-signal); }
        .conf-box.bear { color: var(--red-signal); border-color: var(--red-signal); }

        .signal-box {
            text-align: center;
            padding: 6px;
            border-radius: 6px;
            background-color: rgba(15, 23, 42, 0.6);
            border: 1px dashed var(--border-color);
            margin-bottom: 6px;
        }
        .signal-title { font-size: 15px; font-weight: bold; color: var(--accent-cyan); }
        .signal-confidence { font-size: 9px; color: var(--text-sub); }

        .metrics-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 4px; margin-bottom: 6px; }
        .metric-item {
            background-color: rgba(0,0,0,0.2);
            padding: 4px 6px;
            border-radius: 4px;
            border-left: 3px solid var(--accent-cyan);
        }
        .metric-item.sl { border-left-color: var(--red-signal); }
        .metric-label { font-size: 8px; color: var(--text-sub); text-transform: uppercase; }
        .metric-value { font-size: 10px; font-weight: bold; }

        .tp-list { display: flex; flex-direction: column; gap: 3px; margin-bottom: 6px; }
        .tp-item {
            display: flex;
            justify-content: space-between;
            background-color: rgba(34, 197, 94, 0.08);
            padding: 3px 6px;
            border-radius: 4px;
            font-size: 10px;
            border: 1px solid rgba(34, 197, 94, 0.2);
        }

        .rr-badge {
            background: rgba(6, 182, 212, 0.15);
            border: 1px solid var(--accent-cyan);
            color: var(--accent-cyan);
            padding: 4px;
            border-radius: 4px;
            font-size: 9px;
            text-align: center;
            margin-bottom: 6px;
            font-weight: bold;
        }

        .controls-flex { display: flex; gap: 5px; }
        .btn-run-ai {
            flex: 2;
            background: linear-gradient(135deg, #f59e0b, #d97706);
            color: #000;
            font-weight: bold;
            padding: 7px;
            border: none;
            border-radius: 6px;
            font-size: 11px;
            cursor: pointer;
            text-transform: uppercase;
        }
        .btn-auto-scan {
            flex: 1;
            background-color: var(--card-bg);
            border: 1px solid var(--accent-primary);
            color: var(--accent-primary);
            font-weight: bold;
            padding: 7px;
            border-radius: 6px;
            font-size: 10px;
            cursor: pointer;
        }
        .btn-auto-scan.active { background-color: var(--accent-primary); color: #000; }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 4px;
            background: rgba(0,0,0,0.2);
            padding: 6px;
            border-radius: 6px;
            margin-bottom: 6px;
            font-size: 9px;
            text-align: center;
        }

        .calc-inputs { display: grid; grid-template-columns: 1fr 1fr; gap: 6px; margin-bottom: 6px; }
        .calc-group label { display: block; font-size: 8px; color: var(--text-sub); margin-bottom: 1px; }
        .calc-group input {
            width: 100%;
            background-color: #0d1117;
            border: 1px solid var(--border-color);
            color: var(--text-main);
            padding: 3px 5px;
            border-radius: 4px;
            font-size: 10px;
        }

        .tg-inputs { display: flex; gap: 4px; margin-top: 4px; }
        .tg-inputs input {
            flex: 1;
            background: #0d1117;
            border: 1px solid var(--border-color);
            color: var(--text-main);
            padding: 4px;
            border-radius: 4px;
            font-size: 9px;
        }

        .history-table { width: 100%; border-collapse: collapse; font-size: 9px; margin-top: 4px; }
        .history-table th {
            text-align: left;
            color: var(--text-sub);
            padding: 3px;
            border-bottom: 1px solid var(--border-color);
            background-color: rgba(0,0,0,0.2);
        }
        .history-table td { padding: 4px 3px; border-bottom: 1px solid rgba(255,255,255,0.05); }

        .badge-buy { color: var(--green-signal); font-weight: bold; }
        .badge-sell { color: var(--red-signal); font-weight: bold; }

        .btn-action {
            padding: 1px 4px;
            font-size: 8px;
            border-radius: 3px;
            border: none;
            cursor: pointer;
            font-weight: bold;
        }
        .btn-win { background-color: rgba(34, 197, 94, 0.2); color: var(--green-signal); border: 1px solid var(--green-signal); }
        .btn-loss { background-color: rgba(239, 68, 68, 0.2); color: var(--red-signal); border: 1px solid var(--red-signal); }
        .btn-small { background: none; border: none; color: var(--accent-cyan); font-size: 9px; cursor: pointer; text-decoration: underline; }

        #toastContainer {
            position: fixed;
            bottom: 20px;
            right: 20px;
            z-index: 10000;
            display: flex;
            flex-direction: column;
            gap: 10px;
        }
        .toast {
            background: var(--panel-bg);
            border: 1px solid var(--accent-primary);
            color: var(--text-main);
            padding: 12px 18px;
            border-radius: 8px;
            font-size: 11px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.5);
            animation: slideIn 0.3s ease;
        }
        @keyframes slideIn {
            from { transform: translateX(100%); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }
    </style>
</head>
<body>

    <div id="authOverlay">
        <div class="auth-box">
            <h2>👑 RITH KING PRO</h2>
            <p>សូមចូលប្រើប្រាស់ប្រព័ន្ធវិភាគទីផ្សារ</p>
            
            <button class="auth-btn btn-google" onclick="loginWith('Google')">
                <svg width="16" height="16" viewBox="0 0 24 24"><path fill="#4285F4" d="M23.745 12.27c0-.7-.06-1.4-.19-2.07H12v4.51h6.6c-.29 1.52-1.14 2.82-2.4 3.68v3.05h3.88c2.27-2.09 3.665-5.17 3.665-9.17z"/><path fill="#34A853" d="M12 24c3.24 0 5.95-1.08 7.93-2.91l-3.88-3.05c-1.08.72-2.45 1.16-4.05 1.16-3.13 0-5.78-2.11-6.73-4.96H1.18v3.15C3.15 21.32 7.23 24 12 24z"/><path fill="#FBBC05" d="M5.27 14.24c-.25-.72-.38-1.49-.38-2.24s.13-1.52.38-2.24V6.61H1.18C.43 8.12 0 9.99 0 12s.43 3.88 1.18 5.39l4.09-3.15z"/><path fill="#EA4335" d="M12 4.75c1.77 0 3.35.61 4.6 1.8l3.42-3.42C17.95 1.19 15.24 0 12 0 7.23 0 3.15 2.68 1.18 6.61l4.09 3.15c.95-2.85 3.6-4.96 6.73-4.96z"/></svg>
                បន្តជាមួយ Gmail (Google)
            </button>

            <button class="auth-btn btn-facebook" onclick="loginWith('Facebook')">
                <svg width="16" height="16" fill="currentColor" viewBox="0 0 24 24"><path d="M24 12.073c0-6.627-5.373-12-12-12s-12 5.373-12 12c0 5.99 4.388 10.954 10.125 11.854v-8.385H7.078v-3.47h3.047V9.43c0-3.007 1.792-4.669 4.533-4.669 1.312 0 2.686.235 2.686.235v2.953H15.83c-1.491 0-1.956.925-1.956 1.874v2.25h3.328l-.532 3.47h-2.796v8.385C19.612 23.027 24 18.062 24 12.073z"/></svg>
                បន្តជាមួយ Facebook
            </button>

            <button class="auth-btn btn-apple" onclick="loginWith('Apple')">
                <svg width="16" height="16" fill="currentColor" viewBox="0 0 24 24"><path d="M18.71 19.5c-.83 1.24-1.71 2.45-3.05 2.47-1.34.03-1.77-.79-3.29-.79-1.53 0-2 .77-3.27.82-1.31.05-2.3-1.32-3.14-2.53C4.25 17 2.94 12.45 4.7 9.39c.87-1.52 2.43-2.48 4.12-2.51 1.28-.02 2.5.87 3.29.87.78 0 2.26-1.07 3.81-.91.65.03 2.47.26 3.64 1.98-.09.06-2.17 1.28-2.15 3.81.03 3.02 2.65 4.03 2.68 4.04-.03.07-.42 1.44-1.38 2.83M15.97 5.75c.62-.75 1.04-1.79.93-2.83-.92.04-2.03.62-2.69 1.37-.58.65-1.09 1.71-.95 2.74 1.03.08 2.09-.53 2.71-1.28z"/></svg>
                បន្តជាមួយ Apple ID
            </button>

            <div class="vip-key-box">
                <input type="text" id="vipKeyInput" placeholder="បញ្ចូល VIP License Key (Optional)">
                <button class="btn-vip" onclick="verifyVipKey()">ផ្ទៀងផ្ទាត់ VIP Key</button>
            </div>
        </div>
    </div>

    <div class="top-navbar">
        <div class="brand-logo">
            <span>👑</span>
            <h1 id="txtBrand">RITH KING ANALYZER PRO</h1>
        </div>
        <div class="system-status">
            <span id="userProfileDisplay" style="color:var(--accent-primary); font-weight:bold; font-size:11px;">👤 Rith Admin (FREE)</span>
            <select class="nav-select" id="soundSelect" onchange="changeSoundMode()">
                <option value="beep">🔊 Beep Sound</option>
                <option value="chime">🔔 Chime</option>
                <option value="mute">🔇 Mute</option>
            </select>
            <select class="nav-select" id="langSelect" onchange="changeLanguage()">
                <option value="km">🇰🇭 ភាសាខ្មែរ</option>
                <option value="en">🇺🇸 English</option>
            </select>
            <select class="nav-select" id="themeSelect" onchange="changeTheme()">
                <option value="gold">👑 Gold</option>
                <option value="cyan">🩵 Cyan</option>
                <option value="matrix">🟢 Matrix</option>
                <option value="purple">🟣 Purple</option>
            </select>
            <button class="nav-select" onclick="toggleSplitView()" style="background:var(--accent-primary); color:#000; font-weight:bold;">🪟 Split View</button>
            <span class="status-badge" id="systemStateBadge">Online</span>
        </div>
    </div>

    <div class="terminal-container">
        
        <div class="watchlist-pane">
            <div class="panel-header"><span id="txtWatchHeader">📊 LIVE WATCHLIST</span></div>
            <div id="watchlistContainer">
                <div class="watch-item" onclick="selectWatchAsset('XAUUSD', 'OANDA:XAUUSD')">
                    <div class="watch-top"><span>XAUUSD</span> <span class="watch-chg chg-pos" id="wChg_XAUUSD">+0.45%</span></div>
                    <div class="watch-price" id="wPrice_XAUUSD">$4,062.50</div>
                </div>
                <div class="watc
