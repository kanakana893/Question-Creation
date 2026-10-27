<!DOCTYPE html>
<html lang="ja" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>問題作成・学習アプリ 要件定義書 (Ver 0.5)</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Lucide Icons -->
    <script src="https://unpkg.com/lucide@latest"></script>
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Fira+Code:wght@400;600&family=Inter:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">

    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        cyber: {
                            bg: '#0a0d14',
                            surface: '#121824',
                            card: '#182030',
                            border: '#2a364f',
                            primary: '#3b82f6',
                            cyan: '#06b6d4',
                            neon: '#00f0ff',
                            purple: '#a855f7',
                            pink: '#ec4899',
                            warning: '#f59e0b',
                            danger: '#ef4444',
                            success: '#10b981'
                        }
                    },
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                        mono: ['Fira Code', 'monospace'],
                    }
                }
            }
        }
    </script>
    <style>
        /* カスタムスクロールバー */
        ::-webkit-scrollbar {
            width: 8px;
            height: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #0a0d14;
        }
        ::-webkit-scrollbar-thumb {
            background: #1e293b;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #334155;
        }
        
        /* ガラスモフィズム */
        .glass-panel {
            background: rgba(24, 32, 48, 0.75);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.08);
        }

        .glass-panel-glow {
            background: rgba(24, 32, 48, 0.75);
            backdrop-filter: blur(12px);
            border: 1px solid rgba(6, 182, 212, 0.3);
            box-shadow: 0 0 20px rgba(6, 182, 212, 0.15);
        }

        /* ネオンテキストグラデーション */
        .neon-text {
            background: linear-gradient(135deg, #00f0ff 0%, #3b82f6 50%, #a855f7 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        /* スムーススクロール */
        html {
            scroll-behavior: smooth;
        }

        /* アクティブサイドバーリンク */
        .nav-link.active {
            background: linear-gradient(90deg, rgba(6, 182, 212, 0.15) 0%, transparent 100%);
            border-left: 3px solid #06b6d4;
            color: #00f0ff;
        }
    </style>
</head>
<body class="bg-cyber-bg text-slate-300 font-sans antialiased min-h-screen flex flex-col">

    <!-- ヘッダーバー -->
    <header class="sticky top-0 z-50 glass-panel border-b border-cyber-border px-4 lg:px-8 py-3 flex items-center justify-between">
        <div class="flex items-center space-x-3">
            <button id="mobile-menu-btn" class="lg:hidden text-slate-400 hover:text-white p-1">
                <i data-lucide="menu" class="w-6 h-6"></i>
            </button>
            <div class="flex items-center space-x-2">
                <div class="p-2 bg-gradient-to-tr from-cyan-500 to-blue-600 rounded-lg text-white shadow-lg shadow-cyan-500/30">
                    <i data-lucide="brain-circuit" class="w-6 h-6"></i>
                </div>
                <div>
                    <span class="text-xs font-mono text-cyber-cyan tracking-wider uppercase block leading-none">System Doc</span>
                    <h1 class="text-lg font-bold text-white tracking-tight flex items-center gap-2">
                        問題作成・学習アプリ 要件定義書
                        <span class="text-xs bg-cyber-cyan/10 border border-cyber-cyan/30 text-cyber-cyan font-mono px-2 py-0.5 rounded-full">v0.5</span>
                    </h1>
                </div>
            </div>
        </div>

        <!-- アクションボタン・ステータス -->
        <div class="flex items-center space-x-4">
            <div class="hidden sm:flex items-center space-x-2 text-xs font-mono bg-cyber-surface px-3 py-1.5 rounded-full border border-cyber-border">
                <span class="w-2 h-2 rounded-full bg-cyber-warning animate-pulse"></span>
                <span class="text-slate-400">STATUS:</span>
                <span class="text-cyber-warning font-semibold">ユーザー確認事項反映版</span>
            </div>
            <button onclick="window.print()" class="flex items-center space-x-1.5 bg-cyber-surface hover:bg-cyber-border text-slate-300 px-3 py-1.5 rounded-lg text-xs font-medium border border-cyber-border transition-all">
                <i data-lucide="printer" class="w-4 h-4"></i>
                <span class="hidden md:inline">印刷 / PDF出力</span>
            </button>
        </div>
    </header>

    <div class="flex flex-1 overflow-hidden relative">

        <!-- サイドバーナビゲーション -->
        <aside id="sidebar" class="fixed inset-y-0 left-0 z-40 w-64 bg-cyber-surface/95 border-r border-cyber-border transition-transform transform -translate-x-full lg:translate-x-0 lg:static lg:inset-auto lg:flex flex-col pt-16 lg:pt-0">
            <div class="p-4 border-b border-cyber-border/50">
                <div class="relative">
                    <i data-lucide="search" class="w-4 h-4 absolute left-3 top-2.5 text-slate-500"></i>
                    <input type="text" id="quick-search" placeholder="ドキュメント内検索..." class="w-full bg-cyber-bg border border-cyber-border rounded-lg pl-9 pr-3 py-1.5 text-xs text-slate-200 placeholder-slate-500 focus:outline-none focus:border-cyber-cyan focus:ring-1 focus:ring-cyber-cyan">
                </div>
            </div>

            <nav class="flex-1 overflow-y-auto p-3 space-y-1 text-xs">
                <a href="#metadata" class="nav-link flex items-center gap-2 px-3 py-2 rounded-lg text-slate-400 hover:text-white hover:bg-cyber-card transition-all">
                    <i data-lucide="file-text" class="w-4 h-4 text-cyber-cyan"></i> 文書情報 & 概要
                </a>
                <a href="#overview" class="nav-link flex items-center gap-2 px-3 py-2 rounded-lg text-slate-400 hover:text-white hover:bg-cyber-card transition-all">
                    <i data-lucide="target" class="w-4 h-4 text-blue-400"></i> 1. システム概要 & 用語
                </a>
                <a href="#scope" class="nav-link flex items-center gap-2 px-3 py-2 rounded-lg text-slate-400 hover:text-white hover:bg-cyber-card transition-all">
                    <i data-lucide="layers" class="w-4 h-4 text-purple-400"></i> 2-3. 背景 & 対象範囲
                </a>
                <a href="#functional" class="nav-link flex items-center gap-2 px-3 py-2 rounded-lg text-slate-400 hover:text-white hover:bg-cyber-card transition-all">
                    <i data-lucide="cpu" class="w-4 h-4 text-cyber-neon"></i> 4. 機能要件 (FR)
                </a>
                <a href="#review-logic" class="nav-link flex items-center gap-2 px-3 py-2 rounded-lg text-slate-400 hover:text-white hover:bg-cyber-card transition-all pl-6">
                    <i data-lucide="repeat" class="w-3.5 h-3.5 text-cyber-cyan"></i> 復習ロジック & サイクル
                </a>
                <a href="#screens" class="nav-link flex items-center gap-2 px-3 py-2 rounded-lg text-slate-400 hover:text-white hover:bg-cyber-card transition-all">
                    <i data-lucide="layout" class="w-4 h-4 text-emerald-400"></i> 5. 画面要件
                </a>
                <a href="#data-requirements" class="nav-link flex items-center gap-2 px-3 py-2 rounded-lg text-slate-400 hover:text-white hover:bg-cyber-card transition-all">
                    <i data-lucide="database" class="w-4 h-4 text-amber-400"></i> 6. データ要件
                </a>
                <a href="#interfaces" class="nav-link flex items-center gap-2 px-3 py-2 rounded-lg text-slate-400 hover:text-white hover:bg-cyber-card transition-all">
                    <i data-lucide="network" class="w-4 h-4 text-pink-400"></i> 7. 外部IF & 非機能要件
                </a>
                <a href="#tbd-section" class="nav-link flex items-center gap-2 px-3 py-2 rounded-lg text-amber-400/90 hover:text-amber-300 hover:bg-amber-500/10 transition-all font-semibold">
                    <i data-lucide="alert-triangle" class="w-4 h-4 text-amber-400"></i> 9. 未決定事項 (TBD)
                </a>
                <a href="#acceptance" class="nav-link flex items-center gap-2 px-3 py-2 rounded-lg text-slate-400 hover:text-white hover:bg-cyber-card transition-all">
                    <i data-lucide="check-circle-2" class="w-4 h-4 text-indigo-400"></i> 10. 受け入れ条件 (AC)
                </a>
                <a href="#roadmap" class="nav-link flex items-center gap-2 px-3 py-2 rounded-lg text-slate-400 hover:text-white hover:bg-cyber-card transition-all">
                    <i data-lucide="flag" class="w-4 h-4 text-cyan-400"></i> 11. 実装優先順位
                </a>
            </nav>

            <div class="p-4 border-t border-cyber-border text-[11px] text-slate-500 font-mono">
                Last updated: 2026-10-23<br>
                Target OS: Windows 10 / 11
            </div>
        </aside>

        <!-- オーバーレイ (モバイル表示用) -->
        <div id="sidebar-overlay" class="fixed inset-0 bg-black/60 backdrop-blur-sm z-30 hidden lg:hidden"></div>

        <!-- メインコンテンツエリア -->
        <main class="flex-1 overflow-y-auto p-4 sm:p-6 lg:p-10 space-y-12">

            <!-- ヒーロー / ドキュメントヘッダー -->
            <section id="metadata" class="glass-panel-glow rounded-2xl p-6 lg:p-8 relative overflow-hidden">
                <div class="absolute -right-10 -bottom-10 w-60 h-60 bg-gradient-to-br from-cyber-cyan/10 to-purple-600/10 rounded-full blur-3xl pointer-events-none"></div>
                
                <div class="flex flex-wrap items-center justify-between gap-4 border-b border-cyber-border/80 pb-6 mb-6">
                    <div>
                        <div class="flex items-center gap-2 mb-2">
                            <span class="px-2.5 py-1 rounded-md bg-blue-500/10 text-blue-400 border border-blue-500/30 text-xs font-mono font-semibold">REQUIREMENTS SPECIFICATION</span>
                            <span class="px-2.5 py-1 rounded-md bg-purple-500/10 text-purple-400 border border-purple-500/30 text-xs font-mono">Desktop App</span>
                        </div>
                        <h2 class="text-2xl sm:text-3xl font-extrabold text-white tracking-tight">
                            問題作成・学習アプリ <span class="neon-text">要件定義書</span>
                        </h2>
                    </div>
                    
                    <!-- KPI ミニカード -->
                    <div class="grid grid-cols-2 sm:grid-cols-3 gap-3 w-full sm:w-auto">
                        <div class="bg-cyber-bg/80 border border-cyber-border p-3 rounded-xl">
                            <div class="text-[10px] text-slate-400 uppercase font-mono">バージョン</div>
                            <div class="text-base font-bold text-cyber-cyan font-mono">v0.5</div>
                        </div>
                        <div class="bg-cyber-bg/80 border border-cyber-border p-3 rounded-xl">
                            <div class="text-[10px] text-slate-400 uppercase font-mono">機能要件数</div>
                            <div class="text-base font-bold text-white font-mono">48 FRs</div>
                        </div>
                        <div class="bg-cyber-bg/80 border border-cyber-border p-3 rounded-xl col-span-2 sm:col-span-1">
                            <div class="text-[10px] text-slate-400 uppercase font-mono">未決定課題</div>
                            <div class="text-base font-bold text-cyber-warning font-mono flex items-center gap-1">
                                <i data-lucide="alert-circle" class="w-4 h-4"></i> 2 TBD
                            </div>
                        </div>
                    </div>
                </div>

                <!-- メタデータグリッド -->
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4 text-xs">
                    <div class="bg-cyber-surface/60 p-3 rounded-lg border border-cyber-border/50">
                        <span class="text-slate-500 block mb-1">基準資料:</span>
                        <span class="text-slate-200 font-medium">問題作成・学習アプリ 統合仕様書・要件定義書</span>
                    </div>
                    <div class="bg-cyber-surface/60 p-3 rounded-lg border border-cyber-border/50">
                        <span class="text-slate-500 block mb-1">作成日:</span>
                        <span class="text-slate-200 font-mono">2026年10月23日</span>
                    </div>
                    <div class="bg-cyber-surface/60 p-3 rounded-lg border border-cyber-border/50">
                        <span class="text-slate-500 block mb-1">対象範囲:</span>
                        <span class="text-slate-200 font-medium">個人向け機能全体 (学校機能は除外)</span>
                    </div>
                    <div class="bg-cyber-surface/60 p-3 rounded-lg border border-cyber-border/50">
                        <span class="text-slate-500 block mb-1">主要更新:</span>
                        <span class="text-cyber-cyan font-medium">2段階評価・カード/問題分離の反映</span>
                    </div>
                </div>
            </section>

            <!-- 1. システム概要 & 想定環境 -->
            <section id="overview" class="space-y-6">
                <div class="flex items-center gap-3 border-l-4 border-cyber-cyan pl-4">
                    <h3 class="text-xl font-bold text-white tracking-wide">1. システム概要</h3>
                </div>

                <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
                    <!-- 目的カード -->
                    <div class="lg:col-span-2 glass-panel rounded-xl p-6 space-y-4">
                        <h4 class="text-sm font-semibold text-cyber-cyan flex items-center gap-2 font-mono uppercase tracking-wider">
                            <i data-lucide="target" class="w-4 h-4"></i> 1.1 システムの目的
                        </h4>
                        <p class="text-slate-300 leading-relaxed text-sm">
                            利用者が独自のデッキを作成・管理し、コンテンツ作成時に<strong class="text-white bg-blue-500/20 px-1.5 py-0.5 rounded">「カード形式」</strong>または<strong class="text-white bg-purple-500/20 px-1.5 py-0.5 rounded">「問題形式」</strong>を選択して登録できる暗記・学習アプリ。
                        </p>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4 pt-2">
                            <div class="bg-cyber-surface p-3.5 rounded-lg border border-cyber-border">
                                <span class="text-xs font-bold text-blue-400 block mb-1">🎴 カード形式</span>
                                <p class="text-xs text-slate-400">表面・裏面構造。「もう一度／正解」の2段階評価に基づき、間隔反復スケジュールにより暗記を極限まで効率化。</p>
                            </div>
                            <div class="bg-cyber-surface p-3.5 rounded-lg border border-cyber-border">
                                <span class="text-xs font-bold text-purple-400 block mb-1">📝 問題形式</span>
                                <p class="text-xs text-slate-400">一問一答、選択式、文字入力等の実践演習。解説表示や採点を行う（カード形式の復習ロジックは非適用）。</p>
                            </div>
                        </div>
                    </div>

                    <!-- 想定利用者 -->
                    <div class="glass-panel rounded-xl p-6 space-y-4">
                        <h4 class="text-sm font-semibold text-cyber-purple flex items-center gap-2 font-mono uppercase tracking-wider">
                            <i data-lucide="users" class="w-4 h-4"></i> 1.2 想定利用者
                        </h4>
                        <ul class="space-y-2.5 text-xs">
                            <li class="flex items-start gap-2 text-slate-300">
                                <i data-lucide="check-circle" class="w-4 h-4 text-cyber-cyan shrink-0 mt-0.5"></i>
                                個人学習者および資格試験の受験者
                            </li>
                            <li class="flex items-start gap-2 text-slate-300">
                                <i data-lucide="check-circle" class="w-4 h-4 text-cyber-cyan shrink-0 mt-0.5"></i>
                                ケアレスミスや同一誤答の再発を防ぎたい学習者
                            </li>
                            <li class="flex items-start gap-2 text-slate-300">
                                <i data-lucide="check-circle" class="w-4 h-4 text-cyber-cyan shrink-0 mt-0.5"></i>
                                子供の学習をサポートする保護者
                            </li>
                        </ul>
                    </div>
                </div>

                <!-- 利用形態 & 用語テーブル -->
                <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
                    <!-- 環境 -->
                    <div class="glass-panel rounded-xl p-5 space-y-3">
                        <h4 class="text-sm font-semibold text-white font-mono flex items-center gap-2">
                            <i data-lucide="monitor" class="w-4 h-4 text-cyber-cyan"></i> 1.3 利用形態・対象環境
                        </h4>
                        <div class="overflow-x-auto">
                            <table class="w-full text-left text-xs">
                                <tbody class="divide-y divide-cyber-border/50">
                                    <tr>
                                        <td class="py-2 px-3 text-slate-400 font-medium">形態</td>
                                        <td class="py-2 px-3 text-slate-200">デスクトップアプリ (オフライン動作)</td>
                                    </tr>
                                    <tr>
                                        <td class="py-2 px-3 text-slate-400 font-medium">対象OS</td>
                                        <td class="py-2 px-3 text-slate-200 font-mono">Windows 10 / Windows 11</td>
                                    </tr>
                                    <tr>
                                        <td class="py-2 px-3 text-slate-400 font-medium">データ保存</td>
                                        <td class="py-2 px-3 text-slate-200">完全ローカル保存（外部通信なし）</td>
                                    </tr>
                                    <tr>
                                        <td class="py-2 px-3 text-slate-400 font-medium">メディア保存</td>
                                        <td class="py-2 px-3 text-slate-200">専用ローカルフォルダ保存 + DBパス保持</td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                    </div>

                    <!-- 用語 -->
                    <div class="glass-panel rounded-xl p-5 space-y-3">
                        <h4 class="text-sm font-semibold text-white font-mono flex items-center gap-2">
                            <i data-lucide="book-open" class="w-4 h-4 text-cyber-purple"></i> 1.4 重要用語定義
                        </h4>
                        <div class="overflow-x-auto max-h-48 overflow-y-auto">
                            <table class="w-full text-left text-xs">
                                <thead class="bg-cyber-surface/80 text-slate-400 font-mono sticky top-0">
                                    <tr>
                                        <th class="p-2">用語</th>
                                        <th class="p-2">定義</th>
                                    </tr>
                                </thead>
                                <tbody class="divide-y divide-cyber-border/50">
                                    <tr>
                                        <td class="p-2 font-bold text-cyber-cyan">デッキ</td>
                                        <td class="p-2 text-slate-300">複数の問題をまとめた問題集の単位</td>
                                    </tr>
                                    <tr>
                                        <td class="p-2 font-bold text-cyber-cyan">自己評価</td>
                                        <td class="p-2 text-slate-300">カード解答後に選ぶ「もう一度／正解」の2段階評価</td>
                                    </tr>
                                    <tr>
                                        <td class="p-2 font-bold text-cyber-cyan">復習期限到来</td>
                                        <td class="p-2 text-slate-300">短時間は予定時刻到達、1日以上は日付変更時点</td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>
            </section>

            <!-- 2 & 3. スコープ (対象範囲) -->
            <section id="scope" class="space-y-6">
                <div class="flex items-center gap-3 border-l-4 border-purple-500 pl-4">
                    <h3 class="text-xl font-bold text-white tracking-wide">2 - 3. スコープ (対象範囲定義)</h3>
                </div>

                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <!-- 今回の対象範囲 -->
                    <div class="glass-panel border-emerald-500/30 rounded-xl p-6 space-y-4 relative overflow-hidden">
                        <div class="absolute top-0 right-0 px-3 py-1 bg-emerald-500/10 border-b border-l border-emerald-500/30 text-emerald-400 font-mono text-[10px] rounded-bl-lg font-bold">
                            IN SCOPE
                        </div>
                        <h4 class="text-base font-bold text-emerald-400 flex items-center gap-2">
                            <i data-lucide="check-circle-2" class="w-5 h-5"></i> 今回の実装対象 (Phase 1)
                        </h4>
                        <ul class="space-y-2 text-xs text-slate-300">
                            <li class="flex items-center gap-2"><span class="w-1.5 h-1.5 rounded-full bg-emerald-400"></span>デッキ・問題（カード/問題形式）のCRUD操作</li>
                            <li class="flex items-center gap-2"><span class="w-1.5 h-1.5 rounded-full bg-emerald-400"></span>一問一答、択一/複数選択、文字入力、画像付き問題</li>
                            <li class="flex items-center gap-2"><span class="w-1.5 h-1.5 rounded-full bg-emerald-400"></span>テキスト＆手書きメモ機能（過去3回分の履歴保持）</li>
                            <li class="flex items-center gap-2"><span class="w-1.5 h-1.5 rounded-full bg-emerald-400"></span>カード形式用 2段階評価＆間隔反復復習アルゴリズム</li>
                            <li class="flex items-center gap-2"><span class="w-1.5 h-1.5 rounded-full bg-emerald-400"></span>学習統計（正答率100%方式）、実績・バッジ・演出</li>
                            <li class="flex items-center gap-2"><span class="w-1.5 h-1.5 rounded-full bg-emerald-400"></span>ローカルデータバックアップ・復元・安全な初期化</li>
                        </ul>
                    </div>

                    <!-- 将来構想 -->
                    <div class="glass-panel border-slate-700 rounded-xl p-6 space-y-4 relative overflow-hidden">
                        <div class="absolute top-0 right-0 px-3 py-1 bg-slate-700/50 text-slate-400 font-mono text-[10px] rounded-bl-lg">
                            FUTURE SCOPE
                        </div>
                        <h4 class="text-base font-bold text-slate-400 flex items-center gap-2">
                            <i data-lucide="clock" class="w-5 h-5"></i> 将来構想 (Phase 2以降)
                        </h4>
                        <ul class="space-y-2 text-xs text-slate-400">
                            <li class="flex items-center gap-2"><span class="w-1.5 h-1.5 rounded-full bg-slate-600"></span>AIによる自動問題生成・教材画像解析</li>
                            <li class="flex items-center gap-2"><span class="w-1.5 h-1.5 rounded-full bg-slate-600"></span>教師によるデッキ一括配布機能</li>
                            <li class="flex items-center gap-2"><span class="w-1.5 h-1.5 rounded-full bg-slate-600"></span>生徒の学習履歴をサーバーに集約するクラウド機能</li>
                            <li class="flex items-center gap-2"><span class="w-1.5 h-1.5 rounded-full bg-slate-600"></span>学校・教育機関向けダッシュボード＆ライセンス展開</li>
                            <li class="flex items-center gap-2"><span class="w-1.5 h-1.5 rounded-full bg-slate-600"></span>デッキのユーザー間オンライン共有エクスポート</li>
                        </ul>
                    </div>
                </div>
            </section>

            <!-- 4. 機能要件 (FR) - インタラクティブ検索付き -->
            <section id="functional" class="space-y-6">
                <div class="flex flex-wrap items-center justify-between gap-4 border-l-4 border-cyber-neon pl-4">
                    <div>
                        <h3 class="text-xl font-bold text-white tracking-wide">4. 機能要件 (Functional Requirements)</h3>
                        <p class="text-xs text-slate-400">全48個の機能要件一覧。リアルタイムにフィルタリングが可能です。</p>
                    </div>
                    
                    <!-- カテゴリフィルター -->
                    <div class="flex flex-wrap items-center gap-2">
                        <input type="text" id="fr-search" placeholder="要件ID / キーワード検索..." class="bg-cyber-surface border border-cyber-border rounded-lg px-3 py-1.5 text-xs text-white placeholder-slate-500 focus:outline-none focus:border-cyber-cyan">
                        <select id="fr-filter" class="bg-cyber-surface border border-cyber-border rounded-lg px-3 py-1.5 text-xs text-slate-300 focus:outline-none focus:border-cyber-cyan">
                            <option value="ALL">全てのカテゴリー</option>
                            <option value="デッキ">デッキ管理</option>
                            <option value="問題">問題作成・演習</option>
                            <option value="学習">学習・メモ</option>
                            <option value="復習">復習・評価</option>
                            <option value="データ">データ・バックアップ</option>
                            <option value="演出">演出・実績</option>
                        </select>
                    </div>
                </div>

                <!-- 要件カードリスト -->
                <div id="fr-container" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4 max-h-[600px] overflow-y-auto pr-2">
                    <!-- JSで初期化生成・フィルタリング -->
                </div>
            </section>

            <!-- 4.2 カード形式 復習ロジック特別セクション -->
            <section id="review-logic" class="glass-panel border-cyber-cyan/30 rounded-2xl p-6 lg:p-8 space-y-6 relative">
                <div class="flex items-center gap-3">
                    <div class="p-2 bg-cyber-cyan/10 border border-cyber-cyan/30 rounded-lg text-cyber-cyan">
                        <i data-lucide="zap" class="w-6 h-6"></i>
                    </div>
                    <div>
                        <h3 class="text-lg font-bold text-white">カード形式：復習スケジュール＆学習サイクル（確定仕様）</h3>
                        <p class="text-xs text-slate-400">Ankiの概念を取り入れた2段階自己評価アルゴリズムの定義</p>
                    </div>
                </div>

                <!-- ステップタイムライン -->
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6 pt-2">
                    <div class="bg-cyber-surface/90 border border-cyber-border p-5 rounded-xl space-y-3">
                        <h4 class="text-xs font-mono font-bold text-cyber-warning uppercase flex items-center gap-1.5">
                            <i data-lucide="rotate-ccw" class="w-4 h-4"></i> 「もう一度」選択時
                        </h4>
                        <div class="p-3 bg-red-500/10 border border-red-500/20 rounded-lg text-xs text-slate-300">
                            学習段階を<strong>即時リセット</strong>し、<span class="text-red-400 font-bold font-mono">1分後</span>に再出題候補へ戻す。
                        </div>
                    </div>

                    <div class="bg-cyber-surface/90 border border-cyber-border p-5 rounded-xl space-y-3">
                        <h4 class="text-xs font-mono font-bold text-cyber-cyan uppercase flex items-center gap-1.5">
                            <i data-lucide="trending-up" class="w-4 h-4"></i> 「正解」選択時の段階推移
                        </h4>
                        <div class="flex flex-wrap items-center gap-1.5 text-xs font-mono">
                            <span class="px-2 py-1 bg-cyber-bg border border-cyber-border rounded text-slate-300">10分後</span> →
                            <span class="px-2 py-1 bg-cyber-bg border border-cyber-border rounded text-slate-300">1日後</span> →
                            <span class="px-2 py-1 bg-cyber-bg border border-cyber-border rounded text-slate-300">3日後</span> →
                            <span class="px-2 py-1 bg-cyber-bg border border-cyber-border rounded text-slate-300">7日後</span> →
                            <span class="px-2 py-1 bg-cyber-bg border border-cyber-border rounded text-slate-300">14日後</span> →
                            <span class="px-2 py-1 bg-cyber-cyan/20 border border-cyber-cyan/50 rounded text-cyber-cyan font-bold">以降 2倍</span>
                        </div>
                        <p class="text-[11px] text-slate-400">※1日以上の復習は経過時間ではなく「日付変更（0:00）」で判定。</p>
                    </div>
                </div>
            </section>

            <!-- 5. 画面要件 -->
            <section id="screens" class="space-y-6">
                <div class="flex items-center gap-3 border-l-4 border-emerald-400 pl-4">
                    <h3 class="text-xl font-bold text-white tracking-wide">5. 画面要件</h3>
                </div>

                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
                    <div class="glass-panel p-4 rounded-xl space-y-2 border-t-2 border-t-blue-500">
                        <div class="flex justify-between items-center">
                            <span class="text-xs font-bold text-white">ホーム / デッキ一覧</span>
                            <i data-lucide="home" class="w-4 h-4 text-slate-500"></i>
                        </div>
                        <p class="text-xs text-slate-400">デッキ一覧、正答率、新規作成・学習開始・共有読み込み導線</p>
                    </div>

                    <div class="glass-panel p-4 rounded-xl space-y-2 border-t-2 border-t-purple-500">
                        <div class="flex justify-between items-center">
                            <span class="text-xs font-bold text-white">デッキ詳細・問題一覧</span>
                            <i data-lucide="list" class="w-4 h-4 text-slate-500"></i>
                        </div>
                        <p class="text-xs text-slate-400">デッキ内の問題一覧表示、問題ごと正答率、CRUD操作</p>
                    </div>

                    <div class="glass-panel p-4 rounded-xl space-y-2 border-t-2 border-t-cyber-cyan">
                        <div class="flex justify-between items-center">
                            <span class="text-xs font-bold text-white">問題作成・編集</span>
                            <i data-lucide="edit-3" class="w-4 h-4 text-slate-500"></i>
                        </div>
                        <p class="text-xs text-slate-400">開始時に「カード形式/問題形式」を選択。形式別専用UI</p>
                    </div>

                    <div class="glass-panel p-4 rounded-xl space-y-2 border-t-2 border-t-emerald-500">
                        <div class="flex justify-between items-center">
                            <span class="text-xs font-bold text-white">学習画面</span>
                            <i data-lucide="play" class="w-4 h-4 text-slate-500"></i>
                        </div>
                        <p class="text-xs text-slate-400">逐次表示、手書き/テキストメモ、裏面確認＆2段階評価</p>
                    </div>

                    <div class="glass-panel p-4 rounded-xl space-y-2 border-t-2 border-t-amber-500">
                        <div class="flex justify-between items-center">
                            <span class="text-xs font-bold text-white">復習・進捗画面</span>
                            <i data-lucide="bar-chart-2" class="w-4 h-4 text-slate-500"></i>
                        </div>
                        <p class="text-xs text-slate-400">復習期限到来問題リスト、実績・バッジ、正答率統計</p>
                    </div>

                    <div class="glass-panel p-4 rounded-xl space-y-2 border-t-2 border-t-pink-500">
                        <div class="flex justify-between items-center">
                            <span class="text-xs font-bold text-white">設定画面</span>
                            <i data-lucide="settings" class="w-4 h-4 text-slate-500"></i>
                        </div>
                        <p class="text-xs text-slate-400">復習間隔、出題順序、バックアップ・復元、全初期化</p>
                    </div>
                </div>
            </section>

            <!-- 6 & 7 & 8. データ・外部IF・非機能要件 -->
            <section id="data-requirements" class="space-y-6">
                <div class="flex items-center gap-3 border-l-4 border-amber-400 pl-4">
                    <h3 class="text-xl font-bold text-white tracking-wide">6 - 8. データ・非機能要件</h3>
                </div>

                <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
                    <!-- データ構造 -->
                    <div class="glass-panel p-5 rounded-xl space-y-3">
                        <h4 class="text-sm font-bold text-white flex items-center gap-2 font-mono">
                            <i data-lucide="database" class="w-4 h-4 text-amber-400"></i> データ要件仕様
                        </h4>
                        <ul class="space-y-2 text-xs text-slate-300 divide-y divide-cyber-border/40">
                            <li class="pt-2"><strong>メディア分離:</strong> 画像/手書きはローカル保存、DBはファイルパス管理</li>
                            <li class="pt-2"><strong>カスケード削除:</strong> 問題削除時、関連履歴・メモ・添付ファイルも自動消去</li>
                            <li class="pt-2"><strong>メモ履歴:</strong> 問題/セッションごとに過去3回分保持、4回目で最古上書き</li>
                        </ul>
                    </div>

                    <!-- 非機能要件 -->
                    <div class="glass-panel p-5 rounded-xl space-y-3">
                        <h4 class="text-sm font-bold text-white flex items-center gap-2 font-mono" id="interfaces">
                            <i data-lucide="shield-check" class="w-4 h-4 text-pink-400"></i> 非機能要件 (NFR)
                        </h4>
                        <div class="grid grid-cols-2 gap-3 text-xs">
                            <div class="bg-cyber-surface p-2.5 rounded border border-cyber-border">
                                <span class="text-slate-500 block">性能:</span>
                                BLOB保存の回避で高速化
                            </div>
                            <div class="bg-cyber-surface p-2.5 rounded border border-cyber-border">
                                <span class="text-slate-500 block">信頼性:</span>
                                途中終了時の自動進捗保存
                            </div>
                            <div class="bg-cyber-surface p-2.5 rounded border border-cyber-border">
                                <span class="text-slate-500 block">安全性:</span>
                                インポート時のファイル検証
                            </div>
                            <div class="bg-cyber-surface p-2.5 rounded border border-cyber-border">
                                <span class="text-slate-500 block">プライバシー:</span>
                                外部通信完全遮断
                            </div>
                        </div>
                    </div>
                </div>
            </section>

            <!-- 9. 未決定事項 (TBD) ハイライトカード -->
            <section id="tbd-section" class="space-y-6">
                <div class="flex items-center gap-3 border-l-4 border-cyber-warning pl-4">
                    <h3 class="text-xl font-bold text-white tracking-wide">9. 未決定事項・要確認リスト (TBD)</h3>
                </div>

                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <!-- TBD-002 -->
                    <div class="glass-panel border-cyber-warning/50 rounded-xl p-6 relative overflow-hidden bg-gradient-to-br from-amber-500/5 to-transparent">
                        <div class="flex justify-between items-start mb-4">
                            <span class="px-2.5 py-1 bg-cyber-warning/20 border border-cyber-warning/40 text-cyber-warning rounded-md font-mono text-xs font-bold">
                                TBD-002
                            </span>
                            <span class="text-xs text-cyber-warning flex items-center gap-1 font-semibold">
                                <i data-lucide="alert-triangle" class="w-3.5 h-3.5"></i> 確認必要
                            </span>
                        </div>
                        <h4 class="text-base font-bold text-white mb-2">カード形式 復習間隔の上限値</h4>
                        <p class="text-xs text-slate-300 leading-relaxed mb-4">
                            最大復習間隔として<strong class="text-cyber-warning">「365日」</strong>と<strong class="text-cyber-warning">「999日」</strong>の2つの記載が元の確認資料内に混在しており、最終決定が必要。
                        </p>
                        <div class="bg-cyber-surface p-3 rounded-lg text-[11px] font-mono text-slate-400">
                            決定案: 一般的な資格勉強期間（1年=365日）か、長期記憶（999日）のどちらを優先するか。
                        </div>
                    </div>

                    <!-- TBD-013 -->
                    <div class="glass-panel border-cyber-warning/50 rounded-xl p-6 relative overflow-hidden bg-gradient-to-br from-amber-500/5 to-transparent">
                        <div class="flex justify-between items-start mb-4">
                            <span class="px-2.5 py-1 bg-cyber-warning/20 border border-cyber-warning/40 text-cyber-warning rounded-md font-mono text-xs font-bold">
                                TBD-013
                            </span>
                            <span class="text-xs text-cyber-warning flex items-center gap-1 font-semibold">
                                <i data-lucide="alert-triangle" class="w-3.5 h-3.5"></i> 確認必要
                            </span>
                        </div>
                        <h4 class="text-base font-bold text-white mb-2">メディアファイル欠損時の挙動</h4>
                        <p class="text-xs text-slate-300 leading-relaxed mb-4">
                            ローカルに保存された画像・手書きメモファイルが手動移動・削除された場合のアプリ上でのプレースホルダー表示・検出・修復処理の仕様。
                        </p>
                        <div class="bg-cyber-surface p-3 rounded-lg text-[11px] font-mono text-slate-400">
                            決定案: 「画像リンク切れ」アイコンを表示し、バックアップからの再読み込みを促すUI。
                        </div>
                    </div>
                </div>
            </section>

            <!-- 10. 受け入れ条件 (AC) -->
            <section id="acceptance" class="space-y-6">
                <div class="flex items-center gap-3 border-l-4 border-indigo-500 pl-4">
                    <h3 class="text-xl font-bold text-white tracking-wide">10. 受け入れ条件 (Acceptance Criteria)</h3>
                </div>

                <div class="glass-panel rounded-xl p-5 overflow-x-auto">
                    <table class="w-full text-left text-xs">
                        <thead class="bg-cyber-surface text-slate-400 font-mono border-b border-cyber-border">
                            <tr>
                                <th class="p-3">ID</th>
                                <th class="p-3">対象</th>
                                <th class="p-3">受け入れ検証条件</th>
                            </tr>
                        </thead>
                        <tbody class="divide-y divide-cyber-border/40 text-slate-300">
                            <tr>
                                <td class="p-3 font-mono text-indigo-400 font-bold">AC-001</td>
                                <td class="p-3 font-medium text-white">デッキ</td>
                                <td class="p-3">作成、一覧表示、名前・説明編集が問題なく行えること。</td>
                            </tr>
                            <tr>
                                <td class="p-3 font-mono text-indigo-400 font-bold">AC-007</td>
                                <td class="p-3 font-medium text-white">復習</td>
                                <td class="p-3">「もう一度」で1分後戻り、「正解」で10分→1日→3日...と正確に次回予定が計算されること。</td>
                            </tr>
                            <tr>
                                <td class="p-3 font-mono text-indigo-400 font-bold">AC-014</td>
                                <td class="p-3 font-medium text-white">形式選択</td>
                                <td class="p-3">作成開始時に「カード形式/問題形式」が選択でき、対応する入力欄が表示されること。</td>
                            </tr>
                            <tr>
                                <td class="p-3 font-mono text-indigo-400 font-bold">AC-017</td>
                                <td class="p-3 font-medium text-white">ロジック分離</td>
                                <td class="p-3">カード形式の復習日時と、問題形式の演習履歴が混同されずに分離処理されること。</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </section>

            <!-- 11. 実装優先順位 -->
            <section id="roadmap" class="space-y-6 pb-12">
                <div class="flex items-center gap-3 border-l-4 border-cyan-400 pl-4">
                    <h3 class="text-xl font-bold text-white tracking-wide">11. 優先順位・実装方針</h3>
                </div>

                <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                    <div class="glass-panel p-5 rounded-xl border-t-2 border-t-cyan-500">
                        <span class="text-xs font-mono text-cyan-400 uppercase block mb-1">PHASE 1 (CORE)</span>
                        <h4 class="text-sm font-bold text-white mb-2">基本コア機能</h4>
                        <p class="text-xs text-slate-400">デッキ/問題CRUD、学習フロー、カード/問題分け、メモ保存、ローカルDB、バックアップ</p>
                    </div>
                    <div class="glass-panel p-5 rounded-xl border-t-2 border-t-purple-500">
                        <span class="text-xs font-mono text-purple-400 uppercase block mb-1">PARALLEL</span>
                        <h4 class="text-sm font-bold text-white mb-2">演出 & 実績</h4>
                        <p class="text-xs text-slate-400">最重要要素として紙吹雪・サウンド演出、バッジ解除ロジックを初期段階から並行実装</p>
                    </div>
                    <div class="glass-panel p-5 rounded-xl border-t-2 border-t-slate-600 opacity-60">
                        <span class="text-xs font-mono text-slate-500 uppercase block mb-1">FUTURE</span>
                        <h4 class="text-sm font-bold text-slate-300 mb-2">拡張構想</h4>
                        <p class="text-xs text-slate-400">教師用一括配布、学習データサーバー集約、AI問題生成などのクラウド連携</p>
                    </div>
                </div>
            </section>

        </main>
    </div>

    <!-- JavaScript Data & Logic -->
    <script>
        // 機能要件 (FR-001 ~ FR-048) データ構造
        const functionalRequirements = [
            { id: "FR-001", name: "デッキ作成", cat: "デッキ", desc: "新規デッキ作成、デッキ名・説明設定" },
            { id: "FR-002", name: "デッキ編集・削除", cat: "デッキ", desc: "デッキ情報更新、削除（配下データ整合性維持）" },
            { id: "FR-003", name: "デッキ内問題一覧", cat: "デッキ", desc: "指定デッキの所属問題一覧表示" },
            { id: "FR-004", name: "作成開始時の形式選択", cat: "問題", desc: "作成開始時に「カード形式」または「問題形式」を選択" },
            { id: "FR-005", name: "問題編集・削除", cat: "問題", desc: "問題修正・削除（関連学習履歴・添付ファイルも削除）" },
            { id: "FR-006", name: "問題の追加・移動", cat: "問題", desc: "1問題1デッキ所属原則での別デッキ移動" },
            { id: "FR-007", name: "画像添付", cat: "問題", desc: "問題への画像添付および学習画面での表示" },
            { id: "FR-008", name: "参考URL", cat: "問題", desc: "問題へのURL登録および外部ブラウザ起動" },
            { id: "FR-009", name: "キーワード検索", cat: "問題", desc: "デッキ、問題、タグの横断部分一致検索" },
            { id: "FR-010", name: "一問一答", cat: "問題", desc: "問題文と解答による標準的一問一答" },
            { id: "FR-011", name: "画像付き問題", cat: "問題", desc: "画像を含む視覚的問題の出題" },
            { id: "FR-012", name: "択一選択問題", cat: "問題", desc: "複数選択肢から1つを選ぶ形式" },
            { id: "FR-013", name: "複数選択問題", cat: "問題", desc: "複数該当選択肢の回答（部分点なし、完答正解）" },
            { id: "FR-014", name: "文字入力解答", cat: "問題", desc: "完全一致型（複数正解可）または自己採点による文字入力" },
            { id: "FR-015", name: "学習開始", cat: "学習", desc: "デッキ選択による学習セッションの開始" },
            { id: "FR-016", name: "問題の逐次表示", cat: "学習", desc: "1問ずつ表示し解答は隠す。操作で開示" },
            { id: "FR-017", name: "問題間移動", cat: "学習", desc: "学習中の前後の問題への自由移動" },
            { id: "FR-018", name: "学習対象の絞り込み", cat: "学習", desc: "未学習問題のみ / 全問題の絞り込み出題" },
            { id: "FR-019", name: "途中終了・進捗保存", cat: "学習", desc: "途中終了時の未回答状態保持と再開処理" },
            { id: "FR-020", name: "テキストメモ", cat: "学習", desc: "解答時の思考・計算過程のテキスト記録" },
            { id: "FR-021", name: "手書きメモ", cat: "学習", desc: "マウス/タッチによるフリーハンド手書き記録" },
            { id: "FR-022", name: "過去メモ表示", cat: "学習", desc: "最大3回分のメモ保持と4回目以降の最古上書き" },
            { id: "FR-023", name: "カード形式の自己評価", cat: "復習", desc: "裏面確認後の「もう一度／正解」2段階評価" },
            { id: "FR-024", name: "カード形式の復習日時設定", cat: "復習", desc: "1分, 10分, 1日, 3日, 7日, 14日, 2倍の復習計算" },
            { id: "FR-025", name: "復習対象一覧", cat: "復習", desc: "復習期日到来カードの優先出題" },
            { id: "FR-026", name: "カード復習状態表示", cat: "復習", desc: "次回復習タイミングおよび学習段階の表示" },
            { id: "FR-027", name: "学習履歴", cat: "学習", desc: "日時および評価ログの記録と確認" },
            { id: "FR-028", name: "進捗表示", cat: "学習", desc: "学習数、デッキ状況、未学習/復習待ち統計" },
            { id: "FR-029", name: "問題ごとの正答率", cat: "学習", desc: "100%方式での問題単位正解率算出" },
            { id: "FR-030", name: "デッキごとの正答率", cat: "学習", desc: "100%方式でのデッキ単位正解率算出" },
            { id: "FR-031", name: "デッキエクスポート", cat: "データ", desc: "（今回の対象外）" },
            { id: "FR-032", name: "デッキインポート", cat: "データ", desc: "画像/セーブデータ読み込みのみ対象" },
            { id: "FR-033", name: "インポート検証", cat: "データ", desc: "不正ファイルの検証と取り込み拒否" },
            { id: "FR-034", name: "ローカル保存", cat: "データ", desc: "PC内完全ローカル保存（外部通信なし）" },
            { id: "FR-035", name: "メディアファイル保存", cat: "データ", desc: "画像/手書きをローカルフォルダ保存、DBパス保持" },
            { id: "FR-036", name: "バックアップ", cat: "データ", desc: "問題・履歴・画像・実績等の統合バックアップ" },
            { id: "FR-037", name: "復元", cat: "データ", desc: "バックアップからの上書きデータ復元" },
            { id: "FR-038", name: "全データ初期化", cat: "データ", desc: "事前確認ダイアログ付きの全データリセット" },
            { id: "FR-039", name: "復習設定", cat: "復習", desc: "設定画面からの復習間隔カスタマイズ" },
            { id: "FR-040", name: "出題順序設定", cat: "学習", desc: "登録順 / ランダム出題の切り替え" },
            { id: "FR-041", name: "データ操作設定", cat: "データ", desc: "履歴クリアやデータ管理操作（設定エクスポートなし）" },
            { id: "FR-042", name: "学習演出", cat: "演出", desc: "正解時の紙吹雪・サウンド演出（ON/OFF設定可）" },
            { id: "FR-043", name: "実績・バッジ", cat: "演出", desc: "条件達成時の実績解除と演出通知" },
            { id: "FR-044", name: "実績条件", cat: "演出", desc: "7日連続学習、累計100問正解等の判定（暦日単位）" },
            { id: "FR-045", name: "カード形式の作成", cat: "問題", desc: "表面・裏面の登録編集UI" },
            { id: "FR-046", name: "問題形式の作成", cat: "問題", desc: "問題文・選択肢・正解・解説の登録編集UI" },
            { id: "FR-047", name: "学習ロジックの分離", cat: "学習", desc: "カード形式（間隔反復）と問題形式（通常演習）の分離" },
            { id: "FR-048", name: "固定スケジュール計算", cat: "復習", desc: "固定間隔スケジュールによる復習計算の実行" }
        ];

        // アイコン初期化
        document.addEventListener('DOMContentLoaded', () => {
            lucide.createIcons();
            renderFRs(functionalRequirements);

            // モバイルメニュー制御
            const mobileBtn = document.getElementById('mobile-menu-btn');
            const sidebar = document.getElementById('sidebar');
            const overlay = document.getElementById('sidebar-overlay');

            mobileBtn.addEventListener('click', () => {
                sidebar.classList.toggle('-translate-x-full');
                overlay.classList.toggle('hidden');
            });

            overlay.addEventListener('click', () => {
                sidebar.classList.add('-translate-x-full');
                overlay.classList.add('hidden');
            });
        });

        // 機能要件レンダリング
        function renderFRs(items) {
            const container = document.getElementById('fr-container');
            container.innerHTML = '';

            items.forEach(item => {
                const card = document.createElement('div');
                card.className = 'glass-panel p-3.5 rounded-xl border border-cyber-border/70 hover:border-cyber-cyan/50 transition-all flex flex-col justify-between';
                
                let badgeColor = 'bg-blue-500/10 text-blue-400 border-blue-500/30';
                if(item.cat === '復習') badgeColor = 'bg-cyan-500/10 text-cyan-400 border-cyan-500/30';
                if(item.cat === '演出') badgeColor = 'bg-purple-500/10 text-purple-400 border-purple-500/30';
                if(item.cat === 'データ') badgeColor = 'bg-amber-500/10 text-amber-400 border-amber-500/30';

                card.innerHTML = `
                    <div>
                        <div class="flex items-center justify-between mb-2">
                            <span class="font-mono text-xs font-bold text-white px-2 py-0.5 bg-cyber-surface rounded border border-cyber-border">${item.id}</span>
                            <span class="text-[10px] font-mono px-2 py-0.5 rounded border ${badgeColor}">${item.cat}</span>
                        </div>
                        <h4 class="text-xs font-bold text-slate-100 mb-1">${item.name}</h4>
                        <p class="text-[11px] text-slate-400 leading-snug">${item.desc}</p>
                    </div>
                `;
                container.appendChild(card);
            });
        }

        // フィルタリング処理
        const searchInput = document.getElementById('fr-search');
        const filterSelect = document.getElementById('fr-filter');

        function filterFRs() {
            const query = searchInput.value.toLowerCase();
            const category = filterSelect.value;

            const filtered = functionalRequirements.filter(item => {
                const matchesQuery = item.id.toLowerCase().includes(query) || 
                                     item.name.toLowerCase().includes(query) || 
                                     item.desc.toLowerCase().includes(query);
                const matchesCat = category === 'ALL' || item.cat === category;
                return matchesQuery && matchesCat;
            });

            renderFRs(filtered);
        }

        searchInput.addEventListener('input', filterFRs);
        filterSelect.addEventListener('change', filterFRs);

        // サイドバー検索連携
        document.getElementById('quick-search').addEventListener('input', (e) => {
            const val = e.target.value;
            searchInput.value = val;
            filterFRs();
        });
    </script>
</body>
</html>
