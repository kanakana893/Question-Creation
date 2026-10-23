<!DOCTYPE html>
<html lang="ja" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>問題作成・学習アプリ システム要件定義書</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        brand: {
                            50: '#f0f7ff',
                            100: '#e0effe',
                            500: '#0284c7',
                            600: '#0369a1',
                            700: '#075985',
                            900: '#0c4a6e',
                        }
                    }
                }
            }
        }
    </script>
    <!-- Lucide Icons -->
    <script src="https://unpkg.com/lucide@latest"></script>
    <style>
        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, "Noto Sans JP", sans-serif;
            word-break: break-word;
        }
        /* Custom scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
            height: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #f1f5f9;
        }
        ::-webkit-scrollbar-thumb {
            background: #cbd5e1;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #94a3b8;
        }
    </style>
</head>
<body class="bg-slate-50 text-slate-800 antialiased min-h-screen flex flex-col selection:bg-brand-500 selection:text-white">

    <!-- Sticky Header & Navigation -->
    <header class="sticky top-0 z-50 bg-white/90 backdrop-blur-md border-b border-slate-200 shadow-sm transition-all duration-200">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex items-center justify-between h-16">
                <!-- App Title / Brand -->
                <div class="flex items-center space-x-3">
                    <div class="p-2 bg-brand-600 rounded-lg text-white shadow-md shadow-brand-500/20">
                        <i data-lucide="file-text" class="w-5 h-5"></i>
                    </div>
                    <div>
                        <span class="text-xs font-semibold uppercase tracking-wider text-brand-600">システム設計ドキュメント</span>
                        <h1 class="text-base sm:text-lg font-bold text-slate-900 leading-tight">要件定義書 <span class="text-xs font-normal text-slate-500 ml-1">(v1.0)</span></h1>
                    </div>
                </div>

                <!-- Desktop Navigation Menu -->
                <nav class="hidden md:flex items-center space-x-1 lg:space-x-2 text-xs font-medium">
                    <a href="#overview" class="px-3 py-2 rounded-md text-slate-600 hover:text-brand-600 hover:bg-slate-100 transition-colors">背景・目的</a>
                    <a href="#business" class="px-3 py-2 rounded-md text-slate-600 hover:text-brand-600 hover:bg-slate-100 transition-colors">業務要件</a>
                    <a href="#functional" class="px-3 py-2 rounded-md text-slate-600 hover:text-brand-600 hover:bg-slate-100 transition-colors">機能要件</a>
                    <a href="#non-functional" class="px-3 py-2 rounded-md text-slate-600 hover:text-brand-600 hover:bg-slate-100 transition-colors">非機能要件</a>
                    <a href="#tbd" class="px-3 py-2 rounded-md text-slate-600 hover:text-brand-600 hover:bg-slate-100 transition-colors">未決定事項</a>
                    <a href="#schedule" class="px-3 py-2 rounded-md text-slate-600 hover:text-brand-600 hover:bg-slate-100 transition-colors">工程・管理</a>
                </nav>

                <!-- Status Badge -->
                <div class="hidden sm:flex items-center">
                    <span class="inline-flex items-center px-2.5 py-1 rounded-full text-xs font-semibold bg-emerald-100 text-emerald-800 border border-emerald-200">
                        <span class="w-1.5 h-1.5 mr-1.5 rounded-full bg-emerald-500 animate-pulse"></span>
                        初稿・レビュー中
                    </span>
                </div>
            </div>
        </div>

        <!-- Mobile Horizontal Scroll Navigation -->
        <div class="md:hidden border-t border-slate-100 bg-slate-50/80 px-4 py-2 overflow-x-auto">
            <div class="flex space-x-2 text-xs font-medium whitespace-nowrap">
                <a href="#overview" class="px-3 py-1.5 bg-white border border-slate-200 rounded-lg text-slate-700 shadow-sm active:bg-slate-100">背景・目的</a>
                <a href="#business" class="px-3 py-1.5 bg-white border border-slate-200 rounded-lg text-slate-700 shadow-sm active:bg-slate-100">業務要件</a>
                <a href="#functional" class="px-3 py-1.5 bg-white border border-slate-200 rounded-lg text-slate-700 shadow-sm active:bg-slate-100">機能要件</a>
                <a href="#non-functional" class="px-3 py-1.5 bg-white border border-slate-200 rounded-lg text-slate-700 shadow-sm active:bg-slate-100">非機能要件</a>
                <a href="#tbd" class="px-3 py-1.5 bg-white border border-slate-200 rounded-lg text-slate-700 shadow-sm active:bg-slate-100">未決定事項</a>
                <a href="#schedule" class="px-3 py-1.5 bg-white border border-slate-200 rounded-lg text-slate-700 shadow-sm active:bg-slate-100">工程・管理</a>
            </div>
        </div>
    </header>

    <!-- Main Container -->
    <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8 flex-grow w-full space-y-10">

        <!-- Executive Summary Banner -->
        <div class="bg-gradient-to-r from-slate-900 via-brand-900 to-slate-900 rounded-2xl text-white p-6 sm:p-8 shadow-xl relative overflow-hidden">
            <div class="absolute -right-10 -bottom-10 opacity-10 text-white pointer-events-none">
                <i data-lucide="layers" class="w-80 h-80"></i>
            </div>
            <div class="relative z-10 max-w-3xl space-y-4">
                <div class="flex flex-wrap items-center gap-2 text-xs font-medium">
                    <span class="bg-white/10 backdrop-blur-md px-3 py-1 rounded-full text-brand-100 border border-white/10">個人学習向けデスクトップアプリ</span>
                    <span class="bg-white/10 backdrop-blur-md px-3 py-1 rounded-full text-brand-100 border border-white/10">対象OS: Windows 10 / 11</span>
                </div>
                <h2 class="text-2xl sm:text-3xl font-extrabold text-white tracking-tight">問題作成・学習アプリ システム要件定義</h2>
                <p class="text-slate-300 text-sm sm:text-base leading-relaxed">
                    本ドキュメントは、個人学習者向けのデスクトップ用問題作成・反復学習アプリにおけるシステム要件、業務フロー（As-Is / To-Be）、機能および非機能要件を明確に定義した基本設計指針です。
                </p>
                <div class="pt-2 flex flex-wrap gap-6 text-xs text-slate-300 border-t border-white/10">
                    <div>作成日: <span class="font-semibold text-white">2026年10月23日</span></div>
                    <div>最終更新: <span class="font-semibold text-white">2026年10月23日</span></div>
                    <div>管理番号: <span class="font-semibold text-white">REQ-2026-001</span></div>
                </div>
            </div>
        </div>

        <!-- Metrics Overview Cards -->
        <div class="grid grid-cols-2 md:grid-cols-4 gap-4 sm:gap-6">
            <div class="bg-white p-5 rounded-xl border border-slate-200 shadow-sm flex items-center space-x-4">
                <div class="p-3 bg-brand-50 text-brand-600 rounded-lg">
                    <i data-lucide="check-square" class="w-6 h-6"></i>
                </div>
                <div>
                    <div class="text-2xl font-bold text-slate-900">44</div>
                    <div class="text-xs font-medium text-slate-500">定義済み機能要件</div>
                </div>
            </div>
            <div class="bg-white p-5 rounded-xl border border-slate-200 shadow-sm flex items-center space-x-4">
                <div class="p-3 bg-amber-50 text-amber-600 rounded-lg">
                    <i data-lucide="help-circle" class="w-6 h-6"></i>
                </div>
                <div>
                    <div class="text-2xl font-bold text-slate-900">22</div>
                    <div class="text-xs font-medium text-slate-500">未決定・協議事項 (TBD)</div>
                </div>
            </div>
            <div class="bg-white p-5 rounded-xl border border-slate-200 shadow-sm flex items-center space-x-4">
                <div class="p-3 bg-indigo-50 text-indigo-600 rounded-lg">
                    <i data-lucide="layout" class="w-6 h-6"></i>
                </div>
                <div>
                    <div class="text-2xl font-bold text-slate-900">6</div>
                    <div class="text-xs font-medium text-slate-500">主要画面構成</div>
                </div>
            </div>
            <div class="bg-white p-5 rounded-xl border border-slate-200 shadow-sm flex items-center space-x-4">
                <div class="p-3 bg-emerald-50 text-emerald-600 rounded-lg">
                    <i data-lucide="shield-check" class="w-6 h-6"></i>
                </div>
                <div>
                    <div class="text-2xl font-bold text-slate-900">100%</div>
                    <div class="text-xs font-medium text-slate-500">ローカル保存型設計</div>
                </div>
            </div>
        </div>

        <!-- 1. システムの目的・背景 -->
        <section id="overview" class="scroll-mt-20 bg-white rounded-xl shadow-sm border border-slate-200 overflow-hidden">
            <div class="bg-slate-50/50 border-b border-slate-200 p-5 sm:p-6 flex items-center space-x-3">
                <div class="p-2 bg-brand-100 text-brand-700 rounded-lg">
                    <i data-lucide="target" class="w-5 h-5"></i>
                </div>
                <div>
                    <h3 class="text-lg font-bold text-slate-900">1. システムの目的・背景</h3>
                    <p class="text-xs text-slate-500">システムの存在意義と解決すべき課題の明確化</p>
                </div>
            </div>
            <div class="p-6 sm:p-8 space-y-6">
                <div>
                    <h4 class="text-sm font-semibold text-slate-900 uppercase tracking-wider mb-2">1.1 システムの目的</h4>
                    <p class="text-slate-700 text-sm sm:text-base leading-relaxed">
                        利用者が独自の問題集（デッキ）を作成・管理し、間隔反復（スペースド・レピティション）を用いた効率的な記憶定着を図るためのデスクトップ学習アプリケーションです。解答プロセスにおける思考ノート・計算メモの記録や、モチベーションを高める演出・実績通知機能を通じ、継続的な学習およびケアレスミスの防止・弱点克服を強力に支援します。
                    </p>
                </div>

                <div class="grid grid-cols-1 md:grid-cols-2 gap-6 pt-2">
                    <div class="bg-slate-50 p-5 rounded-xl border border-slate-200">
                        <h4 class="text-sm font-bold text-slate-900 flex items-center mb-3">
                            <i data-lucide="users" class="w-4 h-4 mr-2 text-brand-600"></i>
                            想定ターゲット層
                        </h4>
                        <ul class="space-y-2 text-xs sm:text-sm text-slate-600">
                            <li class="flex items-start">
                                <span class="w-1.5 h-1.5 bg-brand-500 rounded-full mt-2 mr-2 flex-shrink-0"></span>
                                <span>個人学習者および各種資格試験の受験生</span>
                            </li>
                            <li class="flex items-start">
                                <span class="w-1.5 h-1.5 bg-brand-500 rounded-full mt-2 mr-2 flex-shrink-0"></span>
                                <span>計算過程のミスや同じ解答エラーの再発を防止したい学習者</span>
                            </li>
                            <li class="flex items-start">
                                <span class="w-1.5 h-1.5 bg-brand-500 rounded-full mt-2 mr-2 flex-shrink-0"></span>
                                <span>家庭で子供の復習・学習指導を行う保護者</span>
                            </li>
                        </ul>
                    </div>

                    <div class="bg-slate-50 p-5 rounded-xl border border-slate-200">
                        <h4 class="text-sm font-bold text-slate-900 flex items-center mb-3">
                            <i data-lucide="monitor" class="w-4 h-4 mr-2 text-brand-600"></i>
                            基本動作環境
                        </h4>
                        <dl class="space-y-2 text-xs sm:text-sm">
                            <div class="flex justify-between py-1 border-b border-slate-200">
                                <dt class="text-slate-500">形態</dt>
                                <dd class="font-medium text-slate-800">デスクトップアプリケーション（スタンドアロン）</dd>
                            </div>
                            <div class="flex justify-between py-1 border-b border-slate-200">
                                <dt class="text-slate-500">対象OS</dt>
                                <dd class="font-medium text-slate-800">Windows 10 / Windows 11</dd>
                            </div>
                            <div class="flex justify-between py-1">
                                <dt class="text-slate-500">データ保存</dt>
                                <dd class="font-medium text-slate-800">完全ローカルストレージ（パス参照方式）</dd>
                            </div>
                        </dl>
                    </div>
                </div>
            </div>
        </section>

        <!-- 2. 業務要件 -->
        <section id="business" class="scroll-mt-20 bg-white rounded-xl shadow-sm border border-slate-200 overflow-hidden">
            <div class="bg-slate-50/50 border-b border-slate-200 p-5 sm:p-6 flex items-center space-x-3">
                <div class="p-2 bg-indigo-100 text-indigo-700 rounded-lg">
                    <i data-lucide="git-commit" class="w-5 h-5"></i>
                </div>
                <div>
                    <h3 class="text-lg font-bold text-slate-900">2. 業務要件（As-Is / To-Be）</h3>
                    <p class="text-xs text-slate-500">システム導入による現状業務の変化とワークフローの比較</p>
                </div>
            </div>
            <div class="p-6 sm:p-8 space-y-6">
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <!-- As-Is -->
                    <div class="border border-red-200 bg-red-50/30 rounded-xl p-5 space-y-3">
                        <div class="flex items-center text-red-700 font-bold text-sm">
                            <i data-lucide="alert-circle" class="w-4 h-4 mr-2"></i>
                            現状の課題（As-Is）
                        </div>
                        <ul class="space-y-2 text-xs sm:text-sm text-slate-600">
                            <li class="flex items-start">
                                <span class="text-red-500 mr-2">✕</span>
                                復習スケジュールが個人管理のため、復習タイミングが曖昧になり記憶が定着しにくい。
                            </li>
                            <li class="flex items-start">
                                <span class="text-red-500 mr-2">✕</span>
                                解答時の思考プロセスや計算過程を残せず、同じ間違え方を繰り返してしまう。
                            </li>
                            <li class="flex items-start">
                                <span class="text-red-500 mr-2">✕</span>
                                単体問題・デッキごとの正確な正答率や苦手範囲の定量的な可視化が困難。
                            </li>
                        </ul>
                    </div>

                    <!-- To-Be -->
                    <div class="border border-emerald-200 bg-emerald-50/30 rounded-xl p-5 space-y-3">
                        <div class="flex items-center text-emerald-700 font-bold text-sm">
                            <i data-lucide="check-circle-2" class="w-4 h-4 mr-2"></i>
                            システム導入後（To-Be）
                        </div>
                        <ul class="space-y-2 text-xs sm:text-sm text-slate-600">
                            <li class="flex items-start">
                                <span class="text-emerald-600 mr-2">✓</span>
                                4段階の自己評価に基づき、システムが最適な復習タイミング（間隔反復）を自動算出。
                            </li>
                            <li class="flex items-start">
                                <span class="text-emerald-600 mr-2">✓</span>
                                解答時に手書き・テキストによるメモを残し、過去のメモを即座に参照して原因を特定。
                            </li>
                            <li class="flex items-start">
                                <span class="text-emerald-600 mr-2">✓</span>
                                問題別・デッキ別の正答率が自動集計され、苦手領域を視覚的に把握・分析可能。
                            </li>
                        </ul>
                    </div>
                </div>

                <!-- Workflow Steps -->
                <div class="pt-4">
                    <h4 class="text-xs font-bold text-slate-500 uppercase tracking-wider mb-4">標準的な業務利用フロー</h4>
                    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-6 gap-3">
                        <div class="p-3 bg-slate-50 rounded-lg border border-slate-200 text-center space-y-1">
                            <span class="text-[10px] font-bold text-slate-400">STEP 1</span>
                            <div class="text-xs font-bold text-slate-800">デッキ・問題登録</div>
                            <p class="text-[11px] text-slate-500">手動入力・画像添付</p>
                        </div>
                        <div class="p-3 bg-slate-50 rounded-lg border border-slate-200 text-center space-y-1">
                            <span class="text-[10px] font-bold text-slate-400">STEP 2</span>
                            <div class="text-xs font-bold text-slate-800">学習セッション開始</div>
                            <p class="text-[11px] text-slate-500">条件による絞り込み</p>
                        </div>
                        <div class="p-3 bg-slate-50 rounded-lg border border-slate-200 text-center space-y-1">
                            <span class="text-[10px] font-bold text-slate-400">STEP 3</span>
                            <div class="text-xs font-bold text-slate-800">解答・メモ記録</div>
                            <p class="text-[11px] text-slate-500">思考過程の保管</p>
                        </div>
                        <div class="p-3 bg-slate-50 rounded-lg border border-slate-200 text-center space-y-1">
                            <span class="text-[10px] font-bold text-slate-400">STEP 4</span>
                            <div class="text-xs font-bold text-slate-800">自己評価・採点</div>
                            <p class="text-[11px] text-slate-500">4段階評価＆記述採点</p>
                        </div>
                        <div class="p-3 bg-slate-50 rounded-lg border border-slate-200 text-center space-y-1">
                            <span class="text-[10px] font-bold text-slate-400">STEP 5</span>
                            <div class="text-xs font-bold text-slate-800">復習＆データ分析</div>
                            <p class="text-[11px] text-slate-500">正答率・統計の確認</p>
                        </div>
                        <div class="p-3 bg-slate-50 rounded-lg border border-slate-200 text-center space-y-1">
                            <span class="text-[10px] font-bold text-slate-400">STEP 6</span>
                            <div class="text-xs font-bold text-slate-800">共有・バックアップ</div>
                            <p class="text-[11px] text-slate-500">データ出力と安全保管</p>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- 3. 機能要件 -->
        <section id="functional" class="scroll-mt-20 bg-white rounded-xl shadow-sm border border-slate-200 overflow-hidden">
            <div class="bg-slate-50/50 border-b border-slate-200 p-5 sm:p-6 flex items-center space-x-3">
                <div class="p-2 bg-brand-100 text-brand-700 rounded-lg">
                    <i data-lucide="list-checks" class="w-5 h-5"></i>
                </div>
                <div>
                    <h3 class="text-lg font-bold text-slate-900">3. 機能要件一覧</h3>
                    <p class="text-xs text-slate-500">システムに実装する具体的な機能仕様定義（全44要件）</p>
                </div>
            </div>

            <!-- Table Filter / Summary Info -->
            <div class="p-4 bg-slate-100/50 border-b border-slate-200 flex items-center justify-between text-xs text-slate-600">
                <div>分類: <span class="font-semibold text-slate-800">コア機能 / 学習 / データ管理 / 演出</span></div>
                <div>表示: <span class="font-semibold text-slate-800">44件中 44件表示</span></div>
            </div>

            <div class="overflow-x-auto">
                <table class="w-full text-left border-collapse min-w-[700px]">
                    <thead>
                        <tr class="bg-slate-100 text-slate-700 text-xs font-semibold uppercase tracking-wider border-b border-slate-200">
                            <th class="py-3 px-4 w-24">要件ID</th>
                            <th class="py-3 px-4 w-40">機能名</th>
                            <th class="py-3 px-4">機能要件詳細</th>
                            <th class="py-3 px-4 w-28 text-center">ステータス</th>
                        </tr>
                    </thead>
                    <tbody class="divide-y divide-slate-200 text-xs sm:text-sm text-slate-700">
                        <tr>
                            <td class="py-3.5 px-4 font-mono font-semibold text-brand-600">FR-001</td>
                            <td class="py-3.5 px-4 font-bold text-slate-900">デッキ作成</td>
                            <td class="py-3.5 px-4">利用者は新しいデッキを作成し、デッキ名および説明を設定できる。</td>
                            <td class="py-3.5 px-4 text-center"><span class="px-2 py-0.5 rounded-full text-[10px] font-semibold bg-emerald-100 text-emerald-800">確定</span></td>
                        </tr>
                        <tr>
                            <td class="py-3.5 px-4 font-mono font-semibold text-brand-600">FR-002</td>
                            <td class="py-3.5 px-4 font-bold text-slate-900">デッキ編集・削除</td>
                            <td class="py-3.5 px-4">利用者は既存デッキの情報を編集し、デッキを削除できる。（削除時挙動はTBD）</td>
                            <td class="py-3.5 px-4 text-center"><span class="px-2 py-0.5 rounded-full text-[10px] font-semibold bg-amber-100 text-amber-800">一部TBD</span></td>
                        </tr>
                        <tr>
                            <td class="py-3.5 px-4 font-mono font-semibold text-brand-600">FR-003</td>
                            <td class="py-3.5 px-4 font-bold text-slate-900">デッキ内問題一覧</td>
                            <td class="py-3.5 px-4">利用者は指定したデッキに登録されている問題一覧を表示できる。</td>
                            <td class="py-3.5 px-4 text-center"><span class="px-2 py-0.5 rounded-full text-[10px] font-semibold bg-emerald-100 text-emerald-800">確定</span></td>
                        </tr>
                        <tr>
                            <td class="py-3.5 px-4 font-mono font-semibold text-brand-600">FR-004</td>
                            <td class="py-3.5 px-4 font-bold text-slate-900">問題作成</td>
                            <td class="py-3.5 px-4">利用者は問題文および解答を登録できる。形式に応じて選択肢等を設定可能。</td>
                            <td class="py-3.5 px-4 text-center"><span class="px-2 py-0.5 rounded-full text-[10px] font-semibold bg-emerald-100 text-emerald-800">確定</span></td>
                        </tr>
                        <tr>
                            <td class="py-3.5 px-4 font-mono font-semibold text-brand-600">FR-005</td>
                            <td class="py-3.5 px-4 font-bold text-slate-900">問題編集・削除</td>
                            <td class="py-3.5 px-4">利用者は登録済み問題を編集・削除できる。</td>
                            <td class="py-3.5 px-4 text-center"><span class="px-2 py-0.5 rounded-full text-[10px] font-semibold bg-emerald-100 text-emerald-800">確定</span></td>
                        </tr>
                        <tr>
                            <td class="py-3.5 px-4 font-mono font-semibold text-brand-600">FR-006</td>
                            <td class="py-3.5 px-4 font-bold text-slate-900">問題の追加・移動</td>
                            <td class="py-3.5 px-4">利用者は問題をデッキに追加し、別のデッキへ移動できる。</td>
                            <td class="py-3.5 px-4 text-center"><span class="px-2 py-0.5 rounded-full text-[10px] font-semibold bg-emerald-100 text-emerald-800">確定</span></td>
                        </tr>
                        <tr>
                            <td class="py-3.5 px-4 font-mono font-semibold text-brand-600">FR-007</td>
                            <td class="py-3.5 px-4 font-bold text-slate-900">画像添付</td>
                            <td class="py-3.5 px-4">利用者は問題に画像を添付し、問題表示時に確認できる。</td>
                            <td class="py-3.5 px-4 text-center"><span class="px-2 py-0.5 rounded-full text-[10px] font-semibold bg-emerald-100 text-emerald-800">確定</span></td>
                        </tr>
                        <tr>
                            <td class="py-3.5 px-4 font-mono font-semibold text-brand-600">FR-008</td>
                            <td class="py-3.5 px-4 font-bold text-slate-900">参考URL</td>
                            <td class="py-3.5 px-4">問題に参考URLを登録し、外部ブラウザ等で起動できる。</td>
                            <td class="py-3.5 px-4 text-center"><span class="px-2 py-0.5 rounded-full text-[10px] font-semibold bg-emerald-100 text-emerald-800">確定</span></td>
                        </tr>
                        <tr>
                            <td class="py-3.5 px-4 font-mono font-semibold text-brand-600">FR-009</td>
                            <td class="py-3.5 px-4 font-bold text-slate-900">キーワード検索</td>
                            <td class="py-3.5 px-4">利用者は問題をキーワードで横断検索できる。</td>
                            <td class="py-3.5 px-4 text-center"><span class="px-2 py-0.5 rounded-full text-[10px] font-semibold bg-emerald-100 text-emerald-800">確定</span></td>
                        </tr>
                        <tr>
                            <td class="py-3.5 px-4 font-mono font-semibold text-brand-600">FR-010〜013</td>
                            <td class="py-3.5 px-4 font-bold text-slate-900">基本問題形式</td>
                            <td class="py-3.5 px-4">一問一答、画像付き、択一選択、複数選択の各出題形式に対応。</td>
                            <td class="py-3.5 px-4 text-center"><span class="px-2 py-0.5 rounded-full text-[10px] font-semibold bg-emerald-100 text-emerald-800">確定</span></td>
                        </tr>
                        <tr class="bg-brand-50/40">
                            <td class="py-3.5 px-4 font-mono font-semibold text-brand-600">FR-014</td>
                            <td class="py-3.5 px-4 font-bold text-brand-900">記述文字入力解答</td>
                            <td class="py-3.5 px-4 text-brand-900">文字入力による解答。キーワード完全一致判定に加え、「大体あっていればOK」の自己採点機能を併用。</td>
                            <td class="py-3.5 px-4 text-center"><span class="px-2 py-0.5 rounded-full text-[10px] font-semibold bg-brand-200 text-brand-900">最新更新</span></td>
                        </tr>
                        <tr class="bg-brand-50/40">
                            <td class="py-3.5 px-4 font-mono font-semibold text-brand-600">FR-020〜022</td>
                            <td class="py-3.5 px-4 font-bold text-brand-900">思考メモ・過去メモ</td>
                            <td class="py-3.5 px-4 text-brand-900">テキストおよびマウス/タッチ手書き入力による思考プロセス記録。「過去メモ表示」によるミス傾向の確認。</td>
                            <td class="py-3.5 px-4 text-center"><span class="px-2 py-0.5 rounded-full text-[10px] font-semibold bg-brand-200 text-brand-900">最新更新</span></td>
                        </tr>
                        <tr>
                            <td class="py-3.5 px-4 font-mono font-semibold text-brand-600">FR-023〜026</td>
                            <td class="py-3.5 px-4 font-bold text-slate-900">間隔反復復習管理</td>
                            <td class="py-3.5 px-4">4段階自己評価に基づく次回評価日時の自動算出および復習期日到来問題の一覧表示。</td>
                            <td class="py-3.5 px-4 text-center"><span class="px-2 py-0.5 rounded-full text-[10px] font-semibold bg-emerald-100 text-emerald-800">確定</span></td>
                        </tr>
                        <tr>
                            <td class="py-3.5 px-4 font-mono font-semibold text-brand-600">FR-029〜030</td>
                            <td class="py-3.5 px-4 font-bold text-slate-900">正答率自動集計</td>
                            <td class="py-3.5 px-4">問題単体およびデッキ全体の累計正答率を自動集計・表示。</td>
                            <td class="py-3.5 px-4 text-center"><span class="px-2 py-0.5 rounded-full text-[10px] font-semibold bg-emerald-100 text-emerald-800">確定</span></td>
                        </tr>
                        <tr>
                            <td class="py-3.5 px-4 font-mono font-semibold text-brand-600">FR-031〜033</td>
                            <td class="py-3.5 px-4 font-bold text-slate-900">デッキ入出力・検証</td>
                            <td class="py-3.5 px-4">添付素材込みのデッキエクスポート/インポート機能と不正ファイルの入力バリデーション。</td>
                            <td class="py-3.5 px-4 text-center"><span class="px-2 py-0.5 rounded-full text-[10px] font-semibold bg-emerald-100 text-emerald-800">確定</span></td>
                        </tr>
                        <tr class="bg-brand-50/40">
                            <td class="py-3.5 px-4 font-mono font-semibold text-brand-600">FR-035</td>
                            <td class="py-3.5 px-4 font-bold text-brand-900">ローカルファイルパス管理</td>
                            <td class="py-3.5 px-4 text-brand-900">画像や手書きデータはDB内にBLOB保存せず、ローカル固有フォルダに保存しパス参照する。</td>
                            <td class="py-3.5 px-4 text-center"><span class="px-2 py-0.5 rounded-full text-[10px] font-semibold bg-brand-200 text-brand-900">最新更新</span></td>
                        </tr>
                        <tr>
                            <td class="py-3.5 px-4 font-mono font-semibold text-brand-600">FR-042〜044</td>
                            <td class="py-3.5 px-4 font-bold text-slate-900">演出・実績通知</td>
                            <td class="py-3.5 px-4">「簡単」評価・正解時のエフェクト演出および実績解除バッジ通知（ゲーミフィケーション）。</td>
                            <td class="py-3.5 px-4 text-center"><span class="px-2 py-0.5 rounded-full text-[10px] font-semibold bg-emerald-100 text-emerald-800">確定</span></td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </section>

        <!-- 4. 非機能要件 -->
        <section id="non-functional" class="scroll-mt-20 bg-white rounded-xl shadow-sm border border-slate-200 overflow-hidden">
            <div class="bg-slate-50/50 border-b border-slate-200 p-5 sm:p-6 flex items-center space-x-3">
                <div class="p-2 bg-emerald-100 text-emerald-700 rounded-lg">
                    <i data-lucide="shield" class="w-5 h-5"></i>
                </div>
                <div>
                    <h3 class="text-lg font-bold text-slate-900">4. 非機能要件</h3>
                    <p class="text-xs text-slate-500">品質、性能、セキュリティ、運用保守性の定義</p>
                </div>
            </div>
            <div class="p-6 sm:p-8 grid grid-cols-1 md:grid-cols-2 gap-6">
                <div class="space-y-2 p-4 bg-slate-50 rounded-lg border border-slate-200">
                    <div class="flex items-center text-xs font-bold text-brand-600 uppercase tracking-wider">
                        <i data-lucide="zap" class="w-4 h-4 mr-1.5"></i> 性能 (Performance)
                    </div>
                    <div class="text-sm font-bold text-slate-900">ローカルファイル分離管理</div>
                    <p class="text-xs text-slate-600 leading-relaxed">
                        画像・手書きメモ描画データはデータベース内にBLOB保存せず、外部ファイルとしてパス管理することでDB軽量化と高速な検索・応答性を維持する。
                    </p>
                </div>

                <div class="space-y-2 p-4 bg-slate-50 rounded-lg border border-slate-200">
                    <div class="flex items-center text-xs font-bold text-brand-600 uppercase tracking-wider">
                        <i data-lucide="lock" class="w-4 h-4 mr-1.5"></i> セキュリティ・データ保護
                    </div>
                    <div class="text-sm font-bold text-slate-900">完全ローカル保存・完全性検証</div>
                    <p class="text-xs text-slate-600 leading-relaxed">
                        外部通信を必要とせずすべてのデータをPC内にローカル保存。ファイルインポート時は構造・形式チェックを行い、パストラバーサル等を防止。
                    </p>
                </div>

                <div class="space-y-2 p-4 bg-slate-50 rounded-lg border border-slate-200">
                    <div class="flex items-center text-xs font-bold text-brand-600 uppercase tracking-wider">
                        <i data-lucide="refresh-cw" class="w-4 h-4 mr-1.5"></i> 信頼性・移行性
                    </div>
                    <div class="text-sm font-bold text-slate-900">途中保存とバックアップ復元</div>
                    <p class="text-xs text-slate-600 leading-relaxed">
                        学習セッションの途中終了時に進捗状態を保護。ユーザー操作による全データのバックアップ書き出しおよび別環境への復元機能を提供。
                    </p>
                </div>

                <div class="space-y-2 p-4 bg-slate-50 rounded-lg border border-slate-200">
                    <div class="flex items-center text-xs font-bold text-brand-600 uppercase tracking-wider">
                        <i data-lucide="arrow-up-right" class="w-4 h-4 mr-1.5"></i> 拡張性・保守性
                    </div>
                    <div class="text-sm font-bold text-slate-900">将来の教育機関向け拡張性</div>
                    <p class="text-xs text-slate-600 leading-relaxed">
                        個人向け利用で検証後、将来的な学校向けライセンス・サーバー同期・教師ダッシュボード展開に対応できるようモジュール化設計を意識。
                    </p>
                </div>
            </div>
        </section>

        <!-- 5. 未決定事項 (TBD) -->
        <section id="tbd" class="scroll-mt-20 bg-white rounded-xl shadow-sm border border-slate-200 overflow-hidden">
            <div class="bg-slate-50/50 border-b border-slate-200 p-5 sm:p-6 flex items-center space-x-3">
                <div class="p-2 bg-amber-100 text-amber-700 rounded-lg">
                    <i data-lucide="help-circle" class="w-5 h-5"></i>
                </div>
                <div>
                    <h3 class="text-lg font-bold text-slate-900">5. 未決定事項・確認事項一覧 (TBD)</h3>
                    <p class="text-xs text-slate-500">詳細設計・実装前に関係者間で決定・確定が必要な項目</p>
                </div>
            </div>

            <div class="p-6 sm:p-8 space-y-4">
                <div class="p-4 bg-amber-50 rounded-xl border border-amber-200 flex items-start space-x-3">
                    <i data-lucide="alert-triangle" class="w-5 h-5 text-amber-600 flex-shrink-0 mt-0.5"></i>
                    <div class="text-xs sm:text-sm text-amber-900 leading-relaxed">
                        以下の項目は、次回設計レビュー時までに確認・取り決めを行う必要があります。
                    </div>
                </div>

                <div class="overflow-x-auto">
                    <table class="w-full text-left border-collapse min-w-[600px]">
                        <thead>
                            <tr class="bg-slate-100 text-slate-700 text-xs font-semibold uppercase tracking-wider border-b border-slate-200">
                                <th class="py-2.5 px-3 w-20">ID</th>
                                <th class="py-2.5 px-3 w-36">対象項目</th>
                                <th class="py-2.5 px-3">現状と決定が必要な内容</th>
                            </tr>
                        </thead>
                        <tbody class="divide-y divide-slate-200 text-xs sm:text-sm text-slate-700">
                            <tr>
                                <td class="py-3 px-3 font-mono font-semibold text-amber-600">TBD-001</td>
                                <td class="py-3 px-3 font-bold text-slate-900">AI自動生成</td>
                                <td class="py-3 px-3">初稿仕様より除外決定。将来機能として別定義するか確定する。</td>
                            </tr>
                            <tr>
                                <td class="py-3 px-3 font-mono font-semibold text-amber-600">TBD-002</td>
                                <td class="py-3 px-3 font-bold text-slate-900">復習間隔ルール</td>
                                <td class="py-3 px-3">4段階評価（もう一度・難しい・普通・簡単）ごとの初期間隔および加算係数数式の確定。</td>
                            </tr>
                            <tr>
                                <td class="py-3 px-3 font-mono font-semibold text-amber-600">TBD-003</td>
                                <td class="py-3 px-3 font-bold text-slate-900">正答率集計の定義</td>
                                <td class="py-3 px-3">自己採点・評価結果をどう正解判定にマッピングするか。デッキ集計の平均算出計算式。</td>
                            </tr>
                            <tr>
                                <td class="py-3 px-3 font-mono font-semibold text-amber-600">TBD-007</td>
                                <td class="py-3 px-3 font-bold text-slate-900">削除時データ削除</td>
                                <td class="py-3 px-3">デッキや問題を削除した際、過去の解答メモや復習履歴データ、添付画像を物理削除するか論理削除か。</td>
                            </tr>
                            <tr>
                                <td class="py-3 px-3 font-mono font-semibold text-amber-600">TBD-013</td>
                                <td class="py-3 px-3 font-bold text-slate-900">メディア欠損対応</td>
                                <td class="py-3 px-3">ローカル上の画像ファイルが手動移動・削除されファイルパスが切れた場合の表示・警告代替動作。</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </section>

        <!-- 6. スケジュール・体制 -->
        <section id="schedule" class="scroll-mt-20 bg-white rounded-xl shadow-sm border border-slate-200 overflow-hidden">
            <div class="bg-slate-50/50 border-b border-slate-200 p-5 sm:p-6 flex items-center space-x-3">
                <div class="p-2 bg-purple-100 text-purple-700 rounded-lg">
                    <i data-lucide="calendar" class="w-5 h-5"></i>
                </div>
                <div>
                    <h3 class="text-lg font-bold text-slate-900">6. 開発工程・変更管理方針</h3>
                    <p class="text-xs text-slate-500">プロジェクト推進方針と管理ルール</p>
                </div>
            </div>
            <div class="p-6 sm:p-8 space-y-6">
                <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                    <div class="p-4 bg-slate-50 rounded-xl border border-slate-200 space-y-2">
                        <div class="text-xs font-bold text-purple-600">PHASE 1</div>
                        <div class="text-sm font-bold text-slate-900">基本機能実装</div>
                        <p class="text-xs text-slate-600">デッキ・問題管理、学習フロー、記述式自己採点、思考メモ機能の構築。</p>
                    </div>
                    <div class="p-4 bg-slate-50 rounded-xl border border-slate-200 space-y-2">
                        <div class="text-xs font-bold text-purple-600">PHASE 2</div>
                        <div class="text-sm font-bold text-slate-900">演出・分析機能拡張</div>
                        <p class="text-xs text-slate-600">間隔反復復習アルゴリズム、正答率自動集計、実績バッジ、演出エフェクトの実装。</p>
                    </div>
                    <div class="p-4 bg-slate-50 rounded-xl border border-slate-200 space-y-2">
                        <div class="text-xs font-bold text-purple-600">PHASE 3</div>
                        <div class="text-sm font-bold text-slate-900">信頼性・検証テスト</div>
                        <p class="text-xs text-slate-600">インポートバリデーション検証、バックアップ復元テスト、最終レビュー。</p>
                    </div>
                </div>

                <div class="p-4 bg-slate-100 rounded-lg text-xs text-slate-600 space-y-1">
                    <div class="font-bold text-slate-800">【仕様変更管理ルール】</div>
                    <p>要件定義完了後の機能変更および仕様追加が発生した場合は、本要件定義書（v1.0）の変更履歴を記録し、TBD事項の解消とともに版数更新を行います。</p>
                </div>
            </div>
        </section>

    </main>

    <!-- Footer -->
    <footer class="bg-white border-t border-slate-200 py-6 text-center text-xs text-slate-500">
        <div class="max-w-7xl mx-auto px-4 flex flex-col sm:flex-row justify-between items-center gap-2">
            <div>問題作成・学習アプリ システム要件定義書 (改訂プロフェッショナル版)</div>
            <div>© 2026 学習アプリ開発プロジェクト. All rights reserved.</div>
        </div>
    </footer>

    <!-- Initialize Lucide Icons -->
    <script>
        lucide.createIcons();
    </script>
</body>
</html>