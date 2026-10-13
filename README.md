# MTU

<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=5.0, user-scalable=yes">
    <title>تطبيق النادي الإعلامي MTU - بنك الأفكار والأرشيف</title>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700;800;900&family=Cinzel:wght@700;900&display=swap" rel="stylesheet">
    
    <style>
        :root {
            --bg-dark: #060913;
            --bg-card: rgba(15, 23, 42, 0.88);
            --bg-card-solid: #0d1527;
            --accent-gold: #f59e0b;
            --gold-bright: #fbbf24;
            --gold-dark: #b45309;
            --text-main: #f8fafc;
            --text-muted: #94a3b8;
            --border: rgba(245, 158, 11, 0.25);
            --input-bg: #080e1a;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Cairo', sans-serif;
            scroll-behavior: smooth;
            -webkit-tap-highlight-color: transparent;
        }

        html, body {
            width: 100%;
            max-width: 100%;
            overflow-x: hidden;
            background-color: var(--bg-dark);
        }

        body {
            background-image: 
                radial-gradient(circle at 50% 10%, rgba(245, 158, 11, 0.12) 0%, transparent 50%),
                radial-gradient(circle at 10% 80%, rgba(180, 83, 9, 0.08) 0%, transparent 40%),
                radial-gradient(circle at 90% 90%, rgba(251, 191, 36, 0.06) 0%, transparent 50%);
            background-attachment: fixed;
            color: var(--text-main);
            line-height: 1.8;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
        }

        .app-header {
            position: sticky;
            top: 0;
            z-index: 1000;
            background: rgba(6, 9, 19, 0.92);
            backdrop-filter: blur(14px);
            -webkit-backdrop-filter: blur(14px);
            border-bottom: 1px solid var(--border);
            padding: 12px 16px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            width: 100%;
        }

        .brand-logo-small {
            display: flex;
            align-items: center;
            gap: 10px;
            cursor: pointer;
            text-decoration: none;
        }

        .brand-logo-small span {
            font-family: 'Cinzel', sans-serif;
            font-size: 1.1rem;
            font-weight: 900;
            color: var(--gold-bright);
            letter-spacing: 1px;
        }

        .quick-nav {
            display: flex;
            gap: 8px;
            flex-wrap: wrap;
        }

        .nav-btn {
            background: rgba(245, 158, 11, 0.08);
            color: var(--text-main);
            border: 1px solid rgba(245, 158, 11, 0.25);
            padding: 8px 16px;
            border-radius: 20px;
            font-size: 0.88rem;
            font-weight: 700;
            cursor: pointer;
            text-decoration: none;
            transition: all 0.3s ease;
            display: inline-flex;
            align-items: center;
            gap: 6px;
            white-space: nowrap;
        }

        .nav-btn:hover, .nav-btn.active {
            background: linear-gradient(135deg, var(--gold-bright), var(--gold-dark));
            color: #060913;
            border-color: var(--gold-bright);
            box-shadow: 0 4px 15px rgba(245, 158, 11, 0.3);
            transform: translateY(-1px);
        }

        .hero-banner {
            text-align: center;
            padding: 35px 15px 25px;
            background: linear-gradient(180deg, rgba(12, 18, 34, 0.95) 0%, rgba(6, 9, 19, 0.6) 100%);
            border-bottom: 1px solid var(--border);
            position: relative;
        }

        .royal-crest-container {
            display: inline-flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            margin-bottom: 12px;
        }

        .royal-crest {
            width: 120px;
            height: 120px;
            position: relative;
            filter: drop-shadow(0 0 20px rgba(245, 158, 11, 0.4));
            transition: transform 0.4s ease;
        }

        .royal-crest:hover {
            transform: scale(1.05);
        }

        .crest-svg {
            width: 100%;
            height: 100%;
        }

        .crest-center-text {
            position: absolute;
            top: 52%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-family: 'Cinzel', serif;
            font-size: 1.5rem;
            font-weight: 900;
            letter-spacing: 2px;
            background: linear-gradient(180deg, #ffffff 10%, #fef08a 50%, #eab308 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .royal-title-tag {
            font-size: 0.7rem;
            font-weight: 800;
            letter-spacing: 2px;
            color: var(--gold-bright);
            margin-top: -4px;
            background: linear-gradient(90deg, transparent, rgba(245, 158, 11, 0.15), transparent);
            padding: 2px 14px;
            border-bottom: 1px solid rgba(245, 158, 11, 0.35);
        }

        h1 {
            font-size: 1.9rem;
            font-weight: 900;
            margin-bottom: 6px;
            background: linear-gradient(180deg, #ffffff 0%, #cbd5e1 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        p.subtitle {
            color: var(--text-muted);
            font-size: 0.95rem;
            max-width: 650px;
            margin: 0 auto;
        }

        .container {
            max-width: 950px;
            margin: 30px auto;
            padding: 0 16px;
            width: 100%;
            flex: 1;
        }

        .spa-page {
            display: none;
            animation: fadeIn 0.4s ease-in-out;
        }

        .spa-page.active-page {
            display: block;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(8px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .card {
            background: var(--bg-card);
            border: 1px solid var(--border);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border-radius: 16px;
            padding: 28px 22px;
            margin-bottom: 30px;
            box-shadow: 0 10px 30px -10px rgba(0, 0, 0, 0.6);
            width: 100%;
        }

        .section-title {
            font-size: 1.35rem;
            font-weight: 800;
            margin-bottom: 22px;
            display: flex;
            align-items: center;
            gap: 10px;
            color: var(--text-main);
        }

        .section-title span.icon {
            background: linear-gradient(135deg, var(--gold-bright), var(--gold-dark));
            color: #000;
            width: 36px;
            height: 36px;
            border-radius: 10px;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            font-size: 1.1rem;
            font-weight: bold;
            box-shadow: 0 4px 12px rgba(245, 158, 11, 0.3);
            flex-shrink: 0;
        }

        .board-hierarchy {
            display: flex;
            flex-direction: column;
            gap: 16px;
            width: 100%;
        }

        .board-tier-1 {
            display: flex;
            justify-content: center;
            width: 100%;
        }

        .board-tier-2 {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
            gap: 16px;
            width: 100%;
        }

        .board-tier-3 {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 14px;
            width: 100%;
        }

        .board-card {
            background: var(--bg-card-solid);
            border: 1px solid var(--border);
            border-radius: 12px;
            padding: 18px 14px;
            text-align: center;
            transition: transform 0.3s ease, border-color 0.3s ease;
        }

        .board-card:hover {
            transform: translateY(-3px);
            border-color: var(--gold-bright);
        }

        .board-card.supervisor {
            background: linear-gradient(145deg, #131d35 0%, #0d1527 100%);
            border: 1px solid rgba(251, 191, 36, 0.4);
            max-width: 350px;
            width: 100%;
            margin: 0 auto;
        }

        .board-card.tech-lead {
            background: linear-gradient(145deg, #0d1527 0%, #1a233a 100%);
            border: 1px solid rgba(245, 158, 11, 0.5);
            box-shadow: 0 0 15px rgba(245, 158, 11, 0.15);
        }

        .board-role {
            font-size: 0.8rem;
            font-weight: 700;
            color: var(--gold-bright);
            margin-bottom: 4px;
        }

        .board-name {
            font-size: 1.1rem;
            font-weight: 800;
            color: #ffffff;
        }

        .action-banner-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
            gap: 20px;
            margin-top: 25px;
        }

        .action-card {
            background: linear-gradient(145deg, rgba(13, 21, 39, 0.9), rgba(19, 29, 53, 0.9));
            border: 1px solid var(--border);
            border-radius: 14px;
            padding: 24px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            gap: 12px;
        }

        .action-card:hover {
            border-color: var(--gold-bright);
            transform: translateY(-4px);
            box-shadow: 0 10px 25px rgba(245, 158, 11, 0.2);
        }

        .action-card .card-icon {
            font-size: 2.2rem;
            background: rgba(245, 158, 11, 0.15);
            width: 60px;
            height: 60px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            border: 1px solid rgba(245, 158, 11, 0.4);
        }

        .action-card h3 {
            color: #ffffff;
            font-size: 1.2rem;
        }

        .action-card p {
            color: var(--text-muted);
            font-size: 0.88rem;
        }

        .form-row {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
            gap: 16px;
        }

        .form-group {
            margin-bottom: 18px;
        }

        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 700;
            color: #e2e8f0;
            font-size: 0.92rem;
        }

        input[type="text"], textarea {
            width: 100%;
            padding: 13px 15px;
            background-color: var(--input-bg);
            border: 1px solid var(--border);
            border-radius: 10px;
            color: var(--text-main);
            font-size: 0.95rem;
            outline: none;
            transition: all 0.3s ease;
        }

        input[type="text"]:focus, textarea:focus {
            border-color: var(--gold-bright);
            box-shadow: 0 0 15px rgba(251, 191, 36, 0.2);
            background-color: #0d1527;
        }

        textarea {
            resize: vertical;
            min-height: 120px;
        }

        button.btn-submit {
            background: linear-gradient(135deg, var(--gold-bright) 0%, var(--gold-dark) 100%);
            color: #060913;
            font-weight: 800;
            font-size: 1rem;
            padding: 14px 24px;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            width: 100%;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(245, 158, 11, 0.3);
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            min-height: 48px;
        }

        button.btn-submit:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 25px rgba(251, 191, 36, 0.45);
        }

        .archive-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            flex-wrap: wrap;
            gap: 12px;
        }

        .archive-counter {
            background: rgba(245, 158, 11, 0.12);
            color: var(--gold-bright);
            padding: 5px 14px;
            border-radius: 20px;
            font-size: 0.85rem;
            font-weight: 700;
            border: 1px solid rgba(245, 158, 11, 0.35);
        }

        .archive-grid {
            display: flex;
            flex-direction: column;
            gap: 20px;
        }

        .idea-card {
            background: var(--bg-card-solid);
            border: 1px solid var(--border);
            border-radius: 14px;
            padding: 22px 18px;
            position: relative;
            overflow: hidden;
            transition: all 0.3s ease;
        }

        .idea-card.featured {
            border: 1px solid rgba(245, 158, 11, 0.45);
            box-shadow: 0 0 30px rgba(245, 158, 11, 0.1);
            background: linear-gradient(145deg, #0d1527 0%, #131d35 100%);
        }

        .idea-card.featured::before {
            content: '';
            position: absolute;
            top: 0;
            right: 0;
            width: 5px;
            height: 100%;
            background: linear-gradient(180deg, var(--gold-bright), var(--gold-dark));
        }

        .badge-featured {
            background: linear-gradient(135deg, var(--gold-bright), var(--gold-dark));
            color: #000;
            font-size: 0.75rem;
            font-weight: 800;
            padding: 3px 10px;
            border-radius: 6px;
            display: inline-block;
            margin-bottom: 12px;
        }

        .idea-header {
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            margin-bottom: 12px;
            gap: 10px;
            flex-wrap: wrap;
        }

        .idea-title {
            font-size: 1.2rem;
            font-weight: 800;
            color: #ffffff;
            line-height: 1.4;
            flex: 1;
            min-width: 200px;
        }

        .idea-author {
            font-size: 0.82rem;
            color: var(--gold-bright);
            background: rgba(245, 158, 11, 0.1);
            padding: 4px 12px;
            border-radius: 20px;
            border: 1px solid rgba(245, 158, 11, 0.3);
            white-space: nowrap;
            font-weight: 700;
        }

        .idea-body {
            color: #cbd5e1;
            font-size: 0.95rem;
            margin-bottom: 16px;
            line-height: 1.7;
        }

        .detail-box {
            background: rgba(6, 9, 19, 0.7);
            border-radius: 10px;
            padding: 14px;
            margin-top: 14px;
            border: 1px solid rgba(245, 158, 11, 0.2);
        }

        .detail-box h4 {
            color: var(--gold-bright);
            font-size: 0.9rem;
            margin-bottom: 10px;
        }

        .tracks-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 10px;
            margin-top: 10px;
        }

        .track-item {
            background: rgba(255, 255, 255, 0.03);
            border-radius: 8px;
            padding: 10px;
            font-size: 0.85rem;
            border-right: 3px solid var(--gold-bright);
        }

        .track-item strong {
            color: #fff;
            display: block;
            margin-bottom: 2px;
        }

        .idea-footer-info {
            display: flex;
            gap: 14px;
            margin-top: 16px;
            padding-top: 14px;
            border-top: 1px solid var(--border);
            font-size: 0.85rem;
            color: var(--text-muted);
            flex-wrap: wrap;
        }

        .idea-footer-info span {
            color: #fff;
            font-weight: 600;
        }

        footer {
            text-align: center;
            color: var(--text-muted);
            font-size: 0.85rem;
            padding: 20px 15px;
            border-top: 1px solid var(--border);
            margin-top: auto;
            background: rgba(6, 9, 19, 0.95);
        }

        @media (max-width: 768px) {
            .app-header {
                flex-direction: column;
                gap: 10px;
                padding: 10px;
            }

            .quick-nav {
                width: 100%;
                justify-content: center;
            }

            .nav-btn {
                padding: 6px 12px;
                font-size: 0.8rem;
                flex: 1 1 auto;
                text-align: center;
                justify-content: center;
            }

            .hero-banner {
                padding: 25px 12px 20px;
            }

            .royal-crest {
                width: 100px;
                height: 100px;
            }

            .crest-center-text {
                font-size: 1.25rem;
            }

            h1 {
                font-size: 1.5rem;
            }

            .board-tier-2, .board-tier-3, .form-row, .tracks-grid, .action-banner-grid {
                grid-template-columns: 1fr;
            }

            .card {
                padding: 18px 14px;
            }
        }
    </style>
</head>
<body>

    <header class="app-header">
        <div class="brand-logo-small" onclick="navigateTo('home')">
            <span>⚜️ MTU MEDIA CLUB</span>
        </div>
        <nav class="quick-nav">
            <button class="nav-btn active" id="btn-home" onclick="navigateTo('home')">🏠 الرئيسية</button>
            <button class="nav-btn" id="btn-board" onclick="navigateTo('home', 'boardSection')">👑 مجلس الإدارة</button>
            <button class="nav-btn" id="btn-submit" onclick="navigateTo('submitPage')">💡 تقديم فكرة</button>
            <button class="nav-btn" id="btn-archive" onclick="navigateTo('archivePage')">📁 أرشيف المشاريع</button>
        </nav>
    </header>

    <!-- الهيدر والترويسة الملكية -->
    <div class="hero-banner">
        <div class="royal-crest-container">
            <div class="royal-crest" title="النادي الإعلامي MTU">
                <svg class="crest-svg" viewBox="0 0 200 200" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <defs>
                        <linearGradient id="goldGrad" x1="0%" y1="0%" x2="100%" y2="100%">
                            <stop offset="0%" stop-color="#fef08a" />
                            <stop offset="30%" stop-color="#f59e0b" />
                            <stop offset="70%" stop-color="#b45309" />
                            <stop offset="100%" stop-color="#78350f" />
                        </linearGradient>
                        <linearGradient id="shieldGrad" x1="0%" y1="0%" x2="0%" y2="100%">
                            <stop offset="0%" stop-color="#0f172a" />
                            <stop offset="100%" stop-color="#020617" />
                        </linearGradient>
                    </defs>
                    <!-- التاج الملكي -->
                    <path d="M75 42 L85 55 L100 35 L115 55 L125 42 L120 65 L80 65 Z" fill="url(#goldGrad)" stroke="#fef08a" stroke-width="1.5" />
                    <circle cx="75" cy="40" r="3" fill="#ffffff" />
                    <circle cx="100" cy="33" r="4" fill="#ffffff" />
                    <circle cx="125" cy="40" r="3" fill="#ffffff" />
                    <!-- الدرع -->
                    <path d="M60 65 H140 V115 Q140 160 100 180 Q60 160 60 115 Z" fill="url(#shieldGrad)" stroke="url(#goldGrad)" stroke-width="4" />
                    <path d="M68 73 H132 V113 Q132 150 100 168 Q68 150 68 113 Z" fill="none" stroke="url(#goldGrad)" stroke-width="1.5" stroke-dasharray="4 2" opacity="0.8" />
                </svg>
                <div class="crest-center-text">MTU</div>
            </div>
            <div class="royal-title-tag">MEDIA CLUB</div>
        </div>
        <h1>بنك الأفكار وأرشيف المشاريع</h1>
        <p class="subtitle">منصة النادي الإعلامي الرسمية لإدارة المبادرات وتوثيق المشاريع</p>
    </div>

    <div class="container">

        <!-- 1️⃣ الصفحة الرئيسية / الشاملة -->
        <main id="home" class="spa-page active-page">
            
            <!-- أزرار العمليات السريعة -->
            <div class="action-banner-grid">
                <div class="action-card" onclick="navigateTo('submitPage')">
                    <div class="card-icon">💡</div>
                    <h3>تقديم فكرة جديدة</h3>
                    <p>أرسل مبادرتك الإعلامية فوراً للرفع بها إلى مجلس النادي والجامعة</p>
                </div>
                <div class="action-card" onclick="navigateTo('archivePage')">
                    <div class="card-icon">📁</div>
                    <h3>استعراض الأرشيف</h3>
                    <p>تصفّح المشاريع والأفكار الموثقة والمعتمدة السابقة</p>
                </div>
            </div>

            <!-- قسم مجلس الإدارة -->
            <section class="card" id="boardSection" style="margin-top: 30px;">
                <h2 class="section-title">
                    <span class="icon">👑</span>
                    مجلس النادي وهيكلة الإدارة
                </h2>
                
                <div class="board-hierarchy">
                    <div class="board-tier-1">
                        <div class="board-card supervisor">
                            <div class="board-role">مشرف النادي</div>
                            <div class="board-name">د. حمزه فرج</div>
                        </div>
                    </div>

                    <div class="board-tier-2">
                        <div class="board-card">
                            <div class="board-role">رئيس النادي</div>
                            <div class="board-name">عبدالرحمن علي الزهراني</div>
                        </div>
                        <div class="board-card">
                            <div class="board-role">نائب الرئيس</div>
                            <div class="board-name">ماجد الشاطري</div>
                        </div>
                    </div>

                    <div class="board-tier-3">
                        <div class="board-card tech-lead">
                            <div class="board-role">مسؤول تقنية المعلومات (IT)</div>
                            <div class="board-name">خالد أحمد الهلال</div>
                        </div>
                        <div class="board-card">
                            <div class="board-role">عضو مجلس الإدارة</div>
                            <div class="board-name">نواف عبد الله المالكي</div>
                        </div>
                        <div class="board-card">
                            <div class="board-role">عضو مجلس الإدارة</div>
                            <div class="board-name">حمد عايض الحارثي</div>
                        </div>
                        <div class="board-card">
                            <div class="board-role">عضو مجلس الإدارة</div>
                            <div class="board-name">عبد الله مزيد السواط</div>
                        </div>
                        <div class="board-card">
                            <div class="board-role">عضو مجلس الإدارة</div>
                            <div class="board-name">عبد الرحمن نجم العتيبي</div>
                        </div>
                    </div>
                </div>
            </section>
        </main>

        <!-- 2️⃣ صفحة تقديم فكرة جديدة (مستقلة داخل الـ SPA) -->
        <section id="submitPage" class="spa-page">
            <div class="card">
                <h2 class="section-title">
                    <span class="icon">💡</span>
                    تقديم فكرة / مشروع جديد
                </h2>
                <p style="color: var(--text-muted); margin-bottom: 20px; font-size: 0.9rem;">قم بتعبئة البيانات التالية بدقة. سيتم توثيق الفكرة وتحويلها تلقائياً لأرشيف المشاريع للرفع بها لمجلس النادي.</p>
                
                <form id="ideaForm">
                    <div class="form-row">
                        <div class="form-group">
                            <label for="authorName">اسم مُقدم الفكرة (الطالب / العضو):</label>
                            <input type="text" id="authorName" placeholder="أدخل اسمك الكريم" required>
                        </div>

                        <div class="form-group">
                            <label for="ideaTitle">عنوان الفكرة أو المبادرة:</label>
                            <input type="text" id="ideaTitle" placeholder="مثال: بودكاست النادي / ورشة سينمائية" required>
                        </div>
                    </div>

                    <div class="form-group">
                        <label for="ideaDescription">تفاصيل وآلية تطبيق الفكرة:</label>
                        <textarea id="ideaDescription" placeholder="اشرح هدف الفكرة، محاور تنفيذها، والنتائج المتوقعة..." required></textarea>
                    </div>

                    <div class="form-row">
                        <div class="form-group">
                            <label for="ideaLocation">الموقع المقترح للتنفيذ:</label>
                            <input type="text" id="ideaLocation" placeholder="مثال: مسرح الجامعة / قاعة المؤتمرات" required>
                        </div>

                        <div class="form-group">
                            <label for="ideaMembers">المسارات والمشاركون المطلوبون:</label>
                            <input type="text" id="ideaMembers" placeholder="مثال: مسار التقديم، التصوير، والإنتاج" required>
                        </div>
                    </div>

                    <button type="submit" class="btn-submit">
                        <span>حفظ الفكرة والتوجيه للأرشيف</span>
                        <span>🚀</span>
                    </button>
                </form>
            </div>
        </section>

        <!-- 3️⃣ صفحة أرشيف المشاريع (مستقلة داخل الـ SPA) -->
        <section id="archivePage" class="spa-page">
            <div class="archive-header">
                <h2 class="section-title" style="margin-bottom: 0;">
                    <span class="icon">📁</span>
                    أرشيف المشاريع والأفكار
                </h2>
                <span class="archive-counter" id="archiveCount">الأفكار التوثيقية: 1</span>
            </div>

            <div class="archive-grid" id="archiveContainer">
                
                <!-- مشروع خالد الهلال الموثق بالكامل -->
                <div class="idea-card featured">
                    <span class="badge-featured">⭐ مشروع مقترح وموثّق بالتفاصيل</span>
                    
                    <div class="idea-header">
                        <div class="idea-title">🎬 ملتقى سينما الجامعة (رؤية سينمائية وإعلامية)</div>
                        <div class="idea-author">المقترح: خالد أحمد الهلال</div>
                    </div>

                    <div class="idea-body">
                        مشروع متكامل يهدف إلى دمج الفن البصري بالمهارات الخطابية والإعلامية لطلاب الجامعة. يُقيم النادي الإعلامي ملتقى سينمائي وثقافي تنظيمي يضم ورش عمل تفاعلية حية تقودها مسارات النادي، يتبعها عرض فيلم قصير هادف، وختام حواري ونقدي تديره كوادر مسار التقديم والخطابة.
                        
                        <div class="detail-box">
                            <h4>🎯 الورش التفاعلية ومسارات المشاركة:</h4>
                            <div class="tracks-grid">
                                <div class="track-item">
                                    <strong>1. مسار التقديم والخطابة</strong>
                                    الافتتاحية والترحيب، إدارة الجلسة الحوارية والنقدية بعد العرض.
                                </div>
                                <div class="track-item">
                                    <strong>2. مسار الإنتاج</strong>
                                    كيفية التخطيط للفيلم القصير، وتحويل الفكرة إلى سيناريو جاهز.
                                </div>
                                <div class="track-item">
                                    <strong>3. مسار التصوير والإضاءة</strong>
                                    تطبيق عملي شرح زوايا الكاميرا وتأثير الإضاءة في المشاعر.
                                </div>
                                <div class="track-item">
                                    <strong>4. مسار التسويق والإعلام</strong>
                                    استراتيجية تسويق الفيلم وصناعة الهوية والبسترات الإعلانية.
                                </div>
                            </div>
                        </div>

                        <div class="detail-box">
                            <h4>⏱️ أجندة الفعالية ومتطلبات الجامعة:</h4>
                            <p style="font-size: 0.88rem; color: #cbd5e1;">
                                • <strong>الأجندة (75 دقيقة):</strong> افتتاح وترحيب (10د) ⬅️ ورش تفاعلية (30د) ⬅️ عرض الفيلم (20د) ⬅️ حوار وختام (15د).<br>
                                • <strong>المتطلبات:</strong> مسرح الجامعة الرئيسي، شاشة عرض Data Show، نظام صوتي وإضاءة مسرحية.
                            </p>
                        </div>
                    </div>

                    <div class="idea-footer-info">
                        <div>📍 موقع التنفيذ: <span>مسرح الجامعة الرئيسي / قاعة المؤتمرات</span></div>
                        <div>👥 المسارات: <span>جميع مسارات النادي الإعلامي</span></div>
                    </div>
                </div>

            </div>
        </section>

    </div>

    <footer>
        النادي الإعلامي (MTU) - جميع الحقوق محفوظة ©️ 2026
    </footer>

    <script>
        // دالة التنقل بين صفحات الـ SPA
        function navigateTo(pageId, scrollToId = null) {
            // إخفاء جميع الصفحات
            const pages = document.querySelectorAll('.spa-page');
            pages.forEach(page => page.classList.remove('active-page'));

            // إزالة التنشيط من أزرار الهيدر
            const navBtns = document.querySelectorAll('.nav-btn');
            navBtns.forEach(btn => btn.classList.remove('active'));

            // إظهار الصفحة المطلوبة
            const targetPage = document.getElementById(pageId);
            if (targetPage) {
                targetPage.classList.add('active-page');
            }

            // تحديث زر الملاحة النشط
            if (pageId === 'home') {
                document.getElementById('btn-home').classList.add('active');
            } else if (pageId === 'submitPage') {
                document.getElementById('btn-submit').classList.add('active');
            } else if (pageId === 'archivePage') {
                document.getElementById('btn-archive').classList.add('active');
            }

            // التمرير لقسم محدد إذا لزم الأمر
            if (scrollToId) {
                setTimeout(() => {
                    const elem = document.getElementById(scrollToId);
                    if (elem) elem.scrollIntoView({ behavior: 'smooth' });
                }, 100);
            } else {
                window.scrollTo({ top: 0, behavior: 'smooth' });
            }
        }

        // عند تحميل الصفحة
        document.addEventListener('DOMContentLoaded', function() {
            loadSavedIdeas();
        });

        // معالجة تقديم نموذج الفكرة
        document.getElementById('ideaForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const author = document.getElementById('authorName').value;
            const title = document.getElementById('ideaTitle').value;
            const desc = document.getElementById('ideaDescription').value;
            const location = document.getElementById('ideaLocation').value;
            const members = document.getElementById('ideaMembers').value;

            const ideaData = {
                id: Date.now(),
                author,
                title,
                desc,
                location,
                members
            };

            saveIdeaToStorage(ideaData);
            renderIdeaCard(ideaData, true);

            this.reset();
            updateCounter();

            // الانتقال التلقائي لصفحة الأرشيف بعد الحفظ
            navigateTo('archivePage');
        });

        function renderIdeaCard(idea, prepend = false) {
            const archive = document.getElementById('archiveContainer');
            
            const card = document.createElement('div');
            card.className = 'idea-card';
            card.innerHTML = `
                <div class="idea-header">
                    <div class="idea-title">💡 ${escapeHtml(idea.title)}</div>
                    <div class="idea-author">المقترح: ${escapeHtml(idea.author)}</div>
                </div>
                <div class="idea-body">
                    ${escapeHtml(idea.desc)}
                </div>
                <div class="idea-footer-info">
                    <div>📍 الموقع: <span>${escapeHtml(idea.location)}</span></div>
                    <div>👥 المسارات: <span>${escapeHtml(idea.members)}</span></div>
                </div>
            `;

            if (prepend) {
                archive.insertBefore(card, archive.children[1] || null);
            } else {
                archive.appendChild(card);
            }
        }

        function saveIdeaToStorage(idea) {
            let ideas = JSON.parse(localStorage.getItem('mtu_ideas') || '[]');
            ideas.unshift(idea);
            localStorage.setItem('mtu_ideas', JSON.stringify(ideas));
        }

        function loadSavedIdeas() {
            let ideas = JSON.parse(localStorage.getItem('mtu_ideas') || '[]');
            ideas.forEach(idea => {
                renderIdeaCard(idea, false);
            });
            updateCounter();
        }

        function updateCounter() {
            const cards = document.querySelectorAll('.idea-card');
            document.getElementById('archiveCount').textContent = `الأفكار التوثيقية: ${cards.length}`;
        }

        function escapeHtml(text) {
            if (!text) return '';
            return text
                .replace(/&/g, "&amp;")
                .replace(/</g, "&lt;")
                .replace(/>/g, "&gt;")
                .replace(/"/g, "&quot;")
                .replace(/'/g, "&#039;");
        }
    </script>
</body>
</html>
