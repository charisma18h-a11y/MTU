# MTU
<!DOCTYPE html>
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
        }

        /* الهيدر والشعار الملكي */
        header {
            position: relative;
            text-align: center;
            padding: 55px 20px 40px;
            background: linear-gradient(180deg, rgba(12, 18, 34, 0.95) 0%, rgba(6, 9, 19, 0.6) 100%);
            border-bottom: 1px solid var(--border);
            backdrop-filter: blur(12px);
            overflow: hidden;
        }

        header::before {
            content: '';
            position: absolute;
            top: 0;
            left: 50%;
            transform: translateX(-50%);
            width: 70%;
            height: 2px;
            background: linear-gradient(90deg, transparent, var(--gold-dark), var(--gold-bright), var(--gold-dark), transparent);
        }

        /* 👑 الشعار الملكي الفاخر (Royal Crest) */
        .royal-crest-container {
            display: inline-flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            margin-bottom: 22px;
            position: relative;
        }

        .royal-crest {
            width: 145px;
            height: 145px;
            position: relative;
            display: flex;
            align-items: center;
            justify-content: center;
            filter: drop-shadow(0 0 22px rgba(245, 158, 11, 0.4));
            transition: transform 0.4s ease, filter 0.4s ease;
        }

        .royal-crest:hover {
            transform: scale(1.05);
            filter: drop-shadow(0 0 32px rgba(251, 191, 36, 0.6));
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
            font-size: 1.75rem;
            font-weight: 900;
            letter-spacing: 3px;
            background: linear-gradient(180deg, #ffffff 10%, #fef08a 50%, #eab308 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            text-shadow: 0 2px 10px rgba(0,0,0,0.8);
        }

        .royal-title-tag {
            font-size: 0.75rem;
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
            font-size: 0.9rem;
            font-weight: 700;
            display: inline-block;
            margin-top: 10px;
            margin-bottom: 14px;
            border: 1px solid rgba(245, 158, 11, 0.35);
            box-shadow: 0 0 15px rgba(245, 158, 11, 0.1);
        }

        h1 {
            font-size: 2.4rem;
            font-weight: 900;
            margin-bottom: 10px;
            background: linear-gradient(180deg, #ffffff 0%, #cbd5e1 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        p.subtitle {
            color: var(--text-muted);
            font-size: 1.05rem;
            max-width: 680px;
            margin: 0 auto;
        }

        /* الحاوية والبطاقات */
        .container {
            max-width: 950px;
            margin: 40px auto;
            padding: 0 20px;
        }

        .card {
            background: var(--bg-card);
            border: 1px solid var(--border);
            backdrop-filter: blur(12px);
            border-radius: 16px;
            padding: 32px;
            margin-bottom: 40px;
            box-shadow: 0 10px 30px -10px rgba(0, 0, 0, 0.6);
        }

        .section-title {
            font-size: 1.45rem;
            font-weight: 800;
            margin-bottom: 25px;
            display: flex;
            align-items: center;
            gap: 12px;
            color: var(--text-main);
        }

        .section-title span.icon {
            background: linear-gradient(135deg, var(--gold-bright), var(--gold-dark));
            color: #000;
            width: 38px;
            height: 38px;
            border-radius: 10px;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            font-size: 1.2rem;
            font-weight: bold;
            box-shadow: 0 4px 12px rgba(245, 158, 11, 0.3);
        }

        /* النموذج */
        .form-row {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
            gap: 20px;
        }

        .form-group {
            margin-bottom: 22px;
        }

        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 700;
            color: #e2e8f0;
            font-size: 0.95rem;
        }

        input[type="text"], textarea {
            width: 100%;
            padding: 14px 18px;
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
            min-height: 110px;
        }

        button.btn-submit {
            background: linear-gradient(135deg, var(--gold-bright) 0%, var(--gold-dark) 100%);
            color: #060913;
            font-weight: 800;
            font-size: 1.05rem;
            padding: 14px 30px;
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
            box-shadow: 0 8px 25px rgba(251, 191, 36, 0.45);
        }

        /* الأرشيف الملكي */
        .archive-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 25px;
            flex-wrap: wrap;
            gap: 15px;
        }

        .archive-counter {
            background: rgba(245, 158, 11, 0.12);
            color: var(--gold-bright);
            padding: 5px 16px;
            border-radius: 20px;
            font-size: 0.85rem;
            font-weight: 700;
            border: 1px solid rgba(245, 158, 11, 0.35);
        }

        .archive-grid {
            display: flex;
            flex-direction: column;
            gap: 25px;
        }

        /* بطاقة الفكرة المميزة */
        .idea-card {
            background: var(--bg-card-solid);
            border: 1px solid var(--border);
            border-radius: 14px;
            padding: 24px;
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
            padding: 3px 12px;
            border-radius: 6px;
            display: inline-block;
            margin-bottom: 12px;
        }

        .idea-header {
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            margin-bottom: 12px;
            gap: 15px;
            flex-wrap: wrap;
        }

        .idea-title {
            font-size: 1.3rem;
            font-weight: 800;
            color: #ffffff;
            line-height: 1.4;
        }

        .idea-author {
            font-size: 0.85rem;
            color: var(--gold-bright);
            background: rgba(245, 158, 11, 0.1);
            padding: 4px 14px;
            border-radius: 20px;
            border: 1px solid rgba(245, 158, 11, 0.3);
            white-space: nowrap;
            font-weight: 700;
        }

        .idea-body {
            color: #cbd5e1;
            font-size: 0.98rem;
            margin-bottom: 20px;
            line-height: 1.8;
        }

        .detail-box {
            background: rgba(6, 9, 19, 0.7);
            border-radius: 10px;
            padding: 16px;
            margin-top: 15px;
            border: 1px solid rgba(245, 158, 11, 0.2);
        }

        .detail-box h4 {
            color: var(--gold-bright);
            font-size: 0.95rem;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            gap: 8px;
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
            gap: 20px;
            margin-top: 18px;
            padding-top: 15px;
            border-top: 1px solid var(--border);
            font-size: 0.88rem;
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
            font-size: 0.9rem;
            padding-top: 30px;
            border-top: 1px solid var(--border);
            margin-top: 40px;
        }
    </style>
