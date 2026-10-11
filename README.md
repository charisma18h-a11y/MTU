# MTU
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>بنك الأفكار والأرشيف - النادي الإعلامي</title>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700;900&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg-color: #0f172a;
            --card-bg: #1e293b;
            --accent: #f59e0b;
            --accent-hover: #d97706;
            --text-main: #f8fafc;
            --text-muted: #94a3b8;
            --border: #334155;
            --input-bg: #0f172a;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Cairo', sans-serif;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-main);
            line-height: 1.8;
            padding-bottom: 60px;
        }

        header {
            background: linear-gradient(135deg, #1e1b4b, #0f172a);
            text-align: center;
            padding: 50px 20px;
            border-bottom: 2px solid var(--accent);
        }

        .badge {
            background-color: rgba(245, 158, 11, 0.15);
            color: var(--accent);
            padding: 6px 16px;
            border-radius: 20px;
            font-size: 0.9rem;
            font-weight: 700;
            display: inline-block;
            margin-bottom: 12px;
            border: 1px solid var(--accent);
        }

        h1 {
            font-size: 2.2rem;
            font-weight: 900;
            color: #ffffff;
            margin-bottom: 8px;
        }

        p.subtitle {
            color: var(--text-muted);
            font-size: 1rem;
            max-width: 600px;
            margin: 0 auto;
        }

        .container {
            max-width: 900px;
            margin: 40px auto;
            padding: 0 20px;
        }

        .card {
            background-color: var(--card-bg);
            border: 1px solid var(--border);
            border-radius: 12px;
            padding: 28px;
            margin-bottom: 40px;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.3);
        }

        .section-title {
            font-size: 1.5rem;
            font-weight: 700;
            margin-bottom: 20px;
            color: var(--accent);
            border-right: 4px solid var(--accent);
            padding-right: 12px;
        }

        .form-group {
            margin-bottom: 20px;
        }

        .form-row {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
        }

        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: var(--text-main);
            font-size: 0.95rem;
        }

        input[type="text"], textarea, select {
            width: 100%;
            padding: 12px 16px;
            background-color: var(--input-bg);
            border: 1px solid var(--border);
            border-radius: 8px;
            color: var(--text-main);
            font-size: 0.95rem;
            outline: none;
            transition: border-color 0.2s;
        }

        input[type="text"]:focus, textarea:focus, select:focus {
            border-color: var(--accent);
        }

        textarea {
            resize: vertical;
            min-height: 100px;
        }

        button.btn-submit {
            background-color: var(--accent);
            color: #000;
            font-weight: 700;
            font-size: 1rem;
            padding: 12px 28px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            width: 100%;
            transition: background 0.2s;
        }

        button.btn-submit:hover {
            background-color: var(--accent-hover);
        }

        /* الأرشيف */
        .archive-grid {
            display: flex;
            flex-direction: column;
            gap: 20px;
        }

        .idea-card {
            background: var(--card-bg);
            border: 1px solid var(--border);
            border-radius: 10px;
            padding: 20px;
            border-right: 4px solid var(--accent);
        }

        .idea-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
            flex-wrap: wrap;
            gap: 10px;
        }

        .idea-title {
            font-size: 1.2rem;
            font-weight: 700;
            color: #fff;
        }

        .idea-author {
            font-size: 0.85rem;
            color: var(--accent);
            background: rgba(245, 158, 11, 0.1);
            padding: 2px 10px;
            border-radius: 15px;
        }

        .idea-details {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 10px;
            margin-top: 12px;
            padding-top: 12px;
            border-top: 1px solid var(--border);
            font-size: 0.9rem;
            color: var(--text-muted);
        }

        .idea-details span {
            color: var(--text-main);
        }

        footer {
            text-align: center;
            color: var(--text-muted);
            font-size: 0.9rem;
            padding-top: 20px;
        }
    </style>
