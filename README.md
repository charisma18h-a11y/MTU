# MTU
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>بنك الأفكار وأرشيف المشاريع - النادي الإعلامي MTU</title>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700;800;900&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg-dark: #080d1a;
            --bg-card: rgba(18, 25, 44, 0.75);
            --bg-card-solid: #12192c;
            --accent-gold: #fbbf24;
            --accent-purple: #8b5cf6;
            --accent-blue: #3b82f6;
            --accent-cyan: #06b6d4;
            --text-main: #f8fafc;
            --text-muted: #94a3b8;
            --border: rgba(255, 255, 255, 0.08);
            --border-glow: rgba(251, 191, 36, 0.3);
            --input-bg: #0b1120;
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
                radial-gradient(circle at 10% 20%, rgba(139, 92, 246, 0.15) 0%, transparent 40%),
                radial-gradient(circle at 90% 80%, rgba(251, 191, 36, 0.12) 0%, transparent 40%),
                radial-gradient(circle at 50% 50%, rgba(59, 130, 246, 0.08) 0%, transparent 60%);
            background-attachment: fixed;
            color: var(--text-main);
            line-height: 1.8;
            padding-bottom: 60px;
            min-height: 100vh;
        }

        /* الهيدر والشعار */
        header {
            position: relative;
            text-align: center;
            padding: 60px 20px 40px;
            background: linear-gradient(180deg, rgba(15, 23, 42, 0.9) 0%, rgba(8, 13, 26, 0.4) 100%);
            border-bottom: 1px solid var(--border);
            backdrop-filter: blur(10px);
            overflow: hidden;
        }

        header::before {
            content: '';
            position: absolute;
            top: 0;
            left: 50%;
            transform: translateX(-50%);
            width: 80%;
            height: 2px;
            background: linear-gradient(90deg, transparent, var(--accent-gold), var(--accent-purple), transparent);
        }

        /* شعار MTU الاحترافي */
        .logo-container {
            display: inline-flex;
            align-items: center;
            justify-content: center;
            margin-bottom: 20px;
            position: relative;
        }

        .logo-badge {
            width: 85px;
            height: 85px;
            background: linear-gradient(135deg, #1e293b, #0f172a);
            border: 2px solid var(--accent-gold);
            border-radius: 22px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            box-shadow: 0 0 25px rgba(251, 191, 36, 0.25), inset 0 0 15px rgba(139, 92, 246, 0.2);
            transform: rotate(-3deg);
            transition: all 0.3s ease;
        }

        .logo-badge:hover {
            transform: rotate(0deg) scale(1.05);
            box-shadow: 0 0 35px rgba(251, 191, 36, 0.4);
        }

        .logo-text {
            font-size: 1.8rem;
            font-weight: 900;
            background: linear-gradient(135deg, #ffffff 30%, var(--accent-gold) 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            letter-spacing: 2px;
            line-height: 1;
        }

        .logo-subtext {
            font-size: 0.65rem;
            font-weight: 800;
            color: var(--accent-cyan);
            letter-spacing: 1px;
            margin-top: 3px;
        }

        .site-badge {
            background: rgba(251, 191, 36, 0.1);
            color: var(--accent-gold);
            padding: 5px 18px;
            border-radius: 30px;
            font-size: 0.85rem;
            font-weight: 700;
            display: inline-block;
            margin-bottom: 15px;
            border: 1px solid rgba(251, 191, 36, 0.3);
        }

        h1 {
            font-size: 2.5rem;
            font-weight: 900;
            margin-bottom: 12px;
            background: linear-gradient(135deg, #ffffff 0%, #cbd5e1 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        p.subtitle {
            color: var(--text-muted);
            font-size: 1.05rem;
            max-width: 650px;
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
            box-shadow: 0 10px 30px -10px rgba(0, 0, 0, 0.5);
            transition: border-color 0.3s;
        }

        .card:hover {
            border-color: rgba(255, 255, 255, 0.15);
        }

        .section-title {
            font-size: 1.5rem;
            font-weight: 800;
            margin-bottom: 25px;
            display: flex;
            align-items: center;
            gap: 12px;
            color: var(--text-main);
        }

        .section-title span.icon {
            background: linear-gradient(135deg, var(--accent-gold), #d97706);
            color: #000;
            width: 38px;
            height: 38px;
            border-radius: 10px;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            font-size: 1.2rem;
            font-weight: bold;
            box-shadow: 0 4px 12px rgba(251, 191, 36, 0.3);
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
            border-color: var(--accent-gold);
            box-shadow: 0 0 15px rgba(251, 191, 36, 0.15);
            background-color: #0f172a;
        }

        textarea {
            resize: vertical;
            min-height: 110px;
        }

        button.btn-submit {
            background: linear-gradient(135deg, var(--accent-gold) 0%, #d97706 100%);
            color: #0d1322;
            font-weight: 800;
            font-size: 1.05rem;
            padding: 14px 30px;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            width: 100%;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(251, 191, 36, 0.25);
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }

        button.btn-submit:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 25px rgba(251, 191, 36, 0.4);
            background: linear-gradient(135deg, #fcd34d 0%, #f59e0b 100%);
        }

        /* الأرشيف الفاخر */
        .archive-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 25px;
            flex-wrap: wrap;
            gap: 15px;
        }

        .archive-counter {
            background: rgba(139, 92, 246, 0.15);
            color: var(--accent-purple);
            padding: 4px 14px;
            border-radius: 20px;
            font-size: 0.85rem;
            font-weight: 700;
            border: 1px solid rgba(139, 92, 246, 0.3);
        }

        .archive-grid {
            display: flex;
            flex-direction: column;
            gap: 25px;
        }

        /* بطاقة فكرة مميزة */
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
            border: 1px solid rgba(251, 191, 36, 0.4);
            box-shadow: 0 0 30px rgba(251, 191, 36, 0.08);
            background: linear-gradient(145deg, #12192c 0%, #1a233b 100%);
        }

        .idea-card.featured::before {
            content: '';
            position: absolute;
            top: 0;
            right: 0;
            width: 5px;
            height: 100%;
            background: linear-gradient(180deg, var(--accent-gold), var(--accent-purple));
        }

        .badge-featured {
            background: linear-gradient(135deg, var(--accent-gold), #d97706);
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
            color: var(--accent-gold);
            background: rgba(251, 191, 36, 0.1);
            padding: 4px 12px;
            border-radius: 20px;
            border: 1px solid rgba(251, 191, 36, 0.2);
            white-space: nowrap;
            font-weight: 700;
        }

        .idea-body {
            color: #cbd5e1;
            font-size: 0.98rem;
            margin-bottom: 20px;
            line-height: 1.8;
        }

        /* تفاصيل فكرة ملتقى السينما المفصلة */
        .detail-box {
            background: rgba(15, 23, 42, 0.6);
            border-radius: 10px;
            padding: 16px;
            margin-top: 15px;
            border: 1px solid rgba(255, 255, 255, 0.05);
        }

        .detail-box h4 {
            color: var(--accent-cyan);
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
            border-right: 3px solid var(--accent-purple);
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
        <!-- شعار MTU سينمائي وفاخر -->
        <div class="logo-container">
            <div class="logo-badge">
                <div class="logo-text">MTU</div>
                <div class="logo-subtext">MEDIA CLUB</div>
            </div>
        </div>
        <br>
        <span class="site-badge">منصة النادي الإعلامي</span>
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
                    <span class="icon" style="background: linear-gradient(135deg, var(--accent-purple), #6d28d9); color: #fff;">📁</span>
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

            // حفظ في LocalStorage
            saveIdeaToStorage(ideaData);

            // إضافة للواجهة
            renderIdeaCard(ideaData, true);

            // إعادة ضبط النموذج
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
                    <div>👥
