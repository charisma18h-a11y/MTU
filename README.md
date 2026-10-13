# MTU
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>بنك الأفكار وأرشيف المشاريع - ميديا كلب MTU</title>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700;800;900&family=Cinzel:wght@700;900&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg-dark: #0a0a0c;
            --bg-deep: #050507;
            --bg-card: rgba(18, 18, 24, 0.82);
            --bg-card-solid: #121218;
            --accent-primary: #3b82f6;
            --accent-glow: #60a5fa;
            --accent-gold: #f59e0b;
            --text-main: #f8fafc;
            --text-muted: #94a3b8;
            --border: rgba(255, 255, 255, 0.12);
            --input-bg: #0c0c10;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Cairo', sans-serif;
            -webkit-tap-highlight-color: transparent;
        }

        body {
            background-color: var(--bg-dark);
            color: var(--text-main);
            line-height: 1.7;
            padding-bottom: 40px;
            min-height: 100vh;
            overflow-x: hidden;
            width: 100%;
            position: relative;
        }

        /* خلفية فيديو يوتيوب الثابتة (أوضح وبدون خضرة) */
        .bg-video-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            z-index: -99;
            overflow: hidden;
            pointer-events: none;
            background: #000;
        }

        .bg-youtube-video {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%) scale(1.35);
            width: 100vw;
            height: 56.25vw;
            min-height: 100vh;
            min-width: 177.77vh;
            pointer-events: none;
            /* تم زيادة الوضوح وإلغاء التعتيم الشديد */
            filter: brightness(0.65) contrast(1.15) saturate(1.1);
        }

        .bg-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            background: rgba(10, 10, 12, 0.75); /* طبقة تعتيم خفيفة جداً لتظهر تفاصيل الفيديو بوضوح */
            z-index: -98;
            pointer-events: none;
        }

        /* شاشة الترحيب الحديثة */
        #welcomeScreen {
            position: fixed;
            inset: 0;
            z-index: 99999;
            background: var(--bg-deep);
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 20px;
            text-align: center;
            transition: opacity 0.5s ease, visibility 0.5s ease;
        }

        .quick-nav {
            position: sticky;
            top: 0;
            z-index: 1000;
            background: rgba(15, 15, 20, 0.85);
            backdrop-filter: blur(12px);
            border-bottom: 1px solid var(--border);
            padding: 10px 12px;
            display: flex;
            justify-content: center;
            gap: 8px;
            width: 100%;
        }

        .nav-btn {
            background: rgba(255, 255, 255, 0.05);
            color: var(--text-main);
            border: 1px solid var(--border);
            padding: 8px 14px;
            border-radius: 20px;
            font-size: 0.82rem;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.3s ease;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: 6px;
            flex: 1;
            max-width: 160px;
            text-align: center;
            white-space: nowrap;
        }

        .nav-btn:hover, .nav-btn.active {
            background: var(--accent-primary);
            color: #ffffff;
            border-color: var(--accent-glow);
            transform: translateY(-2px);
            box-shadow: 0 4px 15px rgba(59, 130, 246, 0.4);
        }

        header {
            position: relative;
            text-align: center;
            padding: 30px 15px 20px;
            background: rgba(18, 18, 24, 0.65);
            border-bottom: 1px solid var(--border);
            backdrop-filter: blur(12px);
            overflow: hidden;
        }

        /* تصميم الشعار الجديد (عدسة وشاشة إعلامية) */
        .media-crest-container {
            display: inline-flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            margin-bottom: 10px;
            position: relative;
        }

        .media-crest {
            width: 100px;
            height: 100px;
            position: relative;
            display: flex;
            align-items: center;
            justify-content: center;
            filter: drop-shadow(0 0 15px rgba(59, 130, 246, 0.4));
        }

        .crest-svg {
            width: 100%;
            height: 100%;
        }

        .crest-center-text {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-family: 'Cinzel', 'Cairo', serif;
            font-size: 1.15rem;
            font-weight: 900;
            letter-spacing: 2px;
            background: linear-gradient(180deg, #ffffff 20%, #60a5fa 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .media-title-tag {
            font-size: 0.68rem;
            font-weight: 800;
            letter-spacing: 3px;
            color: var(--accent-glow);
            text-transform: uppercase;
            margin-top: 4px;
            background: rgba(59, 130, 246, 0.1);
            padding: 2px 14px;
            border-radius: 12px;
            border: 1px solid rgba(59, 130, 246, 0.3);
        }

        .site-badge {
            background: rgba(59, 130, 246, 0.15);
            color: var(--accent-glow);
            padding: 5px 18px;
            border-radius: 30px;
            font-size: 0.8rem;
            font-weight: 700;
            display: inline-block;
            margin-bottom: 8px;
            border: 1px solid rgba(59, 130, 246, 0.3);
        }

        h1 {
            font-size: 1.6rem;
            font-weight: 900;
            margin-bottom: 6px;
            background: linear-gradient(180deg, #ffffff 0%, #cbd5e1 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        p.subtitle {
            color: var(--text-muted);
            font-size: 0.88rem;
            max-width: 680px;
            margin: 0 auto;
            padding: 0 10px;
        }

        .container {
            max-width: 950px;
            margin: 20px auto;
            padding: 0 12px;
            width: 100%;
        }

        .page-section {
            display: none;
        }

        .page-section.active {
            display: block;
            animation: fadeIn 0.3s ease-in-out;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(8px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .card {
            background: var(--bg-card);
            border: 1px solid var(--border);
            backdrop-filter: blur(12px);
            border-radius: 14px;
            padding: 18px 14px;
            margin-bottom: 20px;
            box-shadow: 0 10px 30px -10px rgba(0, 0, 0, 0.8);
        }

        .section-title {
            font-size: 1.15rem;
            font-weight: 800;
            margin-bottom: 16px;
            display: flex;
            align-items: center;
            gap: 10px;
            color: var(--text-main);
        }

        .section-title span.icon {
            background: var(--accent-primary);
            color: #ffffff;
            width: 30px;
            height: 30px;
            border-radius: 8px;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            font-size: 1rem;
            box-shadow: 0 4px 12px rgba(59, 130, 246, 0.3);
            flex-shrink: 0;
        }

        .board-hierarchy {
            display: flex;
            flex-direction: column;
            gap: 12px;
        }

        .board-tier-1 { display: flex; justify-content: center; }
        .board-tier-2 { display: grid; grid-template-columns: repeat(auto-fit, minmax(140px, 1fr)); gap: 10px; }
        .board-tier-3 { display: grid; grid-template-columns: repeat(auto-fit, minmax(130px, 1fr)); gap: 10px; }

        .board-card {
            background: var(--bg-card-solid);
            border: 1px solid var(--border);
            border-radius: 10px;
            padding: 12px 10px;
            text-align: center;
            transition: transform 0.2s ease;
        }

        .board-card.supervisor {
            background: linear-gradient(145deg, #1e1b4b 0%, #0f172a 100%);
            border: 1px solid rgba(96, 165, 250, 0.4);
            width: 100%;
            max-width: 280px;
            margin: 0 auto;
        }

        .board-card.tech-lead {
            background: linear-gradient(145deg, #0f172a 0%, #1e293b 100%);
            border: 1px solid rgba(59, 130, 246, 0.5);
        }

        .board-role {
            font-size: 0.72rem;
            font-weight: 700;
            color: var(--accent-glow);
            margin-bottom: 2px;
            text-transform: uppercase;
        }

        .board-name {
            font-size: 0.92rem;
            font-weight: 800;
            color: #ffffff;
        }

        .form-row {
            display: grid;
            grid-template-columns: 1fr;
            gap: 12px;
        }

        @media (min-width: 600px) {
            .form-row {
                grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
            }
        }

        .form-group {
            margin-bottom: 14px;
        }

        label {
            display: block;
            margin-bottom: 5px;
            font-weight: 700;
            color: #cbd5e1;
            font-size: 0.85rem;
        }

        input[type="text"], input[type="url"], textarea {
            width: 100%;
            padding: 10px 12px;
            background-color: var(--input-bg);
            border: 1px solid var(--border);
            border-radius: 8px;
            color: var(--text-main);
            font-size: 0.9rem;
            outline: none;
            transition: all 0.3s ease;
        }

        input[type="text"]:focus, input[type="url"]:focus, textarea:focus {
            border-color: var(--accent-primary);
            box-shadow: 0 0 10px rgba(59, 130, 246, 0.25);
            background-color: #121218;
        }

        textarea {
            resize: vertical;
            min-height: 90px;
        }

        button.btn-submit {
            background: var(--accent-primary);
            color: #ffffff;
            font-weight: 800;
            font-size: 0.95rem;
            padding: 12px 20px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            width: 100%;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(59, 130, 246, 0.35);
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }

        button.btn-submit:active {
            transform: scale(0.98);
        }

        .archive-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
            flex-wrap: wrap;
            gap: 10px;
        }

        .archive-counter {
            background: rgba(59, 130, 246, 0.15);
            color: var(--accent-glow);
            padding: 4px 12px;
            border-radius: 16px;
            font-size: 0.78rem;
            font-weight: 700;
            border: 1px solid rgba(59, 130, 246, 0.3);
        }

        .archive-grid {
            display: flex;
            flex-direction: column;
            gap: 15px;
        }

        .idea-card {
            background: var(--bg-card-solid);
            border: 1px solid var(--border);
            border-radius: 12px;
            padding: 15px;
            position: relative;
            overflow: hidden;
        }

        .idea-card.featured {
            border: 1px solid rgba(59, 130, 246, 0.4);
            background: linear-gradient(145deg, #121218 0%, #172033 100%);
        }

        .idea-card.featured::before {
            content: '';
            position: absolute;
            top: 0;
            right: 0;
            width: 4px;
            height: 100%;
            background: var(--accent-primary);
        }

        .badge-featured {
            background: var(--accent-primary);
            color: #ffffff;
            font-size: 0.68rem;
            font-weight: 800;
            padding: 2px 8px;
            border-radius: 4px;
            display: inline-block;
            margin-bottom: 8px;
        }

        .idea-header {
            display: flex;
            flex-direction: column;
            gap: 6px;
            margin-bottom: 8px;
        }

        @media (min-width: 500px) {
            .idea-header {
                flex-direction: row;
                justify-content: space-between;
                align-items: flex-start;
            }
        }

        .idea-title {
            font-size: 1.05rem;
            font-weight: 800;
            color: #ffffff;
            line-height: 1.4;
        }

        .idea-author {
            font-size: 0.75rem;
            color: var(--accent-glow);
            background: rgba(59, 130, 246, 0.12);
            padding: 2px 10px;
            border-radius: 15px;
            border: 1px solid rgba(59, 130, 246, 0.3);
            font-weight: 700;
            align-self: flex-start;
        }

        .idea-body {
            color: #cbd5e1;
            font-size: 0.88rem;
            margin-bottom: 12px;
        }

        .media-container {
            margin-top: 12px;
            display: flex;
            flex-direction: column;
            gap: 10px;
        }

        .media-image {
            width: 100%;
            max-height: 250px;
            object-fit: cover;
            border-radius: 8px;
            border: 1px solid var(--border);
        }

        .video-wrapper {
            position: relative;
            padding-bottom: 56.25%;
            height: 0;
            overflow: hidden;
            border-radius: 8px;
            border: 1px solid var(--border);
        }

        .video-wrapper iframe {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            border: none;
        }

        .detail-box {
            background: rgba(0, 0, 0, 0.4);
            border-radius: 8px;
            padding: 10px;
            margin-top: 10px;
            border: 1px solid rgba(255, 255, 255, 0.08);
        }

        .detail-box h4 {
            color: var(--accent-glow);
            font-size: 0.82rem;
            margin-bottom: 6px;
        }

        .tracks-grid {
            display: grid;
            grid-template-columns: 1fr;
            gap: 6px;
            margin-top: 6px;
        }

        @media (min-width: 480px) {
            .tracks-grid {
                grid-template-columns: repeat(2, 1fr);
            }
        }

        .track-item {
            background: rgba(255, 255, 255, 0.03);
            border-radius: 6px;
            padding: 6px 8px;
            font-size: 0.78rem;
            border-right: 3px solid var(--accent-primary);
        }

        .track-item strong { color: #fff; display: block; margin-bottom: 1px; }

        .idea-footer-info {
            display: flex;
            flex-direction: column;
            gap: 6px;
            margin-top: 12px;
            padding-top: 10px;
            border-top: 1px solid var(--border);
            font-size: 0.8rem;
            color: var(--text-muted);
        }

        @media (min-width: 500px) {
            .idea-footer-info {
                flex-direction: row;
                gap: 15px;
            }
        }

        .idea-footer-info span { color: #fff; font-weight: 600; }

        footer {
            text-align: center;
            color: var(--text-muted);
            font-size: 0.8rem;
            padding-top: 20px;
            border-top: 1px solid var(--border);
            margin-top: 25px;
        }
    </style>
</head>
<body>

    <!-- خلفية فيديو يوتيوب الجديدة المحدثة (أوضح وبدون خضرة) -->
    <div class="bg-video-container">
        <iframe class="bg-youtube-video" src="https://www.youtube.com/embed/_TkXgy18J_g?autoplay=1&mute=1&loop=1&playlist=_TkXgy18J_g&controls=0&showinfo=0&autohide=1&modestbranding=1" frameborder="0" allow="autoplay; encrypted-media"></iframe>
    </div>
    <div class="bg-overlay"></div>

    <!-- شاشة الترحيب -->
    <div id="welcomeScreen">
        <div class="media-crest-container">
            <div class="media-crest" title="ميديا كلب MTU">
                <svg class="crest-svg" viewBox="0 0 200 200" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <defs>
                        <linearGradient id="blueGradW" x1="0%" y1="0%" x2="100%" y2="100%">
                            <stop offset="0%" stop-color="#60a5fa" />
                            <stop offset="100%" stop-color="#1e40af" />
                        </linearGradient>
                    </defs>
                    <!-- تصميم عدسة كاميرا وشاشة إعلامية حديثة -->
                    <circle cx="100" cy="100" r="70" fill="#0f172a" stroke="url(#blueGradW)" stroke-width="6"/>
                    <circle cx="100" cy="100" r="45" fill="none" stroke="url(#blueGradW)" stroke-width="2" stroke-dasharray="6 4"/>
                    <circle cx="100" cy="100" r="22" fill="url(#blueGradW)" opacity="0.8"/>
                    <!-- زوايا الإطار الإعلامي -->
                    <path d="M50 60 H70 M50 60 V80" stroke="#fff" stroke-width="4" stroke-linecap="round"/>
                    <path d="M150 60 H130 M150 60 V80" stroke="#fff" stroke-width="4" stroke-linecap="round"/>
                    <path d="M50 140 H70 M50 140 V120" stroke="#fff" stroke-width="4" stroke-linecap="round"/>
                    <path d="M150 140 H130 M150 140 V120" stroke="#fff" stroke-width="4" stroke-linecap="round"/>
                </svg>
                <div class="crest-center-text">MTU</div>
            </div>
            <div class="media-title-tag">MEDIA CLUB</div>
        </div>

        <span class="site-badge" style="margin-top: 10px;">🎥 إبداع بصري وإنتاج إعلامي</span>
        <h1 style="font-size: 1.5rem; margin-top: 5px;">أهلاً بكم في بنك الأفكار والمشاريع</h1>
        <p class="subtitle" style="margin-bottom: 25px;">بوابة الإبداع والريادة لطلاب جامعة الطائف بروح الإنتاج الإعلامي الحديث</p>
        
        <button onclick="enterSite()" class="btn-submit" style="max-width: 220px; font-size: 1rem;">
            <span>دخول المنصة</span>
            <span>✨</span>
        </button>
    </div>

    <nav class="quick-nav">
        <button class="nav-btn active" onclick="switchPage('homePage', this)">🏛️ المجلس</button>
        <button class="nav-btn" onclick="switchPage('formPage', this)">💡 تقديم فكرة</button>
        <button class="nav-btn" onclick="switchPage('archivePage', this)">📁 الأرشيف</button>
    </nav>

    <header>
        <div class="media-crest-container">
            <div class="media-crest" title="ميديا كلب MTU">
                <svg class="crest-svg" viewBox="0 0 200 200" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <defs>
                        <linearGradient id="blueGrad" x1="0%" y1="0%" x2="100%" y2="100%">
                            <stop offset="0%" stop-color="#60a5fa" />
                            <stop offset="100%" stop-color="#1e40af" />
                        </linearGradient>
                    </defs>
                    <circle cx="100" cy="100" r="70" fill="#0f172a" stroke="url(#blueGrad)" stroke-width="6"/>
                    <circle cx="100" cy="100" r="45" fill="none" stroke="url(#blueGrad)" stroke-width="2" stroke-dasharray="6 4"/>
                    <circle cx="100" cy="100" r="22" fill="url(#blueGrad)" opacity="0.8"/>
                    <path d="M50 60 H70 M50 60 V80" stroke="#fff" stroke-width="4" stroke-linecap="round"/>
                    <path d="M150 60 H130 M150 60 V80" stroke="#fff" stroke-width="4" stroke-linecap="round"/>
                    <path d="M50 140 H70 M50 140 V120" stroke="#fff" stroke-width="4" stroke-linecap="round"/>
                    <path d="M150 140 H130 M150 140 V120" stroke="#fff" stroke-width="4" stroke-linecap="round"/>
                </svg>
                <div class="crest-center-text">MTU</div>
            </div>
            <div class="media-title-tag">MEDIA CLUB</div>
        </div>

        <br>
        <span class="site-badge">🎬 منصة النادي الإعلامي</span>
        <h1>بنك الأفكار والأرشيف</h1>
        <p class="subtitle">المساحة السحابية لاستقبال وتوثيق مبادرات طلاب الجامعة</p>
    </header>

    <div class="container">

        <section id="homePage" class="page-section active">
            <div class="card">
                <h2 class="section-title">
                    <span class="icon">👥</span>
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

                    <div class="board-tier-3">
                        <div class="board-card tech-lead" style="grid-column: 1 / -1; max-width: 320px; margin: 0 auto; width: 100%;">
                            <div class="board-role">مسؤول تقنية المعلومات (IT)</div>
                            <div class="board-name">خالد أحمد الهلال</div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <section id="formPage" class="page-section">
            <div class="card">
                <h2 class="section-title">
                    <span class="icon">💡</span>
                    تقديم فكرة / مشروع جديد
                </h2>
                
                <form id="ideaForm">
                    <div class="form-row">
                        <div class="form-group">
                            <label for="authorName">اسم مُقدم الفكرة:</label>
                            <input type="text" id="authorName" placeholder="أدخل اسمك الكريم" required>
                        </div>

                        <div class="form-group">
                            <label for="ideaTitle">عنوان الفكرة أو المبادرة:</label>
                            <input type="text" id="ideaTitle" placeholder="مثال: بودكاست النادي" required>
                        </div>
                    </div>

                    <div class="form-group">
                        <label for="ideaDescription">تفاصيل وآلية تطبيق الفكرة:</label>
                        <textarea id="ideaDescription" placeholder="اشرح هدف الفكرة وحجم التنفيذ..." required></textarea>
                    </div>

                    <div class="form-row">
                        <div class="form-group">
                            <label for="ideaLocation">الموقع المقترح للتنفيذ:</label>
                            <input type="text" id="ideaLocation" placeholder="مثال: مسرح الجامعة" required>
                        </div>

                        <div class="form-group">
                            <label for="ideaMembers">المسارات والمشاركون:</label>
                            <input type="text" id="ideaMembers" placeholder="مثال: التقديم والتصوير" required>
                        </div>
                    </div>

                    <div class="form-row">
                        <div class="form-group">
                            <label for="imageUrl">رابط صورة/تصميم (اختياري):</label>
                            <input type="url" id="imageUrl" placeholder="https://example.com/image.jpg">
                        </div>

                        <div class="form-group">
                            <label for="videoUrl">رابط فيديو يوتيوب (اختياري):</label>
                            <input type="url" id="videoUrl" placeholder="https://youtube.com/watch?v=...">
                        </div>
                    </div>

                    <button type="submit" class="btn-submit" id="submitBtn">
                        <span>حفظ الفكرة في السحابة</span>
                        <span>🚀</span>
                    </button>
                </form>
            </div>
        </section>

        <section id="archivePage" class="page-section">
            <div class="archive-header">
                <h2 class="section-title" style="margin-bottom: 0;">
                    <span class="icon">📁</span>
                    الأرشيف
                </h2>
                <span class="archive-counter" id="archiveCount">جاري التحميل...</span>
            </div>

            <div class="idea-card featured" style="margin-bottom: 15px;">
                <span class="badge-featured">⭐ مشروع مقترح وموثّق</span>
                <div class="idea-header">
                    <div class="idea-title">🎬 ملتقى سينما الجامعة</div>
                    <div class="idea-author">المقترح: خالد أحمد الهلال</div>
                </div>
                <div class="idea-body">
                    مشروع متكامل يهدف إلى دمج الفن البصري بالمهارات الخطابية والإعلامية لطلاب الجامعة.
                    <div class="detail-box">
                        <h4>🎯 المسارات والورش:</h4>
                        <div class="tracks-grid">
                            <div class="track-item"><strong>1. مسار التقديم</strong>إدارة الجلسات.</div>
                            <div class="track-item"><strong>2. مسار الإنتاج</strong>كتابة السيناريو.</div>
                            <div class="track-item"><strong>3. مسار التصوير</strong>التصوير والإنتاج.</div>
                            <div class="track-item"><strong>4. مسار التسويق</strong>الهوية والإعلام.</div>
                        </div>
                    </div>
                </div>
                <div class="idea-footer-info">
                    <div>📍 الموقع: <span>مسرح الجامعة الرئيسي</span></div>
                    <div>👥 المسارات: <span>جميع المسارات</span></div>
                </div>
            </div>

            <div class="archive-grid" id="archiveContainer">
            </div>
        </section>

        <footer>
            النادي الإعلامي (MTU) ©️ 2026 | ميديا كلب
        </footer>

    </div>

    <script>
        const SCRIPT_URL = "https://script.google.com/macros/s/AKfycbwN5Ty-lRiwKN9lVy9F94l8C9mxgSK-uDkVT9JStVT0eHnWtETg6CFJRpmw5lObZwV6/exec";

        window.enterSite = function() {
            const welcome = document.getElementById('welcomeScreen');
            welcome.style.opacity = '0';
            welcome.style.visibility = 'hidden';
            setTimeout(() => {
                welcome.style.display = 'none';
            }, 500);
        }

        window.switchPage = function(pageId, btnElement) {
            document.querySelectorAll('.page-section').forEach(sec => sec.classList.remove('active'));
            document.querySelectorAll('.nav-btn').forEach(btn => btn.classList.remove('active'));
            
            document.getElementById(pageId).classList.add('active');
            btnElement.classList.add('active');
            window.scrollTo({ top: 0, behavior: 'smooth' });

            if(pageId === 'archivePage') {
                loadSheetIdeas();
            }
        };

        function getYouTubeEmbedUrl(url) {
            if (!url) return '';
            let videoId = '';
            const regExp = /^.*(youtu.be\/|v\/|u\/\w\/|embed\/|watch\?v=|\&v=)([^#\&\?]*).*/;
            const match = url.match(regExp);
            if (match && match[2].length === 11) {
                videoId = match[2];
                return `https://www.youtube.com/embed/${videoId}`;
            }
            return '';
        }

        document.getElementById('ideaForm').addEventListener('submit', async function(e) {
            e.preventDefault();
            
            const submitBtn = document.getElementById('submitBtn');
            submitBtn.disabled = true;
            submitBtn.innerHTML = '<span>جاري الحفظ...</span> ⏳';

            const data = {
                author: document.getElementById('authorName').value.trim(),
                title: document.getElementById('ideaTitle').value.trim(),
                desc: document.getElementById('ideaDescription').value.trim(),
                location: document.getElementById('ideaLocation').value.trim(),
                members: document.getElementById('ideaMembers').value.trim(),
                imageUrl: document.getElementById('imageUrl').value.trim(),
                videoUrl: document.getElementById('videoUrl').value.trim()
            };

            try {
                await fetch(SCRIPT_URL, {
                    method: 'POST',
                    mode: 'no-cors',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(data)
                });

                alert('✅ تم حفظ الفكرة بنجاح!');
                this.reset();
                
                const archiveBtn = document.querySelectorAll('.nav-btn')[2];
                switchPage('archivePage', archiveBtn);
            } catch (error) {
                console.error("Error: ", error);
                alert('❌ تعذر الحفظ: ' + error.message);
            } finally {
                submitBtn.disabled = false;
                submitBtn.innerHTML = '<span>حفظ الفكرة في السحابة</span> <span>🚀</span>';
            }
        });

        async function loadSheetIdeas() {
            const container = document.getElementById('archiveContainer');
            const counter = document.getElementById('archiveCount');

            try {
                container.innerHTML = '<div style="text-align: center; color: var(--text-muted); padding: 20px;">جاري تحميل الأرشيف...</div>';
                const response = await fetch(SCRIPT_URL);
                const ideas = await response.json();

                counter.textContent = `إجمالي المشاركات: ${ideas.length}`;
                container.innerHTML = '';

                if (ideas.length === 0) {
                    container.innerHTML = '<div style="text-align: center; color: var(--text-muted); padding: 20px;">لا توجد أفكار مسجلة حتى الآن.</div>';
                    return;
                }

                ideas.reverse().forEach((idea, index) => {
                    const embedUrl = getYouTubeEmbedUrl(idea.videoUrl || idea.video);
                    const card = document.createElement('div');
                    card.className = 'idea-card';
                    
                    card.innerHTML = `
                        <div class="idea-header">
                            <div class="idea-title">${idea.title || 'بدون عنوان'}</div>
                            <div class="idea-author">المقترح: ${idea.author || 'مجهول'}</div>
                        </div>
                        <div class="idea-body">
                            ${idea.desc || idea.description || ''}
                        </div>
                        ${idea.imageUrl || idea.image ? `
                            <div class="media-container">
                                <img src="${idea.imageUrl || idea.image}" class="media-image" alt="صورة المبادرة" onerror="this.style.display='none'">
                            </div>
                        ` : ''}
                        ${embedUrl ? `
                            <div class="media-container">
                                <div class="video-wrapper">
                                    <iframe src="${embedUrl}" allowfullscreen></iframe>
                                </div>
                            </div>
                        ` : ''}
                        <div class="idea-footer-info">
                            <div>📍 الموقع: <span>${idea.location || 'غير محدد'}</span></div>
                            <div>👥 المسارات: <span>${idea.members || 'غير محدد'}</span></div>
                        </div>
                    `;
                    container.appendChild(card);
                });

            } catch (error) {
                console.error("Error loading archive:", error);
                counter.textContent = 'خطأ في التحميل';
                container.innerHTML = '<div style="text-align: center; color: #ef4444; padding: 20px;">تعذر استرجاع الأرشيف من السحابة.</div>';
            }
        }
    </script>
</body>
</html>
