# MTU
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
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
        }

        body {
            background-color: var(--bg-dark);
            background-image: 
                radial-gradient(circle at 50% 10%, rgba(245, 158, 11, 0.12) 0%, transparent 50%),
                radial-gradient(circle at 10% 80%, rgba(180, 83, 9, 0.08) 0%, transparent 40%),
                radial-gradient(circle at 90% 90%, rgba(251, 191, 36, 0.06) 0%, transparent 50%);
            background-attachment: fixed;
            color: var(--text-main);
            line-height: 1.8;
            padding-bottom: 60px;
            min-height: 100vh;
            overflow-x: hidden;
        }

        /* شريط التنقل العلوي الذكي */
        .quick-nav {
            position: sticky;
            top: 0;
            z-index: 1000;
            background: rgba(6, 9, 19, 0.95);
            backdrop-filter: blur(12px);
            border-bottom: 1px solid var(--border);
            padding: 12px 20px;
            display: flex;
            justify-content: center;
            gap: 15px;
            flex-wrap: wrap;
        }

        .nav-btn {
            background: rgba(245, 158, 11, 0.1);
            color: var(--gold-bright);
            border: 1px solid rgba(245, 158, 11, 0.35);
            padding: 8px 20px;
            border-radius: 20px;
            font-size: 0.9rem;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.3s ease;
            display: inline-flex;
            align-items: center;
            gap: 8px;
        }

        .nav-btn:hover, .nav-btn.active {
            background: linear-gradient(135deg, var(--gold-bright), var(--gold-dark));
            color: #000;
            transform: translateY(-2px);
            box-shadow: 0 4px 15px rgba(245, 158, 11, 0.3);
        }

        /* الهيدر والشعار الملكي */
        header {
            position: relative;
            text-align: center;
            padding: 45px 20px 30px;
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
            margin-bottom: 15px;
            position: relative;
        }

        .royal-crest {
            width: 130px;
            height: 130px;
            position: relative;
            display: flex;
            align-items: center;
            justify-content: center;
            filter: drop-shadow(0 0 22px rgba(245, 158, 11, 0.4));
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
            font-size: 1.6rem;
            font-weight: 900;
            letter-spacing: 3px;
            background: linear-gradient(180deg, #ffffff 10%, #fef08a 50%, #eab308 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .royal-title-tag {
            font-size: 0.7rem;
            font-weight: 800;
            letter-spacing: 3px;
            color: var(--gold-bright);
            text-transform: uppercase;
            margin-top: -6px;
            background: linear-gradient(90deg, transparent, rgba(245, 158, 11, 0.15), transparent);
            padding: 2px 20px;
            border-bottom: 1px solid rgba(245, 158, 11, 0.35);
        }

        .site-badge {
            background: rgba(245, 158, 11, 0.1);
            color: var(--gold-bright);
            padding: 5px 22px;
            border-radius: 30px;
            font-size: 0.85rem;
            font-weight: 700;
            display: inline-block;
            margin-bottom: 10px;
            border: 1px solid rgba(245, 158, 11, 0.35);
        }

        h1 {
            font-size: 2.1rem;
            font-weight: 900;
            margin-bottom: 8px;
            background: linear-gradient(180deg, #ffffff 0%, #cbd5e1 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        p.subtitle {
            color: var(--text-muted);
            font-size: 0.98rem;
            max-width: 680px;
            margin: 0 auto;
            padding: 0 10px;
        }

        /* الحاوية والصفحات */
        .container {
            max-width: 950px;
            margin: 30px auto;
            padding: 0 15px;
        }

        .page-section {
            display: none;
        }

        .page-section.active {
            display: block;
            animation: fadeIn 0.4s ease-in-out;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .card {
            background: var(--bg-card);
            border: 1px solid var(--border);
            backdrop-filter: blur(12px);
            border-radius: 16px;
            padding: 25px;
            margin-bottom: 30px;
            box-shadow: 0 10px 30px -10px rgba(0, 0, 0, 0.6);
        }

        .section-title {
            font-size: 1.35rem;
            font-weight: 800;
            margin-bottom: 20px;
            display: flex;
            align-items: center;
            gap: 12px;
            color: var(--text-main);
        }

        .section-title span.icon {
            background: linear-gradient(135deg, var(--gold-bright), var(--gold-dark));
            color: #000;
            width: 35px;
            height: 35px;
            border-radius: 10px;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            font-size: 1.1rem;
            box-shadow: 0 4px 12px rgba(245, 158, 11, 0.3);
        }

        /* مجلس الإدارة */
        .board-hierarchy {
            display: flex;
            flex-direction: column;
            gap: 15px;
        }

        .board-tier-1 { display: flex; justify-content: center; }
        .board-tier-2 { display: grid; grid-template-columns: repeat(auto-fit, minmax(240px, 1fr)); gap: 15px; }
        .board-tier-3 { display: grid; grid-template-columns: repeat(auto-fit, minmax(180px, 1fr)); gap: 12px; }

        .board-card {
            background: var(--bg-card-solid);
            border: 1px solid var(--border);
            border-radius: 12px;
            padding: 16px;
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
            max-width: 320px;
            width: 100%;
            margin: 0 auto;
        }

        .board-card.tech-lead {
            background: linear-gradient(145deg, #0d1527 0%, #1a233a 100%);
            border: 1px solid rgba(245, 158, 11, 0.5);
        }

        .board-role {
            font-size: 0.78rem;
            font-weight: 700;
            color: var(--gold-bright);
            margin-bottom: 4px;
            text-transform: uppercase;
        }

        .board-name {
            font-size: 1.05rem;
            font-weight: 800;
            color: #ffffff;
        }

        /* نموذج تقديم فكرة */
        .form-row {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
            gap: 15px;
        }

        .form-group {
            margin-bottom: 18px;
        }

        label {
            display: block;
            margin-bottom: 6px;
            font-weight: 700;
            color: #e2e8f0;
            font-size: 0.9rem;
        }

        input[type="text"], textarea {
            width: 100%;
            padding: 12px 16px;
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
            box-shadow: 0 0 12px rgba(251, 191, 36, 0.2);
            background-color: #0d1527;
        }

        textarea {
            resize: vertical;
            min-height: 100px;
        }

        button.btn-submit {
            background: linear-gradient(135deg, var(--gold-bright) 0%, var(--gold-dark) 100%);
            color: #060913;
            font-weight: 800;
            font-size: 1rem;
            padding: 14px 25px;
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
        }

        button.btn-submit:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(251, 191, 36, 0.45);
        }

        /* الأرشيف السحابي */
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
            padding: 5px 15px;
            border-radius: 20px;
            font-size: 0.82rem;
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
            padding: 20px;
            position: relative;
            overflow: hidden;
            transition: all 0.3s ease;
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
            font-size: 0.72rem;
            font-weight: 800;
            padding: 3px 10px;
            border-radius: 6px;
            display: inline-block;
            margin-bottom: 10px;
        }

        .idea-header {
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            margin-bottom: 10px;
            gap: 12px;
            flex-wrap: wrap;
        }

        .idea-title {
            font-size: 1.2rem;
            font-weight: 800;
            color: #ffffff;
        }

        .idea-author {
            font-size: 0.82rem;
            color: var(--gold-bright);
            background: rgba(245, 158, 11, 0.1);
            padding: 3px 12px;
            border-radius: 20px;
            border: 1px solid rgba(245, 158, 11, 0.3);
            font-weight: 700;
        }

        .idea-body {
            color: #cbd5e1;
            font-size: 0.95rem;
            margin-bottom: 15px;
        }

        .detail-box {
            background: rgba(6, 9, 19, 0.7);
            border-radius: 10px;
            padding: 14px;
            margin-top: 12px;
            border: 1px solid rgba(245, 158, 11, 0.2);
        }

        .detail-box h4 {
            color: var(--gold-bright);
            font-size: 0.9rem;
            margin-bottom: 8px;
        }

        .tracks-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
            gap: 8px;
            margin-top: 8px;
        }

        .track-item {
            background: rgba(255, 255, 255, 0.03);
            border-radius: 8px;
            padding: 8px;
            font-size: 0.82rem;
            border-right: 3px solid var(--gold-bright);
        }

        .track-item strong { color: #fff; display: block; margin-bottom: 2px; }

        .idea-footer-info {
            display: flex;
            gap: 15px;
            margin-top: 15px;
            padding-top: 12px;
            border-top: 1px solid var(--border);
            font-size: 0.85rem;
            color: var(--text-muted);
            flex-wrap: wrap;
        }

        .idea-footer-info span { color: #fff; font-weight: 600; }

        footer {
            text-align: center;
            color: var(--text-muted);
            font-size: 0.85rem;
            padding-top: 25px;
            border-top: 1px solid var(--border);
            margin-top: 35px;
        }

        @media (max-width: 600px) {
            h1 { font-size: 1.7rem; }
            .quick-nav { padding: 8px 10px; gap: 8px; }
            .nav-btn { padding: 6px 12px; font-size: 0.82rem; }
            .card { padding: 18px; }
        }
    </style>
</head>
<body>

    <!-- شريط التنقل العلوي بين الصفحات -->
    <nav class="quick-nav">
        <button class="nav-btn active" onclick="switchPage('homePage', this)">🏛️ مجلس النادي</button>
        <button class="nav-btn" onclick="switchPage('formPage', this)">💡 تقديم فكرة</button>
        <button class="nav-btn" onclick="switchPage('archivePage', this)">📁 الأرشيف السحابي</button>
    </nav>

    <!-- الهيدر الرئيسي والشعار -->
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
        <h1>بنك الأفكار وأرشيف المشاريع</h1>
        <p class="subtitle">المساحة السحابية المخصصة لاستقبال مبادرات الطلاب وتوثيقها بشكل مباشر للجميع</p>
    </header>

    <div class="container">

        <!-- 1. صفحة مجلس النادي (الرئيسية) -->
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

        <!-- 2. صفحة تقديم فكرة جديدة -->
        <section id="formPage" class="page-section">
            <div class="card">
                <h2 class="section-title">
                    <span class="icon">💡</span>
                    تقديم فكرة / مشروع جديد (تخزين سحابي مباشر)
                </h2>
                
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

                    <button type="submit" class="btn-submit" id="submitBtn">
                        <span>حفظ الفكرة وإرسالها للسحابة</span>
                        <span>🚀</span>
                    </button>
                </form>
            </div>
        </section>

        <!-- 3. صفحة الأرشيف السحابي -->
        <section id="archivePage" class="page-section">
            <div class="archive-header">
                <h2 class="section-title" style="margin-bottom: 0;">
                    <span class="icon">📁</span>
                    أرشيف الأفكار والمشاريع (سحابي مباشر)
                </h2>
                <span class="archive-counter" id="archiveCount">جاري التحميل من السحابة...</span>
            </div>

            <div class="archive-grid" id="archiveContainer">
                <!-- مشروع ملتقى سينما الجامعة الثابت -->
                <div class="idea-card featured">
                    <span class="badge-featured">⭐ مشروع مقترح وموثّق بالتفاصيل</span>
                    <div class="idea-header">
                        <div class="idea-title">🎬 ملتقى سينما الجامعة (رؤية سينمائية وإعلامية)</div>
                        <div class="idea-author">المقترح: خالد أحمد الهلال</div>
                    </div>
                    <div class="idea-body">
                        مشروع متكامل يهدف إلى دمج الفن البصري بالمهارات الخطابية والإعلامية لطلاب الجامعة. يُقيم النادي الإعلامي ملتقى سينمائي وثقافي تنظيمي يضم ورش عمل تفاعلية حية.
                        <div class="detail-box">
                            <h4>🎯 الورش التفاعلية ومسارات المشاركة:</h4>
                            <div class="tracks-grid">
                                <div class="track-item"><strong>1. مسار التقديم</strong>إدارة الجلسة الحوارية والنقدية.</div>
                                <div class="track-item"><strong>2. مسار الإنتاج</strong>تحويل الفكرة إلى سيناريو.</div>
                                <div class="track-item"><strong>3. مسار التصوير</strong>زوايا الكاميرا والإضاءة.</div>
                                <div class="track-item"><strong>4. مسار التسويق</strong>صناعة الهوية والإعلانات.</div>
                            </div>
                        </div>
                    </div>
                    <div class="idea-footer-info">
                        <div>📍 الموقع: <span>مسرح الجامعة الرئيسي</span></div>
                        <div>👥 المسارات: <span>جميع مسارات النادي الإعلامي</span></div>
                    </div>
                </div>
            </div>
        </section>

        <footer>
            النادي الإعلامي (MTU) - جميع الحقوق محفوظة ©️ 2026
        </footer>

    </div>

    <!-- كود الربط السحابي (Firebase) -->
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
        import { getFirestore, collection, addDoc, getDocs } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-firestore.js";

        // مفاتيح مشروعك الفعلي على فايربيس
        const firebaseConfig = {
            apiKey: "AIzaSyA831Ex0tSyAQaGUQAlIzAFb8fBH89Xktw",
            authDomain: "mtu-media-club.firebaseapp.com",
            projectId: "mtu-media-club",
            storageBucket: "mtu-media-club.firebasestorage.app",
            messagingSenderId: "95732996772",
            appId: "1:95732996772:web:e6f2ed19f699e123ffa431",
            measurementId: "G-KHQXQWTMZG"
        };

        const app = initializeApp(firebaseConfig);
        const db = getFirestore(app);

        // التنقل بين الصفحات السلس
        window.switchPage = function(pageId, btnElement) {
            document.querySelectorAll('.page-section').forEach(sec => sec.classList.remove('active'));
            document.querySelectorAll('.nav-btn').forEach(btn => btn.classList.remove('active'));
            
            document.getElementById(pageId).classList.add('active');
            btnElement.classList.add('active');
            window.scrollTo({ top: 0, behavior: 'smooth' });

            if(pageId === 'archivePage') {
                loadCloudIdeas();
            }
        };

        // إرسال الفكرة إلى السحابة
        document.getElementById('ideaForm').addEventListener('submit', async function(e) {
            e.preventDefault();
            
            const submitBtn = document.getElementById('submitBtn');
            submitBtn.disabled = true;
            submitBtn.innerHTML = '<span>جاري الحفظ في السحابة...</span> ⏳';

            const author = document.getElementById('authorName').value;
            const title = document.getElementById('ideaTitle').value;
            const desc = document.getElementById('ideaDescription').value;
            const location = document.getElementById('ideaLocation').value;
            const members = document.getElementById('ideaMembers').value;

            try {
                await addDoc(collection(db, "ideas"), {
                    author,
                    title,
                    desc,
                    location,
                    members,
                    createdAt: new Date()
                });

                alert('✅ تم حفظ الفكرة في سحابة النادي بنجاح وسيحراها الجميع الآن!');
                this.reset();
                
                // الانتقال تلقائياً للأرشيف لرؤية الفكرة
                const archiveBtn = document.querySelectorAll('.nav-btn')[2];
                switchPage('archivePage', archiveBtn);
            } catch (error) {
                console.error("خطأ أثناء الحفظ: ", error);
                alert('❌ حدث خطأ أثناء الحفظ، تأكد من اتصالك بالإنترنت.');
            } finally {
                submitBtn.disabled = false;
                submitBtn.innerHTML = '<span>حفظ الفكرة وإرسالها للسحابة</span> <span>🚀</span>';
            }
        });

        // جلب الأفكار من سحابة فايربيس
        async function loadCloudIdeas() {
            const container = document.getElementById('archiveContainer');
            const counter = document.getElementById('archiveCount');
            
            try {
                const querySnapshot = await getDocs(collection(db, "ideas"));
                
                // الاحتفاظ بالمشروع الثابت ومسح القديم المكرر إن وجد
                let cloudIdeasHTML = '';
                let count = querySnapshot.size;

                querySnapshot.forEach((doc) => {
                    const idea = doc.data();
                    cloudIdeasHTML += `
                        <div class="idea-card">
                            <div class="idea-header">
                                <div class="idea-title">💡 ${idea.title}</div>
                                <div class="idea-author">المقترح: ${idea.author}</div>
                            </div>
                            <div class="idea-body">
                                ${idea.desc}
                            </div>
                            <div class="idea-footer-info">
                                <div>📍 الموقع: <span>${idea.location}</span></div>
                                <div>👥 المسارات: <span>${idea.members}</span></div>
                            </div>
                        </div>
                    `;
                });

                // تحديث العداد وعرض البطاقات السحابية أسفل المشروع الثابت
                counter.textContent = `الأفكار السحابية: ${count + 1}`;
            } catch (error) {
                console.error("خطأ في جلب البيانات: ", error);
                counter.textContent = 'خطأ في الاتصال بالسحابة';
            }
        }

        // تحميل الأفكار عند فتح الصفحة لأول مرة
        loadCloudIdeas();
    </script>
</body>
</html>
