# MTU
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>بنك الأفكار وأرشيف المشاريع - النادي الإعلامي MTU</title>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700;800;900&family=Cinzel:wght@700;900&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg-dark: #060913;
            --bg-card: rgba(15, 23, 42, 0.85);
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
            -webkit-tap-highlight-color: transparent;
        }

        body {
            background-color: var(--bg-dark);
            background-image: 
                radial-gradient(circle at 50% 10%, rgba(245, 158, 11, 0.12) 0%, transparent 50%),
                radial-gradient(circle at 10% 80%, rgba(180, 83, 9, 0.08) 0%, transparent 40%),
                radial-gradient(circle at 90% 90%, rgba(251, 191, 36, 0.06) 0%, transparent 50%);
            background-attachment: fixed;
            color: var(--text-main);
            line-height: 1.7;
            padding-bottom: 40px;
            min-height: 100vh;
            overflow-x: hidden;
            width: 100%;
        }

        .quick-nav {
            position: sticky;
            top: 0;
            z-index: 1000;
            background: rgba(6, 9, 19, 0.95);
            backdrop-filter: blur(12px);
            border-bottom: 1px solid var(--border);
            padding: 10px 12px;
            display: flex;
            justify-content: center;
            gap: 8px;
            width: 100%;
        }

        .nav-btn {
            background: rgba(245, 158, 11, 0.1);
            color: var(--gold-bright);
            border: 1px solid rgba(245, 158, 11, 0.35);
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
            background: linear-gradient(135deg, var(--gold-bright), var(--gold-dark));
            color: #000;
            transform: translateY(-2px);
            box-shadow: 0 4px 15px rgba(245, 158, 11, 0.3);
        }

        header {
            position: relative;
            text-align: center;
            padding: 30px 15px 20px;
            background: linear-gradient(180deg, rgba(12, 18, 34, 0.95) 0%, rgba(6, 9, 19, 0.6) 100%);
            border-bottom: 1px solid var(--border);
            backdrop-filter: blur(12px);
            overflow: hidden;
        }

        .royal-crest-container {
            display: inline-flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            margin-bottom: 10px;
            position: relative;
        }

        .royal-crest {
            width: 100px;
            height: 100px;
            position: relative;
            display: flex;
            align-items: center;
            justify-content: center;
            filter: drop-shadow(0 0 18px rgba(245, 158, 11, 0.4));
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
            font-family: 'Cinzel', 'Cairo', serif;
            font-size: 1.3rem;
            font-weight: 900;
            letter-spacing: 2px;
            background: linear-gradient(180deg, #ffffff 10%, #fef08a 50%, #eab308 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .royal-title-tag {
            font-size: 0.65rem;
            font-weight: 800;
            letter-spacing: 2px;
            color: var(--gold-bright);
            text-transform: uppercase;
            margin-top: -4px;
            background: linear-gradient(90deg, transparent, rgba(245, 158, 11, 0.15), transparent);
            padding: 2px 15px;
            border-bottom: 1px solid rgba(245, 158, 11, 0.35);
        }

        .site-badge {
            background: rgba(245, 158, 11, 0.1);
            color: var(--gold-bright);
            padding: 4px 16px;
            border-radius: 30px;
            font-size: 0.78rem;
            font-weight: 700;
            display: inline-block;
            margin-bottom: 8px;
            border: 1px solid rgba(245, 158, 11, 0.35);
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
            box-shadow: 0 10px 30px -10px rgba(0, 0, 0, 0.6);
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
            background: linear-gradient(135deg, var(--gold-bright), var(--gold-dark));
            color: #000;
            width: 30px;
            height: 30px;
            border-radius: 8px;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            font-size: 1rem;
            box-shadow: 0 4px 12px rgba(245, 158, 11, 0.3);
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
            background: linear-gradient(145deg, #131d35 0%, #0d1527 100%);
            border: 1px solid rgba(251, 191, 36, 0.4);
            width: 100%;
            max-width: 280px;
            margin: 0 auto;
        }

        .board-card.tech-lead {
            background: linear-gradient(145deg, #0d1527 0%, #1a233a 100%);
            border: 1px solid rgba(245, 158, 11, 0.5);
        }

        .board-role {
            font-size: 0.72rem;
            font-weight: 700;
            color: var(--gold-bright);
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
            color: #e2e8f0;
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
            border-color: var(--gold-bright);
            box-shadow: 0 0 10px rgba(251, 191, 36, 0.2);
            background-color: #0d1527;
        }

        textarea {
            resize: vertical;
            min-height: 90px;
        }

        button.btn-submit {
            background: linear-gradient(135deg, var(--gold-bright) 0%, var(--gold-dark) 100%);
            color: #060913;
            font-weight: 800;
            font-size: 0.95rem;
            padding: 12px 20px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            width: 100%;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(245, 158, 11, 0.3);
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
            background: rgba(245, 158, 11, 0.12);
            color: var(--gold-bright);
            padding: 4px 12px;
            border-radius: 16px;
            font-size: 0.78rem;
            font-weight: 700;
            border: 1px solid rgba(245, 158, 11, 0.35);
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
            border: 1px solid rgba(245, 158, 11, 0.45);
            background: linear-gradient(145deg, #0d1527 0%, #131d35 100%);
        }

        .idea-card.featured::before {
            content: '';
            position: absolute;
            top: 0;
            right: 0;
            width: 4px;
            height: 100%;
            background: linear-gradient(180deg, var(--gold-bright), var(--gold-dark));
        }

        .badge-featured {
            background: linear-gradient(135deg, var(--gold-bright), var(--gold-dark));
            color: #000;
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
            color: var(--gold-bright);
            background: rgba(245, 158, 11, 0.1);
            padding: 2px 10px;
            border-radius: 15px;
            border: 1px solid rgba(245, 158, 11, 0.3);
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
            background: rgba(6, 9, 19, 0.7);
            border-radius: 8px;
            padding: 10px;
            margin-top: 10px;
            border: 1px solid rgba(245, 158, 11, 0.2);
        }

        .detail-box h4 {
            color: var(--gold-bright);
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
            border-right: 3px solid var(--gold-bright);
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

    <nav class="quick-nav">
        <button class="nav-btn active" onclick="switchPage('homePage', this)">🏛️ المجلس</button>
        <button class="nav-btn" onclick="switchPage('formPage', this)">💡 تقديم فكرة</button>
        <button class="nav-btn" onclick="switchPage('archivePage', this)">📁 الأرشيف</button>
    </nav>

    <header>
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
                    <path d="M75 42 L85 55 L100 35 L115 55 L125 42 L120 65 L80 65 Z" fill="url(#goldGrad)" stroke="#fef08a" stroke-width="1.5" />
                    <circle cx="75" cy="40" r="3" fill="#ffffff" />
                    <circle cx="100" cy="33" r="4" fill="#ffffff" />
                    <circle cx="125" cy="40" r="3" fill="#ffffff" />
                    <path d="M60 65 H140 V115 Q140 160 100 180 Q60 160 60 115 Z" fill="url(#shieldGrad)" stroke="url(#goldGrad)" stroke-width="4" />
                    <path d="M68 73 H132 V113 Q132 150 100 168 Q68 150 68 113 Z" fill="none" stroke="url(#goldGrad)" stroke-width="1.5" stroke-dasharray="4 2" opacity="0.8" />
                    <path d="M100 182 L100 192 M90 185 Q100 190 110 185" stroke="url(#goldGrad)" stroke-width="2" />
                </svg>
                <div class="crest-center-text">MTU</div>
            </div>
            <div class="royal-title-tag">MEDIA CLUB</div>
        </div>

        <br>
        <span class="site-badge">👑 منصة النادي الإعلامي</span>
        <h1>بنك الأفكار والأرشيف</h1>
        <p class="subtitle">المساحة السحابية لاستقبال وتوثيق مبادرات طلاب الجامعة</p>
    </header>

    <div class="container">

        <section id="homePage" class="page-section active">
            <div class="card">
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
            النادي الإعلامي (MTU) ©️ 2026
        </footer>

    </div>

    <script>
        const SCRIPT_URL = "https://script.google.com/macros/s/AKfycbwN5Ty-lRiwKN9lVy9F94l8C9mxgSK-uDkVT9JStVT0eHnWtETg6CFJRpmw5lObZwV6/exec";

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
                const response = await fetch(SCRIPT_URL);
                const ideas = await response.json();
                
                let html = '';
                if (ideas.length === 0) {
                    container.innerHTML = '<p style="text-align:center; color: var(--text-muted);">لا توجد أفكار مضافة حتى الآن.</p>';
                    counter.textContent = 'الأفكار: 0';
                    return;
                }

                ideas.forEach(idea => {
                    const embedVideo = getYouTubeEmbedUrl(idea.videoUrl);

                    html += `
                        <div class="idea-card">
                            <div class="idea-header">
                                <div class="idea-title">💡 ${idea.title || 'بدون عنوان'}</div>
                                <div class="idea-author">المقترح: ${idea.author || 'عضو'}</div>
                            </div>
                            <div class="idea-body">
                                ${idea.desc || ''}
                            </div>

                            ${(idea.imageUrl || embedVideo) ? `<div class="media-container">` : ''}
                                ${idea.imageUrl ? `<img src="${idea.imageUrl}" class="media-image" alt="صورة الفكرة" onerror="this.style.display='none'">` : ''}
                                ${embedVideo ? `<div class="video-wrapper"><iframe src="${embedVideo}" allowfullscreen></iframe></div>` : ''}
                            ${(idea.imageUrl || embedVideo) ? `</div>` : ''}

                            <div class="idea-footer-info">
                                <div>📍 الموقع: <span>${idea.location || 'غير محدد'}</span></div>
                                <div>👥 المسارات: <span>${idea.members || 'غير محدد'}</span></div>
                            </div>
                        </div>
                    `;
                });

                container.innerHTML = html;
                counter.textContent = `الأفكار: ${ideas.length}`;
            } catch (error) {
                console.error("Error loading data: ", error);
                counter.textContent = 'خطأ بالاتصال';
            }
        }

        loadSheetIdeas();
    </script>
</body>
</html>