</head>
<body>

    <!-- الهيدر الرئيسي -->
    <header>
        <!-- ⚜️ الشعار الملكي الفاخر (Royal Crest) -->
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

                    <!-- التاج الملكي في الأعلى -->
                    <path d="M75 42 L85 55 L100 35 L115 55 L125 42 L120 65 L80 65 Z" fill="url(#goldGrad)" stroke="#fef08a" stroke-width="1.5" />
                    <circle cx="75" cy="40" r="3" fill="#ffffff" />
                    <circle cx="100" cy="33" r="4" fill="#ffffff" />
                    <circle cx="125" cy="40" r="3" fill="#ffffff" />

                    <!-- الأجنحة الملكية الجانبية -->
                    <path d="M45 75 Q20 60 10 90 Q30 95 48 85 M43 88 Q15 80 15 110 Q35 110 48 95 M42 100 Q20 100 25 125 Q42 120 48 108" fill="url(#goldGrad)" opacity="0.9" />
                    <path d="M155 75 Q180 60 190 90 Q170 95 152 85 M157 88 Q185 80 185 110 Q165 110 152 95 M158 100 Q180 100 175 125 Q158 120 152 108" fill="url(#goldGrad)" opacity="0.9" />

                    <!-- الدرع الملكي الرئيسي -->
                    <path d="M60 65 H140 V115 Q140 160 100 180 Q60 160 60 115 Z" fill="url(#shieldGrad)" stroke="url(#goldGrad)" stroke-width="4" />
                    <path d="M68 73 H132 V113 Q132 150 100 168 Q68 150 68 113 Z" fill="none" stroke="url(#goldGrad)" stroke-width="1.5" stroke-dasharray="4 2" opacity="0.8" />
                    <path d="M100 182 L100 192 M90 185 Q100 190 110 185" stroke="url(#goldGrad)" stroke-width="2" />
                </svg>

                <div class="crest-center-text">MTU</div>
            </div>
            <div class="royal-title-tag">MEDIA CLUB</div>
        </div>

        <br>
        <span class="site-badge">👑 المنصة الملكية للنادي الإعلامي</span>
        <h1>بنك الأفكار وأرشيف المشاريع</h1>
        <p class="subtitle">المساحة المخصصة لاستقبال المبادرات وتوثيق أفكار طلاب ونادي الإعلام للرفع بها للجامعة والإدارة</p>
    </header>

    <div class="container">

        <!-- نموذج تقديم فكرة جديدة -->
        <section class="card">
            <h2 class="section-title">
                <span class="icon">💡</span>
                تقديم فكرة / مشروع جديد
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

                <button type="submit" class="btn-submit">
                    <span>حفظ الفكرة وإضافتها للأرشيف</span>
                    <span>🚀</span>
                </button>
            </form>
        </section>

        <!-- أرشيف الأفكار المستند عليه -->
        <section>
            <div class="archive-header">
                <h2 class="section-title" style="margin-bottom: 0;">
                    <span class="icon">📁</span>
                    أرشيف الأفكار والمشاريع (مرجع الإدارة)
                </h2>
                <span class="archive-counter" id="archiveCount">الأفكار التوثيقية: 1</span>
            </div>

            <div class="archive-grid" id="archiveContainer">
                
                <!-- فكرة خالد الهلال - التوثيق الكامل والمفصل -->
                <div class="idea-card featured">
                    <span class="badge-featured">⭐ مشروع مقترح وموثّق بالتفاصيل</span>
                    
                    <div class="idea-header">
                        <div class="idea-title">🎬 ملتقى سينما الجامعة (رؤية سينمائية وإعلامية)</div>
                        <div class="idea-author">المقترح: خالد الهلال</div>
                    </div>

                    <div class="idea-body">
                        مشروع متكامل يهدف إلى دمج الفن البصري بالمهارات الخطابية والإعلامية لطلاب الجامعة. يُقيم النادي الإعلامي ملتقى سينمائي وثقافي تنظيمي يضم ورش عمل تفاعلية حية تقودها مسارات النادي، يتبعها عرض فيلم قصير هادف، وختام حواري ونقدي تديره كوادر مسار التقديم والخطابة.
                        
                        <!-- المحاور والورش التفصيلية -->
                        <div class="detail-box">
                            <h4>🎯 الورش التفاعلية ومسارات المشاركة:</h4>
                            <div class="tracks-grid">
                                <div class="track-item">
                                    <strong>1. مسار التقديم والخطابة</strong>
                                    الافتتاحية والترحيب، إدارة الجلسة الحوارية والنقدية مع الجمهور بعد العرض.
                                </div>
                                <div class="track-item">
                                    <strong>2. مسار الإنتاج</strong>
                                    كيفية التخطيط للفيلم القصير، وتحويل الفكرة إلى سيناريو جاهز للتنفيذ.
                                </div>
                                <div class="track-item">
                                    <strong>3. مسار التصوير والإضاءة</strong>
                                    تطبيق عملي حقيقي على المسرح لشرح زوايا الكاميرا وتأثير الإضاءة في المشاعر.
                                </div>
                                <div class="track-item">
                                    <strong>4. مسار التسويق والإعلام</strong>
                                    عرض استراتيجية تسويق الفيلم، تصميم الإعلانات التشويقية وصناعة الهوية.
                                </div>
                            </div>
                        </div>

                        <!-- احتياجات الفعالية والأجندة -->
                        <div class="detail-box">
                            <h4>⏱️ أجندة الفعالية والمتطلبات المطلوبة من الجامعة:</h4>
                            <p style="font-size: 0.88rem; color: #cbd5e1;">
                                • <strong>الأجندة (75 دقيقة):</strong> افتتاح وترحيب (10د) ⬅️ ورش تفاعلية للمسارات (30د) ⬅️ عرض الفيلم القصير (20د) ⬅️ حوار وختام (15د).<br>
                                • <strong>المتطلبات:</strong> مسرح الجامعة الرئيسي، شاشة عرض Data Show ونظام صوتي، إضاءة مسرحية متناسقة، ودعم الترويج.
                            </p>
                        </div>
                    </div>

                    <div class="idea-footer-info">
                        <div>📍 موقع التنفيذ: <span>مسرح الجامعة الرئيسي / قاعة المؤتمرات</span></div>
                        <div>👥 المسارات المشاركة: <span>جميع مسارات النادي الإعلامي</span></div>
                    </div>
                </div>

            </div>
        </section>

        <footer>
            النادي الإعلامي (MTU) - جميع الحقوق محفوظة © 2026
        </footer>

    </div>

    <!-- كود حفظ واسترجاع الأفكار ديناميكياً -->
    <script>
        document.addEventListener('DOMContentLoaded', function() {
            loadSavedIdeas();
        });

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

            alert('✅ تم حفظ الفكرة بنجاح وإضافتها إلى أرشيف النادي الإعلامي!');
        });

        function renderIdeaCard(idea, prepend = false) {
            const archive = document.getElementById('archiveContainer');
            
            const card = document.createElement('div');
            card.className = 'idea-card';
            card.innerHTML = `
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
    </script>
</body>
</html>