</head>
<body>

    <header>
        <span class="badge">منصة النادي الإعلامي</span>
        <h1>بنك الأفكار وأرشيف المشاريع</h1>
        <p class="subtitle">شاركونا إبداعاتكم واقتراحاتكم لتطوير فعاليات ومشاريع النادي الإعلامي بالجامعة</p>
    </header>

    <div class="container">

        <!-- نموذج تقديم فكرة جديدة -->
        <section class="card">
            <h2 class="section-title">تقديم فكرة / مشروع جديد</h2>
            <form id="ideaForm">
                
                <div class="form-row">
                    <div class="form-group">
                        <label for="authorName">اسم تقديم الفكرة (العضو/الطالب):</label>
                        <input type="text" id="authorName" placeholder="أدخل اسمك الكريم" required>
                    </div>

                    <div class="form-group">
                        <label for="ideaTitle">عنوان الفكرة / المشروع:</label>
                        <input type="text" id="ideaTitle" placeholder="مثال: ملتقى السينما / بودكاست إعلامي" required>
                    </div>
                </div>

                <div class="form-group">
                    <label for="ideaDescription">تفاصيل وآلية تطبيق الفكرة:</label>
                    <textarea id="ideaDescription" placeholder="اشرح الفكرة وكيف يمكن تنفيذها والهدف منها..." required></textarea>
                </div>

                <div class="form-row">
                    <div class="form-group">
                        <label for="ideaLocation">موقع التنفيذ المقترح:</label>
                        <input type="text" id="ideaLocation" placeholder="مثال: مسرح الجامعة الرئيسي / أونلاين" required>
                    </div>

                    <div class="form-group">
                        <label for="ideaMembers">الأعضاء / المسارات المساهمة:</label>
                        <input type="text" id="ideaMembers" placeholder="مثال: مسار التصوير + مسار التقديم" required>
                    </div>
                </div>

                <button type="submit" class="btn-submit">حفظ الفكرة وإضافتها للأرشيف 🚀</button>
            </form>
        </section>

        <!-- أرشيف الأفكار المستند عليه -->
        <section>
            <h2 class="section-title">أرشيف الأفكار المقترحة (مرجع الإدارة)</h2>
            <div class="archive-grid" id="archiveContainer">
                
                <!-- مثال تجريبي لأول فكرة في الأرشيف (فكرتك!) -->
                <div class="idea-card">
                    <div class="idea-header">
                        <span class="idea-title">🎬 ملتقى سينما الجامعة (الأركان والفيلم القصير)</span>
                        <span class="idea-author">المقترح: خالد الهلال</span>
                    </div>
                    <p style="color: var(--text-muted); font-size: 0.95rem;">
                        تنظيم ملتقى سينمائي يضم أركان تفاعلية لمسارات النادي (تصوير، إنتاج، تسويق، تقديم)، يعقبه عرض فيلم قصير وجلسة حوارية مع الحضور.
                    </p>
                    <div class="idea-details">
                        <div>📍 الموقع: <span>مسرح الجامعة الرئيسي</span></div>
                        <div>👥 المسارات: <span>جميع مسارات النادي الإعلامي</span></div>
                    </div>
                </div>

            </div>
        </section>

        <footer>
            النادي الإعلامي - جامعة الطائف © 2026
        </footer>

    </div>

    <script>
        // كود بسيط لإضافة الفكرة فوراً للأرشيف كمعاينة حية
        document.getElementById('ideaForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const author = document.getElementById('authorName').value;
            const title = document.getElementById('ideaTitle').value;
            const desc = document.getElementById('ideaDescription').value;
            const location = document.getElementById('ideaLocation').value;
            const members = document.getElementById('ideaMembers').value;

            const archive = document.getElementById('archiveContainer');

            const newCard = document.createElement('div');
            newCard.className = 'idea-card';
            newCard.innerHTML = `
                <div class="idea-header">
                    <span class="idea-title">💡 ${title}</span>
                    <span class="idea-author">المقترح: ${author}</span>
                </div>
                <p style="color: var(--text-muted); font-size: 0.95rem;">${desc}</p>
                <div class="idea-details">
                    <div>📍 الموقع: <span>${location}</span></div>
                    <div>👥 المسارات: <span>${members}</span></div>
                </div>
            `;

            archive.prepend(newCard);
            this.reset();
            alert('تم تسجيل الفكرة بنجاح وإضافتها إلى أرشيف النادي!');
        });
    </script>
</body>
</html>
