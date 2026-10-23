<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>問題作成・学習アプリ 統合仕様書・要件定義書（改訂版）</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
        }
        .markdown-body { box-sizing: border-box; min-width: 200px; max-width: 980px; margin: 0 auto; padding: 45px; }
        @media (max-width: 767px) { .markdown-body { padding: 15px; } }
    </style>
</head>
<body class="bg-slate-50 text-slate-800 antialiased min-h-screen flex flex-col">

    <div class="container-lg px-3 my-5 markdown-body w-full">
      
    <!-- Header -->
    <header class="bg-white border-b border-slate-200 shadow-sm py-8 px-4 sm:px-8 mb-8 rounded-xl">
        <div class="max-w-4xl mx-auto">
            <h1 class="text-3xl font-bold text-slate-900 mb-2">問題作成・学習アプリ 統合仕様書・要件定義書</h1>
            <div class="flex flex-wrap gap-4 text-sm text-slate-600">
                <span class="bg-slate-100 px-3 py-1 rounded-full">アプリ形態：デスクトップアプリ（案）</span>
                <span class="bg-slate-100 px-3 py-1 rounded-full">対象OS：Windows 10 / 11（案）</span>
            </div>
        </div>
    </header>

    <!-- Main Content -->
    <main class="max-w-4xl mx-auto px-4 sm:px-8 flex-grow w-full space-y-10 pb-16">

        <!-- 1. アプリ概要・目的 -->
        <section class="bg-white rounded-xl shadow-sm border border-slate-200 p-6 sm:p-8">
            <h2 class="text-xl font-bold text-slate-900 border-b border-slate-100 pb-3 mb-4 flex items-center gap-2" id="1-アプリ概要・目的">
                <span class="text-indigo-600">1.</span> アプリ概要・目的
            </h2>
            <p class="text-slate-700 leading-relaxed">
                ユーザーが独自の問題やデッキ（問題集）を作成・管理し、間隔反復（スペースド・レピティション）を用いた効率的な学習と、学習意欲を極限まで高める演出（ドパガキ用演出・実績機能）、さらに「なぜそう解答したか」の思考プロセスや計算の軌跡を記録・確認できるメモ機能によって、継続的な学習と効果的な弱点克服・記憶定着をサポートするアプリケーション。
            </p>
            
            <div class="mt-6 p-4 bg-indigo-50/50 rounded-lg border border-indigo-100">
                <h3 class="font-bold text-indigo-900 mb-2" id="想定ターゲット層">想定ターゲット層</h3>
                <ul class="list-disc list-inside space-y-2 text-slate-700 text-sm">
                    <li><strong>メインターゲット（一般家庭）：</strong>個人学習者、資格勉強をする社会人、計算問題などでケアレスミスや同じ間違いを繰り返したくない人、子供の学習をサポートする保護者など。</li>
                    <li><strong>将来的な展開目標（学校法人）：</strong>教師が一括でデッキを作成し、生徒に配布・学習進捗を管理できる教育機関向けライセンス展開も視野に入れる。</li>
                </ul>
            </div>
        </section>

        <!-- 2. 機能一覧 -->
        <section class="bg-white rounded-xl shadow-sm border border-slate-200 p-6 sm:p-8 space-y-8">
            <h2 class="text-xl font-bold text-slate-900 border-b border-slate-100 pb-3 mb-4 flex items-center gap-2" id="2-機能一覧">
                <span class="text-indigo-600">2.</span> 機能一覧
            </h2>

            <!-- 2.1 問題・デッキの管理 -->
            <div>
                <h3 class="text-lg font-semibold text-slate-800 mb-3" id="2-1-問題・デッキの管理">2.1 問題・デッキの管理</h3>
                <div class="overflow-x-auto">
                    <table class="w-full text-left border-collapse">
                        <thead>
                            <tr class="bg-slate-100 text-slate-700 text-sm">
                                <th class="py-3 px-4 font-semibold rounded-l-lg">機能名</th>
                                <th class="py-3 px-4 font-semibold rounded-r-lg">機能概要</th>
                            </tr>
                        </thead>
                        <tbody class="divide-y divide-slate-100 text-sm text-slate-600">
                            <tr>
                                <td class="py-3 px-4 font-medium text-slate-800 align-top whitespace-nowrap">デッキ管理</td>
                                <td class="py-3 px-4">デッキ（問題集）を作成・編集・削除する。デッキ名や説明を設定する。指定したデッキ内の問題一覧を表示する。</td>
                            </tr>
                            <tr>
                                <td class="py-3 px-4 font-medium text-slate-800 align-top whitespace-nowrap">問題管理</td>
                                <td class="py-3 px-4">問題を作成・編集・削除する。問題をデッキに追加・移動する。問題文と解答を登録する。</td>
                            </tr>
                            <tr>
                                <td class="py-3 px-4 font-medium text-slate-800 align-top whitespace-nowrap">メディア・リンク</td>
                                <td class="py-3 px-4">問題に画像を添付する。問題に参考URLを登録し、クリックして開けるようにする。</td>
                            </tr>
                            <tr>
                                <td class="py-3 px-4 font-medium text-slate-800 align-top whitespace-nowrap">検索</td>
                                <td class="py-3 px-4">問題をキーワードで横断的に検索する。</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>

            <!-- 2.2 問題形式 -->
            <div>
                <h3 class="text-lg font-semibold text-slate-800 mb-3" id="2-2-問題形式">2.2 問題形式</h3>
                <div class="overflow-x-auto">
                    <table class="w-full text-left border-collapse">
                        <thead>
                            <tr class="bg-slate-100 text-slate-700 text-sm">
                                <th class="py-3 px-4 font-semibold rounded-l-lg">形式名</th>
                                <th class="py-3 px-4 font-semibold rounded-r-lg">概要</th>
                            </tr>
                        </thead>
                        <tbody class="divide-y divide-slate-100 text-sm text-slate-600">
                            <tr>
                                <td class="py-3 px-4 font-medium text-slate-800 align-top whitespace-nowrap">一問一答形式</td>
                                <td class="py-3 px-4">問題文と解答によるシンプルな確認形式。</td>
                            </tr>
                            <tr>
                                <td class="py-3 px-4 font-medium text-slate-800 align-top whitespace-nowrap">画像付き問題</td>
                                <td class="py-3 px-4">画像を視覚情報として伴う問題。</td>
                            </tr>
                            <tr>
                                <td class="py-3 px-4 font-medium text-slate-800 align-top whitespace-nowrap">択一選択問題</td>
                                <td class="py-3 px-4">複数の選択肢から1つ選ぶ問題。</td>
                            </tr>
                            <tr>
                                <td class="py-3 px-4 font-medium text-slate-800 align-top whitespace-nowrap">複数選択問題</td>
                                <td class="py-3 px-4">複数の選択肢から該当するものを複数選ぶ問題。</td>
                            </tr>
                            <tr class="bg-indigo-50/30">
                                <td class="py-3 px-4 font-medium text-slate-800 align-top whitespace-nowrap">
                                    記述問題（文字入力解答）<br>
                                    <span class="text-[10px] font-bold text-white bg-indigo-500 px-2 py-0.5 rounded-full mt-1 inline-block">UPDATE</span>
                                </td>
                                <td class="py-3 px-4 text-indigo-900">
                                    文字入力で解答する問題。<br>
                                    ・<strong>単語完全一致判定</strong>：設定されたキーワード・正解ワードと完全に一致しているかを自動判定する。<br>
                                    ・<strong>自己採点機能（大体あっていればOK）</strong>：完全一致しなくても、ユーザー自身が「大体あっている（ニュアンスが合致している）」と判断した場合は正解扱いにできる柔軟な採点機能を備える。
                                </td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>

            <!-- 2.3 学習 -->
            <div>
                <h3 class="text-lg font-semibold text-slate-800 mb-3" id="2-3-学習">2.3 学習</h3>
                <div class="overflow-x-auto">
                    <table class="w-full text-left border-collapse">
                        <thead>
                            <tr class="bg-slate-100 text-slate-700 text-sm">
                                <th class="py-3 px-4 font-semibold rounded-l-lg">機能名</th>
                                <th class="py-3 px-4 font-semibold rounded-r-lg">機能概要</th>
                            </tr>
                        </thead>
                        <tbody class="divide-y divide-slate-100 text-sm text-slate-600">
                            <tr>
                                <td class="py-3 px-4 font-medium text-slate-800 align-top whitespace-nowrap">学習の開始・フロー</td>
                                <td class="py-3 px-4">デッキを選んで学習を開始する。問題を1問ずつ表示する。解答を隠した状態で問題を表示し、操作して解答を確認する。</td>
                            </tr>
                            <tr class="bg-indigo-50/30">
                                <td class="py-3 px-4 font-medium text-slate-800 align-top whitespace-nowrap">
                                    解答メモ・思考プロセス記録<br>
                                    <span class="text-[10px] font-bold text-white bg-indigo-500 px-2 py-0.5 rounded-full mt-1 inline-block">NEW</span>
                                </td>
                                <td class="py-3 px-4 text-indigo-900">
                                    学習中（または解答時）に、自分が「なぜそう解答したか」の考え方や計算プロセスを記録できるメモ機能。<br>
                                    ・<strong>入力方法</strong>：テキストベースの入力に加え、マウスやタッチ操作（カーソル・ペン）による手書き・フリーハンド描画の両方に対応し、計算問題の式や図なども直感的に残せる。<br>
                                    ・<strong>閲覧機能</strong>：学習画面や履歴から「メモ表示ボタン」を押すことで、前回自分がどのような考え方・ミスで解答したかをいつでも確認でき、同じミスの繰り返しを防ぐ。
                                </td>
                            </tr>
                            <tr>
                                <td class="py-3 px-4 font-medium text-slate-800 align-top whitespace-nowrap">自己評価</td>
                                <td class="py-3 px-4">解答を確認したあと、自分の覚え具合を「もう一度・難しい・普通・簡単」から評価する。記述式の場合は「大体あっていればOK」の自己採点も併せて実施する。</td>
                            </tr>
                            <tr>
                                <td class="py-3 px-4 font-medium text-slate-800 align-top whitespace-nowrap">ナビゲーション</td>
                                <td class="py-3 px-4">学習中に前の問題へ戻る、または次の問題へ進む。</td>
                            </tr>
                            <tr>
                                <td class="py-3 px-4 font-medium text-slate-800 align-top whitespace-nowrap">進捗保存・絞り込み</td>
                                <td class="py-3 px-4">学習を途中で終了し、進捗を保存する。未学習の問題だけ、または指定したデッキの全問題を学習する。</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>

            <!-- 2.4 復習・記憶状況の管理 -->
            <div>
                <h3 class="text-lg font-semibold text-slate-800 mb-3" id="2-4-復習・記憶状況の管理">2.4 復習・記憶状況の管理</h3>
                <div class="overflow-x-auto">
                    <table class="w-full text-left border-collapse">
                        <thead>
                            <tr class="bg-slate-100 text-slate-700 text-sm">
                                <th class="py-3 px-4 font-semibold rounded-l-lg">機能名</th>
                                <th class="py-3 px-4 font-semibold rounded-r-lg">機能概要</th>
                            </tr>
                        </thead>
                        <tbody class="divide-y divide-slate-100 text-sm text-slate-600">
                            <tr>
                                <td class="py-3 px-4 font-medium text-slate-800 align-top whitespace-nowrap">スケジュール管理</td>
                                <td class="py-3 px-4">評価に応じて次回の復習日時を設定する（スペースド・レピティション）。復習時期になった問題を一覧表示し、まとめて学習する。</td>
                            </tr>
                            <tr>
                                <td class="py-3 px-4 font-medium text-slate-800 align-top whitespace-nowrap">ステータス・履歴</td>
                                <td class="py-3 px-4">問題ごとの次回復習日時と学習状態を表示する。過去の学習履歴を確認する。</td>
                            </tr>
                            <tr>
                                <td class="py-3 px-4 font-medium text-slate-800 align-top whitespace-nowrap">設定変更</td>
                                <td class="py-3 px-4">復習間隔の初期値を設定画面から変更する。</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>

            <!-- 2.5 学習履歴・進捗・正答率収集 -->
            <div>
                <h3 class="text-lg font-semibold text-slate-800 mb-3" id="2-5-学習履歴・進捗・正答率">2.5 学習履歴・進捗・正答率</h3>
                <div class="overflow-x-auto">
                    <table class="w-full text-left border-collapse">
                        <thead>
                            <tr class="bg-slate-100 text-slate-700 text-sm">
                                <th class="py-3 px-4 font-semibold rounded-l-lg">機能名</th>
                                <th class="py-3 px-4 font-semibold rounded-r-lg">機能概要</th>
                            </tr>
                        </thead>
                        <tbody class="divide-y divide-slate-100 text-sm text-slate-600">
                            <tr>
                                <td class="py-3 px-4 font-medium text-slate-800 align-top whitespace-nowrap">進捗表示</td>
                                <td class="py-3 px-4">学習した問題数を表示する。デッキごとの学習状況を表示する。未学習・復習待ち・復習期限到来などの状態を確認する。</td>
                            </tr>
                            <tr>
                                <td class="py-3 px-4 font-medium text-slate-800 align-top whitespace-nowrap">ログ記録</td>
                                <td class="py-3 px-4">学習した日時と問題ごとの評価を記録する。</td>
                            </tr>
                            <tr class="bg-indigo-50/30">
                                <td class="py-3 px-4 font-medium text-slate-800 align-top whitespace-nowrap">
                                    正答率収集<br>
                                    <span class="text-[10px] font-bold text-white bg-indigo-500 px-2 py-0.5 rounded-full mt-1 inline-block">UPDATE</span>
                                </td>
                                <td class="py-3 px-4 text-indigo-900">
                                    学習時の解答結果（自己評価や記述式の自己採点、正誤判定）を記録・集計し、以下の正答率を算出・表示する。<br>
                                    ・<strong>1つの問題の正答率</strong>：各問題ごとの累計解答回数に対する正解数の割合を算出し、個々の問題の難易度や苦手度を把握する。<br>
                                    ・<strong>デッキごとの正答率</strong>：デッキに含まれる全問題の集計データから全体の平均正答率を算出し、デッキ単位での理解度を可視化する。
                                </td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>

            <!-- 2.6 デッキの共有 -->
            <div>
                <h3 class="text-lg font-semibold text-slate-800 mb-3" id="2-6-デッキの共有">2.6 デッキの共有</h3>
                <div class="overflow-x-auto">
                    <table class="w-full text-left border-collapse">
                        <thead>
                            <tr class="bg-slate-100 text-slate-700 text-sm">
                                <th class="py-3 px-4 font-semibold rounded-l-lg">機能名</th>
                                <th class="py-3 px-4 font-semibold rounded-r-lg">機能概要</th>
                            </tr>
                        </thead>
                        <tbody class="divide-y divide-slate-100 text-sm text-slate-600">
                            <tr>
                                <td class="py-3 px-4 font-medium text-slate-800 align-top whitespace-nowrap">エクスポート・インポート</td>
                                <td class="py-3 px-4">デッキをファイルに書き出し、別の環境で読み込む。画像など、問題に添付した素材もデッキファイルに含める。</td>
                            </tr>
                            <tr>
                                <td class="py-3 px-4 font-medium text-slate-800 align-top whitespace-nowrap">検証機能</td>
                                <td class="py-3 px-4">読み込み前にファイルの内容を検証し、不正なファイルは取り込まない。</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>

            <!-- 2.7 データ管理 -->
            <div>
                <h3 class="text-lg font-semibold text-slate-800 mb-3" id="2-7-データ管理">2.7 データ管理</h3>
                <div class="overflow-x-auto">
                    <table class="w-full text-left border-collapse">
                        <thead>
                            <tr class="bg-slate-100 text-slate-700 text-sm">
                                <th class="py-3 px-4 font-semibold rounded-l-lg">機能名</th>
                                <th class="py-3 px-4 font-semibold rounded-r-lg">機能概要</th>
                            </tr>
                        </thead>
                        <tbody class="divide-y divide-slate-100 text-sm text-slate-600">
                            <tr class="bg-indigo-50/30">
                                <td class="py-3 px-4 font-medium text-slate-800 align-top whitespace-nowrap">画像・メディアの保存方式</td>
                                <td class="py-3 px-4 text-indigo-900">DBの肥大化と動作の重化を防ぐため、メディアファイルはデータベース内に直接保存（BLOB保存）しない。画像や手書きメモの描画データはアプリ固有のローカルフォルダに保存し、データベースにはそのファイルのパスのみを格納する。</td>
                            </tr>
                            <tr>
                                <td class="py-3 px-4 font-medium text-slate-800 align-top whitespace-nowrap">保存・バックアップ</td>
                                <td class="py-3 px-4">学習データをPC内に保存する。学習データのバックアップをファイルに保存し、復元する。</td>
                            </tr>
                            <tr>
                                <td class="py-3 px-4 font-medium text-slate-800 align-top whitespace-nowrap">データ初期化</td>
                                <td class="py-3 px-4">すべての学習データを削除する前に確認を表示する。</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>

            <!-- 2.8 設定 -->
            <div>
                <h3 class="text-lg font-semibold text-slate-800 mb-3" id="2-8-設定">2.8 設定</h3>
                <div class="overflow-x-auto">
                    <table class="w-full text-left border-collapse">
                        <thead>
                            <tr class="bg-slate-100 text-slate-700 text-sm">
                                <th class="py-3 px-4 font-semibold rounded-l-lg">設定項目</th>
                                <th class="py-3 px-4 font-semibold rounded-r-lg">概要</th>
                            </tr>
                        </thead>
                        <tbody class="divide-y divide-slate-100 text-sm text-slate-600">
                            <tr>
                                <td class="py-3 px-4 font-medium text-slate-800 align-top whitespace-nowrap">復習設定</td>
                                <td class="py-3 px-4">復習間隔を設定する。</td>
                            </tr>
                            <tr>
                                <td class="py-3 px-4 font-medium text-slate-800 align-top whitespace-nowrap">出題順序</td>
                                <td class="py-3 px-4">学習時に表示する問題の順番を設定する（登録順・ランダム）。</td>
                            </tr>
                            <tr>
                                <td class="py-3 px-4 font-medium text-slate-800 align-top whitespace-nowrap">データ操作</td>
                                <td class="py-3 px-4">学習履歴やデータ管理に関する操作を行う。</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>

            <!-- 2.9 ドパガキ用演出・実績機能 -->
            <div>
                <h3 class="text-lg font-semibold text-slate-800 mb-3" id="2-9-ドパガキ用演出・実績機能（学習意欲向上）">2.9 ドパガキ用演出・実績機能（学習意欲向上）</h3>
                <div class="overflow-x-auto">
                    <table class="w-full text-left border-collapse">
                        <thead>
                            <tr class="bg-slate-100 text-slate-700 text-sm">
                                <th class="py-3 px-4 font-semibold rounded-l-lg">演出・機能名</th>
                                <th class="py-3 px-4 font-semibold rounded-r-lg">概要</th>
                            </tr>
                        </thead>
                        <tbody class="divide-y divide-slate-100 text-sm text-slate-600">
                            <tr>
                                <td class="py-3 px-4 font-medium text-slate-800 align-top whitespace-nowrap">ドーパミン促進演出</td>
                                <td class="py-3 px-4">正解時や「簡単」評価時に、紙吹雪やサウンドエフェクトなど、ドーパミンが出るような爽快な演出を行う（学習継続の最重要要素）。</td>
                            </tr>
                            <tr class="bg-indigo-50/30">
                                <td class="py-3 px-4 font-medium text-slate-800 align-top whitespace-nowrap">
                                    実績・バッジ機能<br>
                                    <span class="text-[10px] font-bold text-white bg-indigo-500 px-2 py-0.5 rounded-full mt-1 inline-block">UPDATE</span>
                                </td>
                                <td class="py-3 px-4 text-indigo-900">「7日間連続学習」「累計100問正解」「1つのデッキをマスター」などの条件を満たした際に実績（バッジ）を解除し、豪華なエフェクトと共に通知する。ゲーミフィケーション要素を取り入れ、ユーザーの達成感と学習意欲を持続させる。</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>

        </section>

        <!-- 3. 利用の流れ -->
        <section class="bg-white rounded-xl shadow-sm border border-slate-200 p-6 sm:p-8">
            <h2 class="text-xl font-bold text-slate-900 border-b border-slate-100 pb-3 mb-4 flex items-center gap-2" id="3-利用の流れ">
                <span class="text-indigo-600">3.</span> 利用の流れ
            </h2>
            <ol class="space-y-3 text-slate-700 text-sm list-decimal list-inside leading-relaxed">
                <li class="pl-2"><strong>問題・デッキを作成</strong>：デッキ名や説明を設定し、手動入力によって問題文・解答（記述式の完全一致ワード等）・選択肢・画像を登録する。</li>
                <li class="pl-2"><strong>学習の開始</strong>：学習したいデッキや「未学習の問題」を選択し、学習セッションを開始する。</li>
                <li class="pl-2"><strong>解答とメモの記録</strong>：問題を解く際、テキストやカーソル/手書き描画によって「なぜそう解答したか」の思考プロセスや計算メモを残す。</li>
                <li class="pl-2"><strong>解答確認と自己評価・自己採点</strong>：解答を確認し、必要に応じて「メモ表示ボタン」で過去の思考やミスの傾向を見返しながら、評価（「もう一度・難しい・普通・簡単」）を行う。記述式の場合は単語完全一致判定および「大体あっていればOK」の自己採点を行う。</li>
                <li class="pl-2"><strong>復習・進捗管理</strong>：評価に基づき自動設定された復習スケジュールに従って定期的に復習を行い、学習履歴や正答率を確認する。</li>
                <li class="pl-2"><strong>データの共有・バックアップ</strong>：必要に応じてデッキをファイルに書き出して共有したり、PC内データのバックアップ・復元を行う。</li>
            </ol>
        </section>

        <!-- 4. 画面レイアウト構成案・画面遷移 -->
        <section class="bg-white rounded-xl shadow-sm border border-slate-200 p-6 sm:p-8 space-y-6">
            <h2 class="text-xl font-bold text-slate-900 border-b border-slate-100 pb-3 mb-4 flex items-center gap-2" id="4-画面レイアウト構成案・画面遷移">
                <span class="text-indigo-600">4.</span> 画面レイアウト構成案・画面遷移
            </h2>
            
            <div>
                <h3 class="text-lg font-semibold text-slate-800 mb-3" id="4-1-想定する画面">4.1 想定する画面</h3>
                <div class="overflow-x-auto">
                    <table class="w-full text-left border-collapse">
                        <thead>
                            <tr class="bg-slate-100 text-slate-700 text-sm">
                                <th class="py-3 px-4 font-semibold rounded-l-lg">画面名</th>
                                <th class="py-3 px-4 font-semibold rounded-r-lg">主な内容・操作</th>
                            </tr>
                        </thead>
                        <tbody class="divide-y divide-slate-100 text-sm text-slate-600">
                            <tr>
                                <td class="py-3 px-4 font-medium text-slate-800 align-top whitespace-nowrap">ホーム／デッキ一覧</td>
                                <td class="py-3 px-4">デッキの一覧表示（正答率表示含む）、新規作成、学習開始、共有ファイル読み込みへの導線。</td>
                            </tr>
                            <tr>
                                <td class="py-3 px-4 font-medium text-slate-800 align-top whitespace-nowrap">デッキ詳細・問題一覧</td>
                                <td class="py-3 px-4">選択したデッキ内の問題一覧表示（正答率表示含む）、問題の追加・編集・削除。</td>
                            </tr>
                            <tr>
                                <td class="py-3 px-4 font-medium text-slate-800 align-top whitespace-nowrap">問題作成・編集</td>
                                <td class="py-3 px-4">問題文、解答（記述式の完全一致ワード含む）、画像添付、参考URLの入力・編集。</td>
                            </tr>
                            <tr>
                                <td class="py-3 px-4 font-medium text-slate-800 align-top whitespace-nowrap">学習画面</td>
                                <td class="py-3 px-4">問題の表示、解答オープン、記述式の単語一致＆自己採点機能、<strong>解答メモ欄（テキスト入力／カーソル・手書き描画対応）</strong>、<strong>メモ表示ボタン（過去の思考・ミス確認）</strong>、自己評価、爽快感のある演出。</td>
                            </tr>
                            <tr>
                                <td class="py-3 px-4 font-medium text-slate-800 align-top whitespace-nowrap">復習・進捗画面</td>
                                <td class="py-3 px-4">復習期限到来問題の一覧、学習履歴・実績（バッジ）データおよび正答率統計の確認。</td>
                            </tr>
                            <tr>
                                <td class="py-3 px-4 font-medium text-slate-800 align-top whitespace-nowrap">設定画面</td>
                                <td class="py-3 px-4">復習間隔の変更、出題順序の設定、データバックアップ・初期化などの管理。</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>

            <div>
                <h3 class="text-lg font-semibold text-slate-800 mb-3" id="4-2-画面遷移の案">4.2 画面遷移の案</h3>
                <div class="bg-slate-50 border border-slate-200 rounded-lg p-4 font-mono text-sm text-slate-700">
                    ホーム／デッキ一覧（正答率表示）<br>
                    &nbsp;&nbsp;├── デッキ詳細・問題一覧（正答率表示） ── 問題作成・編集（手動登録）<br>
                    &nbsp;&nbsp;├── 学習画面（記述式・自己採点、解答メモ記録 ＆ メモ表示ボタンによる確認）<br>
                    &nbsp;&nbsp;├── 復習・進捗画面（実績・バッジ確認、統計表示）<br>
                    &nbsp;&nbsp;└── 設定画面
                </div>
            </div>
        </section>

        <!-- 5. 開発方針・追加機能の検討 -->
        <section class="bg-white rounded-xl shadow-sm border border-slate-200 p-6 sm:p-8 space-y-6">
            <h2 class="text-xl font-bold text-slate-900 border-b border-slate-100 pb-3 mb-4 flex items-center gap-2" id="5-開発方針・追加機能の検討">
                <span class="text-indigo-600">5.</span> 開発方針・追加機能の検討
            </h2>
            <div class="space-y-6 text-slate-700 text-sm leading-relaxed">
                <div>
                    <h3 class="font-semibold text-slate-800 mb-2" id="5-1-基本機能と開発の優先順位">5.1 基本機能と開発の優先順位</h3>
                    <ul class="list-disc list-inside space-y-1 pl-2 text-slate-600">
                        <li>デッキ・問題の管理機能（作成、編集、削除、検索）</li>
                        <li>基本的な問題形式（一問一答、選択肢、記述式（完全一致＋自己採点機能））</li>
                        <li>基礎的な学習機能（解答確認・自己評価・進捗保存）および<strong>解答メモ機能（テキスト・手書き描画・メモ表示ボタン）</strong></li>
                        <li>データ管理（ローカルパスによる画像・メモ画像保存方式・バックアップ）と復習スケジュール管理・正答率収集機能</li>
                    </ul>
                </div>
                <div>
                    <h3 class="font-semibold text-slate-800 mb-2" id="5-2-演出および拡張機能の扱い">5.2 演出および拡張機能の扱い</h3>
                    <ul class="list-disc list-inside space-y-1 pl-2 text-slate-600">
                        <li><strong>ドパガキ用演出・実績機能（最重要）</strong>：ユーザーの学習継続意欲を大きく左右するため、基本機能と並行して早期段階から爽快感のある演出や、実績解除（トロフィー・バッジ等）によるゲーミフィケーションの仕組みを実装する。</li>
                        <li><strong>デッキ共有・検証機能</strong>：ユーザー間でのコンテンツ共有を円滑にするため、不正ファイルのブロック機能を含めて堅牢に実装する。</li>
                    </ul>
                </div>
                <div class="bg-indigo-50/50 p-4 rounded-lg border border-indigo-100">
                    <h3 class="font-semibold text-indigo-900 mb-2" id="5-3-今後の拡張・法人向け対応の検討">5.3 今後の拡張・法人向け対応の検討</h3>
                    <ul class="list-disc list-inside space-y-2 text-slate-700">
                        <li><strong>学校法人向け展開の準備：</strong>一般家庭向けで動作と学習効果を検証・成熟させたのち、学校法人向け展開を想定したアーキテクチャへの移行を考慮しておく。</li>
                        <li><strong>将来の機能拡張：</strong>「管理者（教師）によるデッキの一斉配信機能」や「生徒の学習履歴のサーバー集約・ダッシュボード化」などの機能拡張ができるよう、データのエクスポートや外部API連携がしやすいローカルDB構造にしておく。</li>
                    </ul>
                </div>
            </div>
        </section>

    </main>

    <!-- Footer -->
    <footer class="bg-white border-t border-slate-200 py-6 text-center text-xs text-slate-500">
        問題作成・学習アプリ 統合仕様書・要件定義書（改訂版）
    </footer>
    </div>

</body>
</html>
