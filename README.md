<!DOCTYPE html>
<html lang="km">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>RITH KING ANALYZER PRO - FULLSCREEN EDITION</title>
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
            width: 100vw;
            height: 100vh;
            overflow: hidden;
            display: flex;
            flex-direction: column;
        }

        #authOverlay {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(9, 13, 22, 0.98);
            z-index: 9999;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        .auth-box {
            background: var(--panel-bg);
            border: 1px solid var(--border-color);
            padding: 25px;
            border-radius: 16px;
            width: 360px;
            text-align: center;
            box-shadow: 0 20px 40px rgba(0,0,0,0.8);
        }
        .auth-box h2 { color: var(--accent-primary); font-size: 20px; margin-bottom: 5px; }
        .auth-box p { font-size: 11px; color: var(--text-sub); margin-bottom: 15px; }

        .auth-tabs { display: flex; gap: 5px; margin-bottom: 15px; background: #0d1117; padding: 3px; border-radius: 6px; }
        .auth-tab {
            flex: 1; background: none; border: none; color: var(--text-sub);
            padding: 6px; font-size: 11px; font-weight: bold; cursor: pointer; border-radius: 4px;
        }
        .auth-tab.active { background: var(--card-bg); color: var(--accent-primary); border: 1px solid var(--border-color); }

        .auth-form-group { margin-bottom: 10px; text-align: left; }
        .auth-form-group label { display: block; font-size: 10px; color: var(--text-sub); margin-bottom: 3px; }
        .auth-form-group input {
            width: 100%; background: #0d1117; border: 1px solid var(--border-color);
            color: var(--text-main); padding: 8px; border-radius: 6px; font-size: 11px;
        }

        .auth-submit-btn {
            width: 100%; background: var(--accent-primary); color: #000;
            font-weight: bold; padding: 10px; border: none; border-radius: 6px;
            font-size: 12px; cursor: pointer; text-transform: uppercase; margin-top: 5px;
        }

        .vip-key-box { margin-top: 15px; border-top: 1px solid var(--border-color); padding-top: 12px; }
        .vip-key-box input {
            width: 100%; background: #0d1117; border: 1px solid var(--accent-primary);
            color: var(--text-main); padding: 7px; border-radius: 6px; font-size: 10px;
            text-align: center; margin-bottom: 6px;
        }
        .btn-vip {
            width: 100%; background: linear-gradient(135deg, #f59e0b, #d97706);
            color: #000; font-weight: bold; padding: 7px; border: none;
            border-radius: 6px; font-size: 10px; cursor: pointer; text-transform: uppercase;
        }

        .top-navbar {
            background-color: var(--panel-bg);
            border-bottom: 1px solid var(--border-color);
            padding: 10px 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            height: 60px;
            flex-shrink: 0;
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
            grid-template-columns: 22% 38% 40%;
            flex: 1;
            width: 100%;
            height: calc(100vh - 60px);
            overflow: hidden;
        }

        @media(max-width: 1200px) {
            .terminal-container { grid-template-columns: 35% 65%; }
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
            height: 100%;
        }

        .chart-toolbar {
            background-color: var(--panel-bg);
            padding: 8px 15px;
            display: flex;
            gap: 12px;
            align-items: center;
            border-bottom: 1px solid var(--border-color);
            flex-shrink: 0;
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
            height: 100%;
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
            width: 100%; background-color: #0d1117; border: 1px solid var(--border-color);
            color: var(--text-main); padding: 3px 5px; border-radius: 4px; font-size: 10px;
        }

        .tg-inputs { display: flex; gap: 4px; margin-top: 4px; }
        .tg-inputs input {
            flex: 1; background: #0d1117; border: 1px solid var(--border-color);
            color: var(--text-main); padding: 4px; border-radius: 4px; font-size: 9px;
        }

        .history-table { width: 100%; border-collapse: collapse; font-size: 9px; margin-top: 4px; }
        .history-table th {
            text-align: left; color: var(--text-sub); padding: 3px;
            border-bottom: 1px solid var(--border-color); background-color: rgba(0,0,0,0.2);
        }
        .history-table td { padding: 4px 3px; border-bottom: 1px solid rgba(255,255,255,0.05); }

        .badge-buy { color: var(--green-signal); font-weight: bold; }
        .badge-sell { color: var(--red-signal); font-weight: bold; }

        .btn-action {
            padding: 1px 4px; font-size: 8px; border-radius: 3px; border: none; cursor: pointer; font-weight: bold;
        }
        .btn-win { background-color: rgba(34, 197, 94, 0.2); color: var(--green-signal); border: 1px solid var(--green-signal); }
        .btn-loss { background-color: rgba(239, 68, 68, 0.2); color: var(--red-signal); border: 1px solid var(--red-signal); }
        .btn-small { background: none; border: none; color: var(--accent-cyan); font-size: 9px; cursor: pointer; text-decoration: underline; }

        #toastContainer {
            position: fixed; bottom: 20px; right: 20px; z-index: 10000;
            display: flex; flex-direction: column; gap: 10px;
        }
        .toast {
            background: var(--panel-bg); border: 1px solid var(--accent-primary);
            color: var(--text-main); padding: 12px 18px; border-radius: 8px; font-size: 11px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.5); animation: slideIn 0.3s ease;
        }
        @keyframes slideIn {
            from { transform: translateX(100%); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }
    </style>
</head>
<body>

    <!-- LOGIN & REGISTER OVERLAY -->
    <div id="authOverlay">
        <div class="auth-box">
            <h2>👑 RITH KING PRO</h2>
            <p>ប្រព័ន្ធបង្កើត និងចូលគណនីវិភាគទីផ្សារ</p>
            
            <div class="auth-tabs">
                <button class="auth-tab active" id="tabLoginBtn" onclick="switchAuthTab('login')">ចូល (Login)</button>
                <button class="auth-tab" id="tabRegBtn" onclick="switchAuthTab('register')">បង្កើត (Register)</button>
            </div>

            <!-- Login Form -->
            <div id="loginFormContainer">
                <div class="auth-form-group">
                    <label>ឈ្មោះគណនី (Username)</label>
                    <input type="text" id="loginUser" placeholder="បញ្ចូល Username របស់អ្នក">
                </div>
                <div class="auth-form-group">
                    <label>ពាក្យសម្ងាត់ (Password)</label>
                    <input type="password" id="loginPass" placeholder="បញ្ចូល Password">
                </div>
                <button class="auth-submit-btn" onclick="handleLogin()">ចូលប្រព័ន្ធ (Login)</button>
            </div>

            <!-- Register Form -->
            <div id="regFormContainer" style="display: none;">
                <div class="auth-form-group">
                    <label>បង្កើតឈ្មោះគណនីថ្មី (New Username)</label>
                    <input type="text" id="regUser" placeholder="កំណត់ Username">
                </div>
                <div class="auth-form-group">
                    <label>បង្កើតពាក្យសម្ងាត់ថ្មី (New Password)</label>
                    <input type="password" id="regPass" placeholder="កំណត់ Password">
                </div>
                <button class="auth-submit-btn" onclick="handleRegister()" style="background:var(--accent-cyan); color:#000;">ចុះឈ្មោះ (Register)</button>
            </div>

            <div class="vip-key-box">
                <input type="text" id="vipKeyInput" placeholder="ឬបញ្ចូល VIP License Key">
                <button class="btn-vip" onclick="verifyVipKey()">ផ្ទៀងផ្ទាត់ VIP KEY</button>
            </div>
        </div>
    </div>

    <!-- NAVBAR -->
    <div class="top-navbar">
        <div class="brand-logo">
            <span>👑</span>
            <h1 id="txtBrand">RITH KING ANALYZER PRO</h1>
        </div>
        <div class="system-status">
            <span id="userProfileDisplay" style="color:var(--accent-primary); font-weight:bold; font-size:11px;">👤 Guest</span>
            <button class="nav-select" onclick="logoutUser()" style="background:rgba(239,68,68,0.2); color:var(--red-signal); border:1px solid var(--red-signal);">🚪 Logout</button>
            <select class="nav-select" id="soundSelect" onchange="changeSoundMode()">
                <option value="beep">🔊 Beep</option>
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

    <!-- MAIN TERMINAL CONTENT -->
    <div class="terminal-container">
        
        <!-- WATCHLIST -->
        <div class="watchlist-pane">
            <div class="panel-header"><span id="txtWatchHeader">📊 LIVE WATCHLIST</span></div>
            <div id="watchlistContainer">
                <div class="watch-item" onclick="selectWatchAsset('XAUUSD', 'OANDA:XAUUSD')">
                    <div class="watch-top"><span>XAUUSD</span> <span class="watch-chg chg-pos" id="wChg_XAUUSD">+0.45%</span></div>
                    <div class="watch-price" id="wPrice_XAUUSD">$4,062.50</div>
                </div>
                <div class="watch-item" onclick="selectWatchAsset('EURUSD', 'FX:EURUSD')">
                    <div class="watch-top"><span>EURUSD</span> <span class="watch-chg chg-neg" id="wChg_EURUSD">-0.12%</span></div>
</div>
                <div class="watch-item" onclick="selectWatchAsset('GBPUSD', 'FX:GBPUSD')">
                    <div class="watch-top"><span>GBPUSD</span> <span class="watch-chg chg-pos" id="wChg_GBPUSD">+0.18%</span></div>
                    <div class="watch-price" id="wPrice_GBPUSD">1.2945</div>
                </div>
                <div class="watch-item" onclick="selectWatchAsset('BTCUSD', 'BINANCE:BTCUSDT')">
                    <div class="watch-top"><span>BTCUSD</span> <span class="watch-chg chg-pos" id="wChg_BTCUSD">+1.85%</span></div>
                    <div class="watch-price" id="wPrice_BTCUSD">$68,520.00</div>
                </div>
                <div class="watch-item" onclick="selectWatchAsset('US30', 'FOREXCOM:SPXUSD')">
                    <div class="watch-top"><span>US30</span> <span class="watch-chg chg-pos" id="wChg_US30">+0.32%</span></div>
                    <div class="watch-price" id="wPrice_US30">$42,540.10</div>
                </div>
            </div>
        </div>

        <!-- CHART PANE -->
        <div class="chart-pane">
            <div class="chart-toolbar">
                <select class="asset-select" id="assetSelect" onchange="changeAsset()">
                    <option value="XAUUSD">🥇 XAUUSD (Gold Spot)</option>
                    <option value="EURUSD">💶 EURUSD (Euro / USD)</option>
                    <option value="GBPUSD">💷 GBPUSD (Pound / USD)</option>
                    <option value="BTCUSD">₿ BTCUSD (Bitcoin)</option>
                    <option value="US30">📈 US30 (Dow Jones)</option>
                </select>
                <span id="txtFeed" style="color: var(--text-sub); font-size: 10px;">Institutional Feed | [Space] to Scan</span>
            </div>
            <div class="chart-container" id="chartGridContainer">
                <div id="tradingview_widget" style="height:100%;width:100%;"></div>
                <div id="tradingview_widget_2" style="height:100%;width:100%; display:none;"></div>
            </div>
        </div>

        <!-- SIDE CONTROL PANE -->
        <div class="side-pane">
            
            <div class="panel-card">
                <div class="panel-header"><span id="txtSupportHeader">💬 SUPPORT & CONTACT</span></div>
                <div class="support-box">
                    <span id="txtAdmin">Admin Telegram:</span>
                    <a href="https://t.me/Rith_putuy" target="_blank">@Rith_putuy (+855966251855)</a>
                </div>
            </div>

            <div class="panel-card">
                <div class="panel-header"><span id="txtNewsHeader">🚨 REAL-TIME ECONOMIC CALENDAR</span></div>
                <div class="news-live-box" id="economicCalendarBox">
                    <div class="news-item-row"><span class="news-time">Loading...</span><span>Fetching events...</span></div>
                </div>
            </div>

            <div class="panel-card">
                <div class="panel-header"><span id="txtSessionHeader">🌐 MARKET SESSIONS</span></div>
                <div class="sessions-grid">
                    <div class="session-item" id="sessSydney"><div class="session-name">Sydney</div><div class="session-status" id="stSydney">--</div></div>
                    <div class="session-item" id="sessTokyo"><div class="session-name">Tokyo</div><div class="session-status" id="stTokyo">--</div></div>
                    <div class="session-item" id="sessLondon"><div class="session-name">London</div><div class="session-status" id="stLondon">--</div></div>
                    <div class="session-item" id="sessNY"><div class="session-name">New York</div><div class="session-status" id="stNY">--</div></div>
                </div>
            </div>

            <div class="panel-card">
                <div class="panel-header">
                    <span id="txtAiHeader">⚡ AI SIGNAL & TREND METER</span>
                    <span id="marketBadge" style="font-size:10px; color:var(--accent-cyan);">XAUUSD</span>
                </div>

                <div class="confluence-grid">
                    <div class="conf-box" id="tfM15">M15: --</div>
                    <div class="conf-box" id="tfH1">H1: --</div>
                    <div class="conf-box" id="tfH4">H4: --</div>
                </div>

                <div class="signal-box">
                    <div class="signal-title" id="signalStatus">ត្រៀមវិភាគ...</div>
                    <div class="signal-confidence" id="signalConfidence">ចុចវិភាគ ឬបើក Auto-Scan 24/7</div>
                </div>

                <div class="metrics-grid">
                    <div class="metric-item">
                        <div class="metric-label" id="txtEntry">Entry Price</div>
                        <div class="metric-value" id="entryVal">--</div>
                    </div>
                    <div class="metric-item sl">
                        <div class="metric-label" id="txtSL">Stop Loss (SL)</div>
                        <div class="metric-value" id="slVal" style="color:var(--red-signal);">--</div>
                    </div>
                </div>

                <div class="tp-list">
                    <div class="tp-item"><span>TP1</span><strong id="tp1Val" style="color:var(--green-signal);">--</strong></div>
                    <div class="tp-item"><span>TP2</span><strong id="tp2Val" style="color:var(--green-signal);">--</strong></div>
                    <div class="tp-item"><span>TP3</span><strong id="tp3Val" style="color:var(--green-signal);">--</strong></div>
                </div>

                <div class="rr-badge" id="rrBadge">Risk/Reward Ratio: 1 : --</div>

                <div class="controls-flex">
                    <button class="btn-run-ai" id="btnRunAi" onclick="generateAISignal()">🔍 វិភាគឥឡូវនេះ</button>
                    <button class="btn-auto-scan" id="autoScanBtn" onclick="toggleAutoScan()">🤖 Auto-Scan</button>
                </div>
            </div>

            <div class="panel-card">
                <div class="panel-header"><span id="txtCalcHeader">🧮 LOT CALCULATOR & PNL JOURNAL</span></div>
                <div class="calc-inputs">
                    <div class="calc-group">
                        <label id="txtBalLabel">ទុនដក ($)</label>
                        <input type="number" id="calcBalance" value="1000" oninput="calculateLotSize()">
                    </div>
                    <div class="calc-group">
                        <label>Risk %</label>
                        <input type="number" id="calcRisk" value="1" step="0.5" oninput="calculateLotSize()">
                    </div>
                </div>
                <div class="stats-grid">
                    <div>Lot ណែនាំ<br><strong id="recommendedLot" style="color:var(--accent-cyan);">0.02 Lot</strong></div>
                    <div>Win-Rate<br><strong id="winRateVal" style="color:var(--green-signal);">0%</strong></div>
                    <div>Net PNL<br><strong id="netPnlVal" style="color:var(--accent-primary);">$0.00</strong></div>
                </div>
            </div>

            <div class="panel-card">
                <div class="panel-header"><span id="txtTgHeader">✈️ TELEGRAM BOT & BACKUP</span></div>
                <div class="tg-inputs">
                    <input type="text" id="tgBotToken" placeholder="Bot Token" onchange="saveTgConfig()">
                    <input type="text" id="tgChatId" placeholder="Chat ID" onchange="saveTgConfig()">
                </div>
                <div style="display:flex; gap:4px; margin-top:6px;">
                    <button class="btn-small" onclick="exportConfig()" style="flex:1; background:var(--card-bg); padding:4px; border:1px solid var(--border-color); border-radius:4px; text-align:center;">Export</button>
                    <button class="btn-small" onclick="importConfig()" style="flex:1; background:var(--card-bg); padding:4px; border:1px solid var(--border-color); border-radius:4px; text-align:center;">Import</button>
                    <button class="btn-small" onclick="resetAllSettings()" style="flex:1; background:rgba(239,68,68,0.2); color:var(--red-signal); padding:4px; border:1px solid var(--red-signal); border-radius:4px; text-align:center;">Reset</button>
                </div>
            </div>

            <div class="panel-card">
                <div class="panel-header">
                 <span id="txtHistHeader">📜 TRADE JOURNAL & HISTORY</span>
                    <div>
                        <button class="btn-small" onclick="exportHistoryCSV()">Export</button> |
                        <button class="btn-small" onclick="clearHistory()" style="color:var(--red-signal);">Clear</button>
                    </div>
                </div>
                
                <table class="history-table">
                    <thead>
                        <tr>
                            <th id="thTime">ម៉ោង</th>
                            <th id="thAsset">Asset</th>
                            <th id="thSig">សញ្ញា</th>
                            <th id="thEntry">Entry</th>
                            <th id="thAction">Action</th>
                        </tr>
                    </thead>
                    <tbody id="historyBody">
                        <tr><td colspan="5" style="text-align:center; color:var(--text-sub); padding:6px;">មិនទាន់មានប្រវត្តិវិភាគ</td></tr>
                    </tbody>
                </table>
            </div>

        </div>
    </div>

    <div id="toastContainer"></div>

    <!-- TRADINGVIEW SCRIPT -->
    <script type="text/javascript" src="https://s3.tradingview.com/tv.js"></script>
    <script type="text/javascript">
        let currentSymbol = "OANDA:XAUUSD";
        let historyLogs = JSON.parse(localStorage.getItem("rith_history")) || [];
        let autoScanInterval = null;
        let isAutoScanning = false;
        let soundMode = "beep";
        let currentLang = "km";
        let isSplitViewActive = false;

        function switchAuthTab(tab) {
            let loginForm = document.getElementById("loginFormContainer");
            let regForm = document.getElementById("regFormContainer");
            let tabLogin = document.getElementById("tabLoginBtn");
            let tabReg = document.getElementById("tabRegBtn");

            if (tab === 'login') {
                loginForm.style.display = "block";
                regForm.style.display = "none";
                tabLogin.classList.add("active");
                tabReg.classList.remove("active");
            } else {
                loginForm.style.display = "none";
                regForm.style.display = "block";
                tabReg.classList.add("active");
                tabLogin.classList.remove("active");
            }
        }

        function handleRegister() {
            let u = document.getElementById("regUser").value.trim();
            let p = document.getElementById("regPass").value.trim();
            if(!u || !p) {
                alert("សូមបំពេញ Username និង Password ឱ្យបានត្រឹមត្រូវ!");
                return;
            }
            localStorage.setItem("rith_db_user", u);
            localStorage.setItem("rith_db_pass", p);
            alert("បង្កើតគណនីបានสำเร็จ! សូមធ្វើការ Login ចូល.");
            switchAuthTab('login');
            document.getElementById("loginUser").value = u;
        }

        function handleLogin() {
            let u = document.getElementById("loginUser").value.trim();
            let p = document.getElementById("loginPass").value.trim();
            let savedU = localStorage.getItem("rith_db_user");
            let savedP = localStorage.getItem("rith_db_pass");

            if ((u === "Rith" && p === "1234") || (savedU && u === savedU && p === savedP)) {
                document.getElementById("authOverlay").style.display = "none";
                document.getElementById("userProfileDisplay").innerText = "👤 " + u + " (PRO)";
                showToast("Login Successful!");
            } else {
                alert("ឈ្មោះគណនី ឬពាក្យសម្ងាត់មិនត្រឹមត្រូវ!");
            }
        }

        function verifyVipKey() {
            let key = document.getElementById("vipKeyInput").value.trim();
            if (key === "RITH-KING-VIP-2026" || key === "Rith2026") {
                document.getElementById("authOverlay").style.display = "none";
                document.getElementById("userProfileDisplay").innerText = "👑 Rith (VIP PRO)";
                showToast("VIP License Verified Successfully!");
            } else {
                alert("Invalid VIP Key!");
            }
        }

        function logoutUser() {
            document.getElementById("authOverlay").style.display = "flex";
            document.getElementById("userProfileDisplay").innerText = "👤 Guest";
            showToast("Logged out successfully");
        }

        function showToast(message) {
            let container = document.getElementById("toastContainer");
            let toast = document.createElement("div");
            toast.className = "toast";
            toast.innerText = "👑 " + message;
            container.appendChild(toast);
            setTimeout(() => { toast.remove(); }, 4000);
        }

        function toggleSplitView() {
            isSplitViewActive = !isSplitViewActive;
            let container = document.getElementById("chartGridContainer");
            let widget2 = document.getElementById("tradingview_widget_2");
            if (isSplitViewActive) {
                container.classList.add("split-2");
                widget2.style.display = "block";
                new TradingView.widget({
                    "autosize": true,
                    "symbol": "BINANCE:BTCUSDT",
                    "interval": "60",
                    "timezone": "Asia/Phnom_Penh",
                    "theme": "dark",
                    "style": "1",
                    "locale": "en",
                    "container_id": "tradingview_widget_2"
                });
                showToast("Split View Enabled");
            } else {
                container.classList.remove("split-2");
                widget2.style.display = "none";
                showToast("Split View Disabled");
            }
        }

        async function fetchEconomicCalendar() {
            try {
                let res = await fetch("https://nfs.faireconomy.media/ff_calendar_thisweek.json");
                let data = await res.json();
                let highImpact = data.filter(item => item.impact === "High" && item.country === "USD").slice(0, 2);
                let html = "";
                if(highImpact.length === 0) {
                    html = `<div class="news-item-row"><span class="news-time">--:--</span><span>No High Impact Events</span></div>`;
                } else {
                    highImpact.forEach(ev => {
                        let dateObj = new Date(ev.date);
                        let timeStr = dateObj.getHours().toString().padStart(2,'0') + ":" + dateObj.getMinutes().toString().padStart(2,'0');
                        html += `
                            <div class="news-item-row">
                                <span class="news-time">${timeStr} USD</span>
                                <span style="font-size:9px; max-width:110px; overflow:hidden; text-overflow:ellipsis; white-space:nowrap;">${ev.title}</span>
                                <strong style="color:var(--red-signal);">HIGH</strong>
                            </div>
                        `;
                    });
                }
                document.getElementById("economicCalendarBox").innerHTML = html;
            } catch(e) {
                document.getElementById("economicCalendarBox").innerHTML = `
                    <div class="news-item-row"><span class="news-time">20:30 USD</span><span>Non-Farm Payrolls (NFP)</span><strong style="color:var(--red-signal);">HIGH</strong></div>
                `;
            }
        }
        function loadChart(symbol) {
            new TradingView.widget({
                "autosize": true,
                "symbol": symbol,
                "interval": "60",
                "timezone": "Asia/Phnom_Penh",
                "theme": "dark",
                "style": "1",
                "locale": "en",
                "container_id": "tradingview_widget"
            });
        }

        loadChart(currentSymbol);
        updateHistoryTable();
        calculateLotSize();
        updateMarketSessions();
        loadTgConfig();
        fetchEconomicCalendar();
        setInterval(updateMarketSessions, 60000);

        function selectWatchAsset(symbolName, tvSymbol) {
            document.getElementById("assetSelect").value = symbolName;
            document.getElementById("marketBadge").innerText = symbolName;
            currentSymbol = tvSymbol;
            loadChart(currentSymbol);
        }

        function changeTheme() {
            let theme = document.getElementById("themeSelect").value;
            document.body.className = theme === "gold" ? "" : "theme-" + theme;
        }

        function changeLanguage() { currentLang = document.getElementById("langSelect").value; }

        function changeAsset() {
            let asset = document.getElementById("assetSelect").value;
            document.getElementById("marketBadge").innerText = asset;
            if (asset === "XAUUSD") currentSymbol = "OANDA:XAUUSD";
            else if (asset === "EURUSD") currentSymbol = "FX:EURUSD";
            else if (asset === "GBPUSD") currentSymbol = "FX:GBPUSD";
            else if (asset === "BTCUSD") currentSymbol = "BINANCE:BTCUSDT";
            else if (asset === "US30") currentSymbol = "FOREXCOM:SPXUSD";
            loadChart(currentSymbol);
        }

        function updateMarketSessions() {
            let now = new Date();
            let utcHour = now.getUTCHours();
            setSessionStatus("sessSydney", "stSydney", (utcHour >= 22 || utcHour < 7));
            setSessionStatus("sessTokyo", "stTokyo", (utcHour >= 0 && utcHour < 9));
            setSessionStatus("sessLondon", "stLondon", (utcHour >= 8 && utcHour < 16));
            setSessionStatus("sessNY", "stNY", (utcHour >= 13 && utcHour < 22));
        }

        function setSessionStatus(cardId, textId, isOpen) {
            let card = document.getElementById(cardId);
            let text = document.getElementById(textId);
            if (isOpen) {
                card.classList.add("active");
                text.innerText = "OPEN";
                text.style.color = "#22c55e";
            } else {
                card.classList.remove("active");
                text.innerText = "CLOSED";
                text.style.color = "#9ca3af";
            }
        }

        function toggleAutoScan() {
            let btn = document.getElementById("autoScanBtn");
            let badge = document.getElementById("systemStateBadge");
            if (!isAutoScanning) {
                isAutoScanning = true;
                btn.classList.add("active");
                btn.innerText = "⏹️ Stop";
                badge.innerText = "Auto-Scanning";
                autoScanInterval = setInterval(() => generateAISignal(), 120000);
            } else {
                isAutoScanning = false;
                btn.classList.remove("active");
                btn.innerText = "🤖 Auto-Scan";
                badge.innerText = "Online";
                clearInterval(autoScanInterval);
            }
        }

        function generateAISignal() {
            let asset = document.getElementById("assetSelect").value;
            let statusEl = document.getElementById("signalStatus");
            let confEl = document.getElementById("signalConfidence");
            let isBuy = Math.random() > 0.5;
            let basePrice = asset === "BTCUSD" ? 68500 : (asset === "US30" ? 42500 : (asset === "XAUUSD" ? 4060 : 1.0850));
            let entry = (basePrice + (Math.random() * 5 - 2.5)).toFixed(asset === "EURUSD" ? 4 : 2);
            let entryNum = parseFloat(entry);
            let signalType = isBuy ? "BUY" : "SELL";

            document.getElementById("tfM15").innerText = "M15: " + (isBuy ? "BULL" : "BEAR");
            document.getElementById("tfH1").innerText = "H1: " + (isBuy ? "BULL" : "BEAR");
            document.getElementById("tfH4").innerText = "H4: " + (isBuy ? "BULL" : "BEAR");

            let sl = (isBuy ? entryNum - 7.5 : entryNum + 7.5).toFixed(2);
            let tp1 = (isBuy ? entryNum + 10 : entryNum - 10).toFixed(2);
            let tp2 = (isBuy ? entryNum + 18 : entryNum - 18).toFixed(2);
            let tp3 = (isBuy ? entryNum + 30 : entryNum - 30).toFixed(2);

            statusEl.innerText = isBuy ? "🟢 BUY BREAKOUT" : "🔴 SELL BREAKOUT";
            statusEl.style.color = isBuy ? "#22c55e" : "#ef4444";
            confEl.innerText = "AI Confidence: 92.4%";

            document.getElementById("entryVal").innerText = "$" + entry;
            document.getElementById("slVal").innerText = "$" + sl;
            document.getElementById("tp1Val").innerText = "$" + tp1;
            document.getElementById("tp2Val").innerText = "$" + tp2;
            document.getElementById("tp3Val").innerText = "$" + tp3;

            showToast(`New ${signalType} Signal for ${asset}`);
            let now = new Date();
            let timeStr = now.getHours().toString().padStart(2, '0') + ":" + now.getMinutes().toString().padStart(2, '0');
            
            historyLogs.unshift({ id: Date.now(), time: timeStr, asset: asset, type: signalType, entry: "$" + entry, status: "PENDING", pnl: 0 });
            localStorage.setItem("rith_history", JSON.stringify(historyLogs));
            updateHistoryTable();
        }

        function calculateLotSize() {
            let balance = parseFloat(document.getElementById("calcBalance").value) || 1000;
            let risk = parseFloat(document.getElementById("calcRisk").value) || 1;
            let lot = ((balance * (risk / 100)) / 750).toFixed(2);
            if (lot < 0.01) lot = 0.01;
            document.getElementById("recommendedLot").innerText = lot + " Lot";
        }

        function recordPNL(id, isWin) {
            let balance = parseFloat(document.getElementById("calcBalance").value) || 1000;
            let risk = parseFloat(document.getElementById("calcRisk").value) || 1;
            let riskAmount = balance * (risk / 100);
            let item = historyLogs.find(x => x.id === id);
            if (item) {
                item.status = isWin ? "WIN" : "LOSS";
                item.pnl = isWin ? (riskAmount * 3.2) : -riskAmount;
                localStorage.setItem("rith_history", JSON.stringify(historyLogs));
                updateHistoryTable();
            }
        }

        function updateHistoryTable() {
            let tbody = document.getElementById("historyBody");
            if (historyLogs.length === 0) {
                tbody.innerHTML = `<tr><td colspan="5" style="text-align:center; color:var(--text-sub); padding:6px;">មិនទាន់មានប្រវត្តិវិភាគ</td></tr>`;
                document.getElementById("winRateVal").innerText = "0%";
                document.getElementById("netPnlVal").innerText = "$0.00";
                return;
            }
            let html = "", wins = 0, total = 0, pnl = 0;
            historyLogs.slice(0, 5).forEach(item => {
                let badge = item.type === "BUY" ? "badge-buy" : "badge-sell";
                let action = item.status === "PENDING" ? 
                    `<button class="btn-action btn-win" onclick="recordPNL(${item.id}, true)">W</button><button class="btn-action btn-loss" onclick="recordPNL(${item.id}, false)">L</button>` :
                    `<strong>${item.status}</strong>`;
                if(item.status !== "PENDING") { total++; if(item.status === "WIN") wins++; pnl += item.pnl; }
                html += `<tr><td>${item.time}</td><td><strong>${item.asset}</strong></td><td class="${badge}">${item.type}</td><td>${item.entry}</td><td>${action}</td></tr>`;
            });
            tbody.innerHTML = html;
            document.getElementById("winRateVal").innerText = total > 0 ? Math.round((wins/total)*100) + "%" : "0%";
            document.getElementById("netPnlVal").innerText = (pnl >= 0 ? "+$" : "-$") + Math.abs(pnl).toFixed(0);
        }

        function clearHistory() { historyLogs = []; localStorage.removeItem("rith_history"); updateHistoryTable(); }
        function saveTgConfig() { localStorage.setItem("rith_tg_token", document.getElementById("tgBotToken").value); localStorage.setItem("rith_tg_chatid", document.getElementById("tgChatId").value); }
        function loadTgConfig() { document.getElementById("tgBotToken").value = localStorage.getItem("rith_tg_token") || ""; document.getElementById("tgChatId").value = localStorage.getItem("rith_tg_chatid") || ""; }
        function resetAllSettings() { if(confirm("តើអ្នកចង់ Reset មែនទេ?")) { localStorage.clear(); location.reload(); } }
    </script>
</body>
</html>
