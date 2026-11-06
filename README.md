<!DOCTYPE html>
<html lang="km">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>RITH KING ANALYZER PRO</title>
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
            background: rgba(9, 13, 22, 0.95);
            z-index: 9999;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        .auth-box {
            background: var(--panel-bg);
            border: 1px solid var(--border-color);
            padding: 25px;
            border-radius: 12px;
            width: 360px;
            text-align: center;
            box-shadow: 0 15px 35px rgba(0,0,0,0.6);
        }
        .auth-box h2 { color: var(--accent-primary); font-size: 20px; margin-bottom: 5px; }
        .auth-box p { font-size: 11px; color: var(--text-sub); margin-bottom: 20px; }
        
        .auth-submit {
            width: 100%;
            background: linear-gradient(135deg, #f59e0b, #d97706);
            color: #000;
            font-weight: bold;
            padding: 12px;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            text-transform: uppercase;
            font-size: 12px;
            transition: 0.2s;
        }
        .auth-submit:hover { opacity: 0.9; }

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

        .chart-container { flex: 1; width: 100%; height: 100%; }

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
    </style>
</head>
<body>

    <div id="authOverlay">
        <div class="auth-box">
            <h2>👑 RITH KING TERMINAL</h2>
            <p>ប្រព័ន្ធវិភាគទីផ្សារហិរញ្ញវត្ថុអាជីព</p>
            <button class="auth-submit" onclick="enterTerminal()">ចូលប្រព័ន្ធ (Enter Terminal)</button>
        </div>
    </div>

    <div class="top-navbar">
        <div class="brand-logo">
            <span>👑</span>
            <h1 id="txtBrand">RITH KING ANALYZER PRO</h1>
        </div>
        <div class="system-status">
            <span id="userProfileDisplay" style="color:var(--accent-primary); font-weight:bold; font-size:11px;">👤 Rith Admin</span>
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
                <div class="watch-item" onclick="selectWatchAsset('EURUSD', 'FX:EURUSD')">
                    <div class="watch-top"><span>EURUSD</span> <span class="watch-chg chg-neg" id="wChg_EURUSD">-0.12%</span></div>
                    <div class="watch-price" id="wPrice_EURUSD">1.0842</div>
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
            <div class="chart-container">
                <div id="tradingview_widget" style="height:100%;width:100%;"></div>
            </div>
        </div>

        <div class="side-pane">
            
            <div class="panel-card">
                <div class="panel-header"><span id="txtSupportHeader">💬 SUPPORT & CONTACT</span></div>
                <div class="support-box">
                    <span id="txtAdmin">Admin Telegram:</span>
                    <a href="https://t.me/Rith_putuy" target="_blank">@Rith_putuy (+855966251855)</a>
                </div>
            </div>

            <div class="panel-card">
                <div class="panel-header"><span id="txtNewsHeader">🚨 HIGH-IMPACT NEWS FILTER</span></div>
                <div class="news-live-box">
                    <div class="news-item-row">
                        <span class="news-time">20:30 USD</span>
                        <span>Non-Farm Payrolls (NFP)</span>
                        <strong style="color:var(--red-signal);">HIGH IMPACT</strong>
                    </div>
                    <div class="news-item-row">
                        <span class="news-time">22:00 USD</span>
                        <span>ISM Services PMI</span>
                        <strong style="color:var(--accent-primary);">MED</strong>
                    </div>
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
                    <span id="marketBadge" style="font-size:10px; co
