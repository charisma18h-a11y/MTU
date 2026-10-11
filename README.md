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
            --gold-bright: #fbbf24;
            --gold-dark: #b45309;
            --text-main: #f8fafc;
            --text-muted: #94a3b8;
            --border: rgba(245, 158, 11, 0.25);
            --input-bg: #080e1a;
        }

        * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Cairo', sans-serif; }

        body {
            background-color: var(--bg-dark);
            background-image: 
                radial-gradient(circle at 50% 10%, rgba(245, 158, 11, 0.12) 0%, transparent 50%),
                radial-gradient(circle at 10% 80%, rgba(180, 83, 9, 0.08) 0%, transparent 40%);
            background-attachment: fixed;
            color: var(--text-main);
            line-height: 1.8;
            padding-bottom: 60px;
            min-height: 100vh;
        }

        header {
            position: relative;
            text-align: center;
            padding: 55px 20px 40px;
            background: linear-gradient(180deg, rgba(12, 18, 34, 0.95) 0%, rgba(6, 9, 19, 0.6) 100%);
            border-bottom: 1px solid var(--border);
            backdrop-filter: blur(12px);
        }

        .royal-crest-container {
            display: inline-flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            margin-bottom: 22px;
        }

        .royal-crest {
            width: 145px;
            height: 145px;
            position: relative;
            display: flex;
            align-items: center;
            justify-content: center;
            filter: drop-shadow(0 0 22px rgba(245, 158, 11, 0.4));
        }

        .crest-svg { width: 100%; height: 100%; }

        .crest-center-text {
            position: absolute;
            top: 52%; left: 50%;
            transform: translate(-50%, -50%);
            font-family: 'Cinzel', 'Cairo', serif;
            font-size: 1.75rem;
            font-weight: 900;
            letter-spacing: 3px;
            background: linear-gradient(180deg, #ffffff 10%, #fef08a 50%, #eab308 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .royal-title-tag {
            font-size: 0.75rem; font-weight: 800; letter-spacing: 3px;
            color: var(--gold-bright); text-transform: uppercase; margin-top: -6px;
            padding: 2px 20px; border-bottom: 1px solid rgba(245, 158, 11, 0.35);
        }

        .site-badge {
            background: rgba(245, 158, 11, 0.1);
            color: var(--gold-bright);
            padding: 5px 22px; border-radius: 30px;
            font-size: 0.9rem; font-weight: 700;
            display: inline-block; margin: 10px 0 14px;
            border: 1px solid rgba(245, 158, 11, 0.35);
        }

        h1 { font-size: 2.4rem; font-weight: 900; margin-bottom: 10px; color: #fff; }
        p.subtitle { color: var(--text-muted); font-size: 1.05rem; max-width: 680px; margin: 0 auto; }

        .container { max-width: 950px; margin: 40px auto; padding: 0 20px; }

        .card {
            background: var(--bg-card);
            border: 1px solid var(--border);
            border-radius: 16px; padding: 32px;
            margin-bottom: 40px; box-shadow: 0 10px 30px rgba(0,0,0,0.6);
        }

        .section-title {
            font-size: 1.45rem; font-weight: 800; margin-bottom: 25px;
            display: flex; align-items: center; gap: 12px; color: var(--text-main);
        }

        .section-title span.icon {
            background: linear-gradient(135deg, var(--gold-bright), var(--gold-dark));
            color: #000; width: 38px; height: 38px; border-radius: 10px;
            display: inline-flex; align-items: center; justify-content: center;
        }

        .form-row { display: grid; grid-template-columns: repeat(auto-fit, minmax(260px, 1fr)); gap: 20px; }
        .form-group { margin-bottom: 22px; }
        label { display: block; margin-bottom: 8px; font-weight: 700; color: #e2e8f0; font-size: 0.95rem; }

        input[type="text"], textarea {
            width: 100%; padding: 14px 18px;
            background-color: var(--input-bg);
            border: 1px solid var(--border); border-radius: 10px;
            color: var(--text-main); font-size: 0.95rem; outline: none;
        }

        input[type="text"]:focus, textarea:focus { border-color: var(--gold-bright); }
        textarea { resize: vertical; min-height: 110px; }

        button.btn-submit {
            background: linear-gradient(135deg, var(--gold-bright) 0%, var(--gold-dark) 100%);
            color: #060913; font-weight: 800; font-size: 1.05rem;
            padding: 14px 30px; border: none; border-radius: 10px;
            cursor: pointer; width: 100%; display: flex; align-items: center;
            justify-content: center; gap: 10px; box-shadow: 0 4px 15px rgba(245, 158, 11, 0.3);
        }

        .archive-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 25px; flex-wrap: wrap; gap: 15px; }
        .archive-counter { background: rgba(245, 158, 11, 0.12); color: var(--gold-bright); padding: 5px 16px; border-radius: 20px; font-size: 0.85rem; font-weight: 700; border: 1px solid rgba(245, 158, 11, 0.35); }
        .archive-grid { display: flex; flex-direction: column; gap: 25px; }

        .idea-card {
            background: var(--bg-card-solid);
            border: 1px solid var(--border); border-radius: 14px;
            padding: 24px; position: relative; overflow: hidden;
        }

        .idea-card.featured {
            border: 1px solid rgba(245, 158, 11, 0.45);
            background: linear-gradient(145deg, #0d1527 0%, #131d35 100%);
        }

        .idea-card.featured::before {
            content: ''; position: absolute; top: 0; right: 0; width: 5px; height: 100%;
            background: linear-gradient(180deg, var(--gold-bright), var(--gold-dark));
        }

        .badge-featured { background: linear-gradient(135deg, var(--gold-bright), var(--gold-dark)); color: #000; font-size: 0.75rem; font-weight: 800; padding: 3px 12px; border-radius: 6px; display: inline-block; margin-bottom: 12px; }
        .idea-header { display: flex; justify-content: space-between; align-items: flex-start; margin-bottom: 12px; gap: 15px; flex-wrap: wrap; }
        .idea-title { font-size: 1.3rem; font-weight: 800; color: #fff; }
        .idea-author { font-size: 0.85rem; color: var(--gold-bright); background: rgba(245, 158, 11, 0.1); padding: 4px 14px; border-radius: 20px; border: 1px solid rgba(245, 158, 11, 0.3); font-weight: 700; }
        .idea-body { color: #cbd5e1; font-size: 0.98rem; margin-bottom: 20px; line-height: 1.8; }
        .idea-footer-info { display: flex; gap: 20px; margin-top: 18px; padding-top: 15px; border-top: 1px solid var(--border); font-size: 0.88rem; color: var(--text-muted); flex-wrap: wrap; }
        .idea-footer-info span { color: #fff; font-weight: 600; }
        footer { text-align: center; color: var(--text-muted); font-size: 0.9rem; padding-top: 30px; border-top: 1px solid var(--border); margin-top: 40px; }
    </style>
</head>
<body>

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
                    <circle cx="75" cy="40" r="3" fill="#fff" /><circle cx="100" cy="33" r="4" fill="#fff" /><circle cx="125" cy="40" r="3" fill="#fff" />
                    <path d="M45 75 Q20 60 10 90 Q30 95 48 85 M43 88 Q15 80 15 110 Q35 110 48 95 M42 100 Q20 100 25 125 Q42 120 48 108" fill="url(#goldGrad)" opacity="0.9" />
                    <path d="M155 75 Q180 60 190 90 Q170 95 152 85 M157 88 Q185 80 185 110 Q165 110 152 95 M158 100 Q180 100 175 125 Q158 120 152 108" fill="url(#goldGrad)" opacity="0.9" />
                    <path d="M60 65 H140 V115 Q140 160 100 180 Q60 160 60 115 Z" fill="url(#shieldGrad)" stroke="url(#goldGrad)" stroke-width="4" />
                    <path d="M68 73 H132 V113 Q132 150 100 168 Q68 150 68 113 Z" fill="none" stroke="url(#goldGrad)" stroke-width="1.5" stroke-dasharray="4 2" opacity="0.8" />
                </svg>
                <div class="crest-center-text">MTU</div>
            </div>
            <div class="royal-title-tag">MEDIA CLUB</div>
        </div>
        <span class="site-badge">👑 المنصة الملكية للنادي الإعلامي</span>
        <h1>بنك الأفكار وأرشيف المشاريع</h1>
        <p class="subtitle">المساحة المخصصة لاستقبال المبادرات وتوثيق أفكار طلاب ونادي الإعلام للرفع بها للجامعة والإدارة</p>
    </header>

    <div class="container">
        <section class="card">
            <h2 class="section-title"><span class="icon">💡</span> تقديم فكرة / مشروع جديد</h2>
            <form id="ideaForm">
                <div class="form-row">
                    <div class="form-group">
                        <label for="author">اسم مُقدم الفكرة:</label>
                        <input type="text" id="author" placeholder="أدخل اسمك الكريم" required>
                    </div>
                    <div class="form-group">
                        <label for="title">عنوان الفكرة أو المبادرة:</label>
                        <input type="text" id="title" placeholder="مثال: بودكاست النادي" required>
                    </div>
                </div>
                <div class="form-group">
                    <label for="desc">تفاصيل وآلية تطبيق الفكرة:</label>
                    <textarea id="desc" placeholder="اشرح هدف الفكرة ومحاور تنفيذها..." required></textarea>
                </div>
                <div class="form-row">
                    <div class="form-group">
                        <label for="location">الموقع المقترح للتنفيذ:</label>
                        <input type="text" id="location" placeholder="مثال: مسرح الجامعة" required>
                    </div>
                    <div class="form-group">
                        <label for="members">المسارات والمشاركون:</label>
                        <input type="text" id="members" placeholder="مثال: مسار التقديم والتصوير" required>
                    </div>
                </div>
                <button type="submit" class="btn-submit"><span>حفظ الفكرة وإرسالها للسحابة</span><span>🚀</span></button>
            </form>
        </section>

        <section>
            <div class="archive-header">
                <h2 class="section-title" style="margin-bottom: 0;"><span class="icon">📁</span> أرشيف الأفكار السحابي (مرجع الإدارة)</h2>
                <span class="archive-counter" id="archiveCount">جاري تحميل الأفكار...</span>
            </div>
            <div class="archive-grid" id="archiveContainer"></div>
        </section>

        <footer>النادي الإعلامي (MTU) - جميع الحقوق محفوظة © 2026</footer>
    </div>

    <script>
        // ضع رابط SheetDB الخاص بك هنا بدلاً من الرابط المؤقت
        const API_URL = "https://sheetdb.io/api/v1/YOUR_API_KEY";

        document.addEventListener('DOMContentLoaded', function() {
            fetchIdeas();
        });

        document.getElementById('ideaForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const submitBtn = document.querySelector('.btn-submit');
            submitBtn.textContent = "جاري الإرسال للسحابة...";
            submitBtn.disabled = true;

            const formData = {
                data: {
                    author: document.getElementById('author').value,
                    title: document.getElementById('title').value,
                    desc: document.getElementById('desc').value,
                    location: document.getElementById('location').value,
                    members: document.getElementById('members').value
                }
            };

            fetch(API_URL, {
                method: 'POST',
                headers: {
                    'Accept': 'application/json',
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(formData)
            })
            .then(res => res.json())
            .then(data => {
                alert('✅ تم إرسال الفكرة وحفظها في السحابة بنجاح!');
                this.reset();
                submitBtn.innerHTML = '<span>حفظ الفكرة وإرسالها للسحابة</span><span>🚀</span>';
                submitBtn.disabled = false;
                fetchIdeas();
            })
            .catch(err => {
                console.error(err);
                alert('⚠️ حدث خطأ، تأكد من وضع رابط SheetDB بشكل صحيح.');
                submitBtn.innerHTML = '<span>حفظ الفكرة وإرسالها للسحابة</span><span>🚀</span>';
                submitBtn.disabled = false;
            });
        });

        function fetchIdeas() {
            const archive = document.getElementById('archiveContainer');
            archive.innerHTML = '<p style="text-align:center; color:var(--text-muted);">جاري جلب الأفكار من السحابة...</p>';

            fetch(API_URL)
            .then(res => res.json())
            .then(data => {
                archive.innerHTML = '';
                
                let html = `
                    <div class="idea-card featured">
                        <span class="badge-featured">⭐ مشروع مقترح وموثّق بالتفاصيل</span>
                        <div class="idea-header">
                            <div class="idea-title">🎬 ملتقى سينما الجامعة (رؤية سينمائية وإعلامية)</div>
                            <div class="idea-author">المقترح: خالد الهلال</div>
                        </div>
                        <div class="idea-body">
                            مشروع متكامل يهدف إلى دمج الفن البصري بالمهارات الخطابية والإعلامية لطلاب الجامعة. يُقيم النادي الإعلامي ملتقى سينمائي وثقافي تنظيمي يضم ورش عمل تفاعلية حية تقودها مسارات النادي، يتبعها عرض فيلم قصير هادف، وختام حواري ونقدي.
                        </div>
                        <div class="idea-footer-info">
                            <div>📍 الموقع: <span>مسرح الجامعة الرئيسي</span></div>
                            <div>👥 المسارات: <span>جميع مسارات النادي الإعلامي</span></div>
                        </div>
                    </div>
                `;

                if (Array.isArray(data)) {
                    data.reverse().forEach(idea => {
                        if(idea.title) {
                            html += `
                                <div class="idea-card">
                                    <div class="idea-header">
                                        <div class="idea-title">💡 ${idea.title}</div>
                                        <div class="idea-author">المقترح: ${idea.author || 'غير محدد'}</div>
                                    </div>
                                    <div class="idea-body">${idea.desc || ''}</div>
                                    <div class="idea-footer-info">
                                        <div>📍 الموقع: <span>${idea.location || ''}</span></div>
                                        <div>👥 المسارات: <span>${idea.members || ''}</span></div>
                                    </div>
                                </div>
                            `;
                        }
                    });
                }

                archive.innerHTML = html;
                document.getElementById('archiveCount').textContent = `الأفكار السحابية: ${Array.isArray(data) ? data.length + 1 : 1}`;
            })
            .catch(err => {
                archive.innerHTML = '<p style="text-align:center; color:#ef4444;">تعذر تحميل الأفكار، تأكد من ربط رابط API بشكل صحيح.</p>';
            });
        }
    </script>
</body>
</html>
