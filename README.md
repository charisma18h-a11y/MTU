# MTU
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>منصة النادي الإعلامي - جامعة الطائف</title>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700;800;900&family=Montserrat:wght@800;900&display=swap" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>
    <style>
        :root {
            --bg-dark: #0a0a0c;
            --bg-deep: #050507;
            --bg-card: rgba(18, 18, 24, 0.88);
            --bg-card-solid: #121218;
            --accent-primary: #3b82f6;
            --accent-glow: #60a5fa;
            --text-main: #f8fafc;
            --text-muted: #94a3b8;
            --border: rgba(255, 255, 255, 0.12);
            --input-bg: #0c0c10;
            --brand-red: #ff4d2d;
            --admin-color: #238636;
        }

        * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Cairo', sans-serif; -webkit-tap-highlight-color: transparent; }

        body {
            background-color: var(--bg-dark); color: var(--text-main); line-height: 1.7; padding-bottom: 40px; min-height: 100vh; overflow-x: hidden; width: 100%; position: relative;
        }

        .bg-video-container {
            position: fixed; top: 0; left: 0; width: 100vw; height: 100vh; z-index: -99; overflow: hidden; pointer-events: none; background: #000;
        }
        .bg-video-container iframe {
            position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%) scale(1.35); width: 100vw; height: 56.25vw; min-height: 100vh; min-width: 177.77vh; pointer-events: none; filter: brightness(0.55) contrast(1.1);
        }
        .bg-overlay {
            position: fixed; top: 0; left: 0; width: 100vw; height: 100vh; background: radial-gradient(circle at center, rgba(10, 10, 12, 0.6) 0%, rgba(5, 5, 7, 0.9) 100%); z-index: -98; pointer-events: none;
        }

        .mtu-logo-container { display: inline-flex; align-items: center; justify-content: center; margin-bottom: 15px; position: relative; }
        .mtu-logo-text { font-family: 'Montserrat', sans-serif; font-size: 3.2rem; font-weight: 900; letter-spacing: -1px; color: #ffffff; line-height: 1; display: flex; align-items: flex-start; position: relative; }
        .mtu-dot { width: 14px; height: 14px; background-color: var(--brand-red); border-radius: 50%; display: inline-block; margin-left: 2px; margin-top: 2px; box-shadow: 0 0 10px rgba(255, 77, 45, 0.8); }

        #welcomeScreen {
            position: fixed; inset: 0; z-index: 99999; background: var(--bg-deep); display: flex; flex-direction: column; align-items: center; justify-content: center; padding: 20px; text-align: center; transition: opacity 0.5s ease;
        }

        .auth-card {
            background: var(--bg-card); border: 1px solid var(--border); backdrop-filter: blur(12px); border-radius: 16px; padding: 25px 20px; width: 100%; max-width: 400px; box-shadow: 0 15px 35px rgba(0,0,0,0.8); margin-top: 15px;
        }

        .quick-nav {
            position: sticky; top: 0; z-index: 1000; background: rgba(15, 15, 20, 0.85); backdrop-filter: blur(12px); border-bottom: 1px solid var(--border); padding: 10px 12px; display: flex; justify-content: center; gap: 6px; width: 100%; flex-wrap: wrap;
        }

        .nav-btn {
            background: rgba(255, 255, 255, 0.05); color: var(--text-main); border: 1px solid var(--border); padding: 8px 12px; border-radius: 20px; font-size: 0.78rem; font-weight: 700; cursor: pointer; transition: all 0.3s ease; display: inline-flex; align-items: center; justify-content: center; gap: 5px; text-align: center; white-space: nowrap;
        }

        .nav-btn:hover, .nav-btn.active {
            background: var(--accent-primary); color: #ffffff; border-color: var(--accent-glow); transform: translateY(-2px); box-shadow: 0 4px 15px rgba(59, 130, 246, 0.4);
        }

        header { position: relative; text-align: center; padding: 30px 15px 20px; background: rgba(18, 18, 24, 0.65); border-bottom: 1px solid var(--border); backdrop-filter: blur(12px); }
        .site-badge { background: rgba(59, 130, 246, 0.15); color: var(--accent-glow); padding: 5px 18px; border-radius: 30px; font-size: 0.8rem; font-weight: 700; display: inline-block; margin-bottom: 8px; border: 1px solid rgba(59, 130, 246, 0.3); }
        h1 { font-size: 1.6rem; font-weight: 900; margin-bottom: 6px; color: #fff; }
        p.subtitle { color: var(--text-muted); font-size: 0.88rem; max-width: 680px; margin: 0 auto; }

        .container { max-width: 950px; margin: 20px auto; padding: 0 12px; width: 100%; }
        .page-section { display: none; }
        .page-section.active { display: block; }

        .card { background: var(--bg-card); border: 1px solid var(--border); backdrop-filter: blur(12px); border-radius: 14px; padding: 18px 14px; margin-bottom: 20px; box-shadow: 0 10px 30px -10px rgba(0, 0, 0, 0.8); }
        .section-title { font-size: 1.15rem; font-weight: 800; margin-bottom: 16px; display: flex; align-items: center; gap: 10px; color: var(--text-main); }
        .section-title span.icon { background: var(--accent-primary); color: #ffffff; width: 30px; height: 30px; border-radius: 8px; display: inline-flex; align-items: center; justify-content: center; }

        .profile-header-card { text-align: center; padding: 25px; }
        .avatar-container { position: relative; width: 95px; height: 95px; margin: 0 auto 12px; }
        .avatar-preview { width: 100%; height: 100%; border-radius: 50%; object-fit: cover; border: 3px solid var(--accent-primary); background: #1a1a24; display: flex; align-items: center; justify-content: center; font-size: 2rem; color: var(--text-muted); }
        .avatar-upload-btn { position: absolute; bottom: 0; left: 0; background: var(--accent-primary); color: #fff; width: 32px; height: 32px; border-radius: 50%; display: flex; align-items: center; justify-content: center; cursor: pointer; border: 2px solid var(--bg-card); font-size: 1rem; box-shadow: 0 4px 10px rgba(0,0,0,0.5); }
        
        .board-hierarchy { display: flex; flex-direction: column; gap: 12px; }
        .board-tier-1 { display: flex; justify-content: center; }
        .board-tier-2 { display: grid; grid-template-columns: repeat(auto-fit, minmax(140px, 1fr)); gap: 10px; }
        .board-tier-3 { display: grid; grid-template-columns: repeat(auto-fit, minmax(130px, 1fr)); gap: 10px; }
        .board-card { background: var(--bg-card-solid); border: 1px solid var(--border); border-radius: 10px; padding: 12px 10px; text-align: center; }
        .board-card.supervisor { background: linear-gradient(145deg, #1e1b4b 0%, #0f172a 100%); width: 100%; max-width: 280px; margin: 0 auto; }
        .board-card.tech-lead { background: linear-gradient(145deg, #0f172a 100%, #1e293b 100%); }
        .board-role { font-size: 0.72rem; font-weight: 700; color: var(--accent-glow); margin-bottom: 2px; }
        .board-name { font-size: 0.92rem; font-weight: 800; color: #ffffff; }

        .form-row { display: grid; grid-template-columns: 1fr; gap: 12px; }
        @media (min-width: 600px) { .form-row { grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); } }
        .form-group { margin-bottom: 14px; text-align: right; }
        label { display: block; margin-bottom: 5px; font-weight: 700; color: #cbd5e1; font-size: 0.85rem; }
        input, textarea, select { width: 100%; padding: 10px 12px; background-color: var(--input-bg); border: 1px solid var(--border); border-radius: 8px; color: var(--text-main); font-size: 0.9rem; outline: none; }
        button.btn-submit { background: var(--accent-primary); color: #ffffff; font-weight: 800; font-size: 0.95rem; padding: 12px 20px; border: none; border-radius: 8px; cursor: pointer; width: 100%; display: flex; align-items: center; justify-content: center; gap: 8px; }

        .member-row-item { background: rgba(255,255,255,0.03); border: 1px solid var(--border); padding: 12px; border-radius: 8px; margin-bottom: 8px; display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 10px; }

        .archive-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 15px; }
        .archive-counter { background: rgba(59, 130, 246, 0.15); color: var(--accent-glow); padding: 4px 12px; border-radius: 16px; font-size: 0.78rem; font-weight: 700; border: 1px solid rgba(59, 130, 246, 0.3); }
        .archive-grid { display: flex; flex-direction: column; gap: 15px; }
        .idea-card { background: var(--bg-card-solid); border: 1px solid var(--border); border-radius: 12px; padding: 15px; position: relative; }
        .idea-header { display: flex; justify-content: space-between; margin-bottom: 8px; flex-wrap: wrap; gap: 6px; }
        .idea-title { font-size: 1.05rem; font-weight: 800; color: #fff; }
        .idea-author { font-size: 0.75rem; color: var(--accent-glow); background: rgba(59, 130, 246, 0.12); padding: 2px 10px; border-radius: 15px; }
        .idea-body { color: #cbd5e1; font-size: 0.88rem; margin-bottom: 12px; }
        .video-wrapper { position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; border-radius: 8px; margin-top: 10px; }
        .video-wrapper iframe { position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: none; }
        .auth-switch { text-align: center; margin-top: 12px; font-size: 0.85rem; color: var(--text-muted); }
        .auth-switch a { color: var(--accent-glow); cursor: pointer; text-decoration: underline; }
        .error-msg { color: #f85149; font-size: 0.8rem; text-align: center; margin-top: 8px; }
        footer { text-align: center; color: var(--text-muted); font-size: 0.8rem; padding-top: 20px; border-top: 1px solid var(--border); margin-top: 25px; }
    </style>
</head>
<body>

    <div class="bg-video-container">
        <iframe src="https://www.youtube.com/embed/_TkXgy18J_g?autoplay=1&mute=1&controls=0&loop=1&playlist=_TkXgy18J_g&playsinline=1&enablejsapi=1" allow="autoplay; encrypted-media"></iframe>
    </div>
    <div class="bg-overlay"></div>

    <!-- شاشة تسجيل الدخول -->
    <div id="welcomeScreen">
        <div class="mtu-logo-container"><div class="mtu-logo-text">MTU<span class="mtu-dot"></span></div></div>
        <span class="site-badge" style="margin-top: 5px;">منصة النادي الإعلامي</span>
        <h1 id="authMainTitle" style="font-size: 1.3rem; margin-top: 5px;">تسجيل الدخول لمنصة النادي الإعلامي</h1>
        
        <div class="auth-card">
            <form id="authForm" onsubmit="handleSupabaseAuth(event)">
                <div class="form-group" id="fullNameGroup" style="display: none;">
                    <label>الاسم الكامل:</label>
                    <input type="text" id="authFullName" placeholder="ادخل اسمك الكامل">
                </div>
                <div class="form-group" id="trackGroup" style="display: none;">
                    <label>اختر مسارك في النادي:</label>
                    <select id="authTrack">
                        <option value="تصوير وإضاءة">📷 تصوير وإضاءة</option>
                        <option value="مونتاج وموشن جرافيك">🎬 مونتاج وموشن جرافيك</option>
                        <option value="إنتاج برامج وبودكاست">🎙️ إنتاج برامج وبودكاست</option>
                        <option value="تصميم وهوية بصرية">🎨 تصميم وهوية بصرية</option>
                        <option value="كتابة وصحافة إعلامية">✍️ كتابة وصحافة إعلامية</option>
                    </select>
                </div>
                <div class="form-group"><label>البريد الإلكتروني:</label><input type="email" id="authEmail" placeholder="name@example.com" required></div>
                <div class="form-group"><label>كلمة المرور:</label><input type="password" id="authPassword" placeholder="••••••••" required></div>
                <button type="submit" class="btn-submit" id="authBtn"><span id="authBtnText">دخول المنصة</span><span>🚀</span></button>
                <div id="authError" class="error-msg"></div>
            </form>
            <div class="auth-switch"><span id="switchText">ليس لديك حساب؟</span> <a onclick="toggleAuthMode()" id="switchLink">التسجيل في النادي الإعلامي</a></div>
        </div>
    </div>

    <!-- شريط التنقل العلوي -->
    <nav class="quick-nav">
        <button class="nav-btn active" onclick="switchPage('homePage', this)">🏛️ المجلس</button>
        <button class="nav-btn" onclick="switchPage('profilePage', this)">👤 بروفايلي</button>
        <button class="nav-btn" onclick="switchPage('formPage', this)">💡 تقديم فكرة</button>
        <button class="nav-btn" onclick="switchPage('archivePage', this)">📁 الأرشيف</button>
        <button class="nav-btn" id="adminNavBtn" style="display: none; background: rgba(35, 134, 54, 0.2); border-color: var(--admin-color);" onclick="switchPage('adminPage', this)">⚙️ المشرف</button>
        <button class="nav-btn" onclick="logout()" style="background: rgba(248, 81, 73, 0.15); border-color: rgba(248, 81, 73, 0.3); color: #f85149;">🚪 خروج</button>
    </nav>

    <header>
        <div class="mtu-logo-container" style="margin-bottom: 5px;"><div class="mtu-logo-text" style="font-size: 2.2rem;">MTU<span class="mtu-dot" style="width: 10px; height: 10px;"></span></div></div>
        <br><span class="site-badge">منصة النادي الإعلامي</span>
        <h1>بنك الأفكار والأرشيف</h1>
        <p class="subtitle">المساحة السحابية لاستقبال وتوثيق مبادرات طلاب جامعة الطائف</p>
    </header>

    <div class="container">

        <!-- شريط الحالة والترحيب الشخصي -->
        <div class="card" style="padding: 12px 20px; display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 10px;">
            <div>👤 أهلاً بك: <strong id="barUserName" style="color: var(--accent-glow);">...</strong></div>
            <div>المسار: <span id="barUserTrack" style="background: rgba(59,130,246,0.15); padding: 2px 10px; border-radius: 10px; border: 1px solid rgba(59,130,246,0.3);">عضو</span></div>
            <div>الرتبة: <span id="barUserRole" style="background: rgba(35,134,54,0.15); padding: 2px 10px; border-radius: 10px; color: #4ade80;">عضو</span></div>
        </div>

        <!-- صفحة المجلس -->
        <section id="homePage" class="page-section active">
            <div class="card">
                <h2 class="section-title"><span class="icon">👥</span>مجلس النادي وهيكلة الإدارة</h2>
                <div class="board-hierarchy">
                    <div class="board-tier-1"><div class="board-card supervisor"><div class="board-role">مشرف النادي</div><div class="board-name">د. حمزه فرج</div></div></div>
                    <div class="board-tier-2">
                        <div class="board-card"><div class="board-role">رئيس النادي</div><div class="board-name">عبدالرحمن علي الزهراني</div></div>
                        <div class="board-card"><div class="board-role">نائب الرئيس</div><div class="board-name">ماجد الشاطري</div></div>
                    </div>
                    <div class="board-tier-3">
                        <div class="board-card"><div class="board-role">عضو مجلس الإدارة</div><div class="board-name">نواف عبد الله المالكي</div></div>
                        <div class="board-card"><div class="board-role">عضو مجلس الإدارة</div><div class="board-name">حمد عايض الحارثي</div></div>
                        <div class="board-card"><div class="board-role">عضو مجلس الإدارة</div><div class="board-name">عبد الله مزيد السواط</div></div>
                        <div class="board-card"><div class="board-role">عضو مجلس الإدارة</div><div class="board-name">عبد الرحمن نجم العتيبي</div></div>
                    </div>
                    <div class="board-tier-3">
                        <div class="board-card tech-lead" style="grid-column: 1 / -1; max-width: 320px; margin: 0 auto; width: 100%;">
                            <div class="board-role">مسؤول تقنية المعلومات (IT)</div><div class="board-name">خالد أحمد الهلال</div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- صفحة بروفايلي الشخصي -->
        <section id="profilePage" class="page-section">
            <div class="card profile-header-card">
                <div class="avatar-container">
                    <div class="avatar-preview" id="avatarPreviewContainer">👤</div>
                    <label for="avatarFileInput" class="avatar-upload-btn" title="اختر صورة من الجوال">➕</label>
                    <input type="file" id="avatarFileInput" accept="image/*" style="display: none;" onchange="previewAvatar(this)">
                </div>
                <h2 id="profileDisplayName" style="font-size: 1.3rem; margin-bottom: 4px; color: #fff;">اسم العضو</h2>
                <span id="profileRoleBadge" style="background: rgba(59,130,246,0.2); color: var(--accent-glow); padding: 3px 12px; border-radius: 12px; font-size: 0.75rem; font-weight: 700;">عضو</span>
                
                <form id="profileForm" onsubmit="updateProfile(event)" style="margin-top: 20px; text-align: right;">
                    <div class="form-group">
                        <label>نبذة تعريفية عنك (Bio):</label>
                        <textarea id="inputBio" placeholder="اكتب نبذة عن مهاراتك واهتماماتك الإعلامية..."></textarea>
                    </div>
                    <div class="form-row">
                        <div class="form-group">
                            <label>مسارك في النادي:</label>
                            <select id="inputTrack">
                                <option value="تصوير وإضاءة">📷 تصوير وإضاءة</option>
                                <option value="مونتاج وموشن جرافيك">🎬 مونتاج وموشن جرافيك</option>
                                <option value="إنتاج برامج وبودكاست">🎙️ إنتاج برامج وبودكاست</option>
                                <option value="تصميم وهوية بصرية">🎨 تصميم وهوية بصرية</option>
                                <option value="كتابة وصحافة إعلامية">✍️ كتابة وصحافة إعلامية</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label>رابط معرض الأعمال (Portfolio / GitHub):</label>
                            <input type="url" id="inputPortfolio" placeholder="https://github.com/username">
                        </div>
                    </div>
                    <button type="submit" class="btn-submit" id="saveProfileBtn"><span>حفظ التعديلات في البروفايل</span><span>💾</span></button>
                </form>
            </div>
        </section>

        <!-- صفحة تقديم فكرة -->
        <section id="formPage" class="page-section">
            <div class="card">
                <h2 class="section-title"><span class="icon">💡</span>تقديم فكرة / مشروع جديد</h2>
                <form id="ideaForm">
                    <div class="form-row">
                        <div class="form-group"><label>اسم مُقدم الفكرة:</label><input type="text" id="authorName" readonly style="opacity: 0.8;"></div>
                        <div class="form-group"><label>عنوان الفكرة أو المبادرة:</label><input type="text" id="ideaTitle" required></div>
                    </div>
                    <div class="form-group"><label>تفاصيل وآلية تطبيق الفكرة:</label><textarea id="ideaDescription" required></textarea></div>
                    <div class="form-row">
                        <div class="form-group"><label>الموقع المقترح للتنفيذ:</label><input type="text" id="ideaLocation" required></div>
                        <div class="form-group"><label>المسارات والمشاركون:</label><input type="text" id="ideaMembers" required></div>
                    </div>
                    <div class="form-row">
                        <div class="form-group"><label>رابط صورة/تصميم (اختياري):</label><input type="url" id="imageUrl"></div>
                        <div class="form-group"><label>رابط فيديو يوتيوب (اختياري):</label><input type="url" id="videoUrl"></div>
                    </div>
                    <button type="submit" class="btn-submit" id="submitBtn"><span>حفظ الفكرة في السحابة</span><span>🚀</span></button>
                </form>
            </div>
        </section>

        <!-- صفحة الأرشيف -->
        <section id="archivePage" class="page-section">
            <div class="archive-header">
                <h2 class="section-title" style="margin-bottom: 0;"><span class="icon">📁</span>الأرشيف</h2>
                <span class="archive-counter" id="archiveCount">جاري التحميل...</span>
            </div>
            <div class="archive-grid" id="archiveContainer"></div>
        </section>

        <!-- لوحة تحكم المشرف المحمية -->
        <section id="adminPage" class="page-section">
            <div class="card">
                <h2 class="section-title"><span class="icon">⚙️</span>لوحة تحكم المشرف وإدارة الأعضاء</h2>
                <p style="color: var(--text-muted); font-size: 0.9rem; margin-bottom: 15px;">أهلاً بك يا مشرف المنصة. يمكنك استعراض جميع الأعضاء ونقلهم بين المسارات مباشرة.</p>
                <div style="margin-top: 15px;">
                    <h3 style="font-size: 1rem; margin-bottom: 10px; color: var(--accent-glow);">قائمة أعضاء النادي المسجلين:</h3>
                    <div id="adminMembersList">جاري جلب الأعضاء...</div>
                </div>
            </div>
        </section>

        <footer>النادي الإعلامي (MTU) ©️ 2026 | Media Club</footer>
    </div>

    <script>
        const SUPABASE_URL = 'https://hlgvjdknxtywdqjikayz.supabase.co';
        const SUPABASE_ANON_KEY = 'sb_publishable_xw3iN_Cb5eFA125MyBx8TQ_3aTyXjqr';
        const supabaseClient = supabase.createClient(SUPABASE_URL, SUPABASE_ANON_KEY);
        const SCRIPT_URL = "https://script.google.com/macros/s/AKfycbwN5Ty-lRiwKN9lVy9F94l8C9mxgSK-uDkVT9JStVT0eHnWtETg6CFJRpmw5lObZwV6/exec";
        
        let currentUser = null;
        let isRegisterMode = false;
        let uploadedAvatarBase64 = '';

        function toggleAuthMode() {
            isRegisterMode = !isRegisterMode;
            document.getElementById('authMainTitle').innerText = isRegisterMode ? 'التسجيل في النادي الإعلامي' : 'تسجيل الدخول لمنصة النادي الإعلامي';
            document.getElementById('authBtnText').innerText = isRegisterMode ? 'إتمام التسجيل والإنشاء' : 'دخول المنصة';
            document.getElementById('fullNameGroup').style.display = isRegisterMode ? 'block' : 'none';
            document.getElementById('trackGroup').style.display = isRegisterMode ? 'block' : 'none';
            document.getElementById('switchText').innerText = isRegisterMode ? 'لديك حساب بالفعل؟' : 'ليس لديك حساب؟';
            document.getElementById('switchLink').innerText = isRegisterMode ? 'سجل الدخول هنا' : 'التسجيل في النادي الإعلامي';
            document.getElementById('authError').innerText = '';
        }

        async function handleSupabaseAuth(e) {
            e.preventDefault();
            const email = document.getElementById('authEmail').value.trim();
            const password = document.getElementById('authPassword').value.trim();
            const fullName = document.getElementById('authFullName').value.trim();
            const track = document.getElementById('authTrack').value;
            const errorEl = document.getElementById('authError');
            const btn = document.getElementById('authBtn');

            errorEl.innerText = '';
            btn.disabled = true;
            btn.innerHTML = '<span>جاري المعالجة...</span> ⏳';

            try {
                if (isRegisterMode) {
                    const { data, error } = await supabaseClient.auth.signUp({
                        email, password, options: { data: { full_name: fullName } }
                    });
                    if (error) throw error;
                    if (data.user) {
                        await supabaseClient.from('profiles').upsert({
                            id: data.user.id, full_name: fullName || 'عضو جديد', role: 'member', track: track
                        });
                    }
                    alert('✅ تم التسجيل بنجاح!');
                }
                const { data: loginData, error: loginError } = await supabaseClient.auth.signInWithPassword({ email, password });
                if (loginError) throw loginError;
                if (loginData.user) loadUserProfile(loginData.user);
            } catch (err) {
                errorEl.innerText = err.message || 'خطأ في المصادقة.';
                btn.disabled = false;
                btn.innerHTML = '<span>تأكيد</span> 🚀';
            }
        }

        async function loadUserProfile(user) {
            currentUser = user;
            const welcome = document.getElementById('welcomeScreen');
            if (welcome) {
                welcome.style.opacity = '0';
                setTimeout(() => welcome.style.display = 'none', 500);
            }

            const { data: profile } = await supabaseClient
                .from('profiles')
                .select('*')
                .eq('id', user.id)
                .maybeSingle();

            const name = profile?.full_name || user.email.split('@')[0];
            const role = profile?.role || 'member';
            const track = profile?.track || 'عام';

            document.getElementById('barUserName').innerText = name;
            document.getElementById('barUserTrack').innerText = track;
            document.getElementById('barUserRole').innerText = role === 'admin' ? 'مشرف (Admin)' : 'عضو';
            
            document.getElementById('profileDisplayName').innerText = name;
            document.getElementById('authorName').value = name;
            document.getElementById('inputBio').value = profile?.bio || '';
            document.getElementById('inputTrack').value = track;
            document.getElementById('inputPortfolio').value = profile?.portfolio_url || '';
            
            uploadedAvatarBase64 = profile?.avatar_url || '';
            if (uploadedAvatarBase64) {
                document.getElementById('avatarPreviewContainer').innerHTML = `<img src="${uploadedAvatarBase64}" style="width:100%; height:100%; border-radius:50%; object-fit:cover;">`;
            }

            if (role === 'admin') {
                document.getElementById('profileRoleBadge').innerText = 'مشرف (Admin)';
                document.getElementById('adminNavBtn').style.display = 'inline-flex';
                loadAdminMembers();
            } else {
                document.getElementById('profileRoleBadge').innerText = 'عضو (Member)';
            }
        }

        // اختيار ورفع الصورة بضغطة زر من الجوال وضغط حجمها لتجنب ثقل الكود
        function previewAvatar(input) {
            if (input.files && input.files[0]) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    const img = new Image();
                    img.src = e.target.result;
                    img.onload = function() {
                        const canvas = document.createElement('canvas');
                        const ctx = canvas.getContext('2d');
                        const MAX_WIDTH = 200;
                        const MAX_HEIGHT = 200;
                        let width = img.width;
                        let height = img.height;

                        if (width > height) {
                            if (width > MAX_WIDTH) { height *= MAX_WIDTH / width; width = MAX_WIDTH; }
                        } else {
                            if (height > MAX_HEIGHT) { width *= MAX_HEIGHT / height; height = MAX_HEIGHT; }
                        }
                        canvas.width = width;
                        canvas.height = height;
                        ctx.drawImage(img, 0, 0, width, height);
                        uploadedAvatarBase64 = canvas.toDataURL('image/jpeg', 0.7);
                        document.getElementById('avatarPreviewContainer').innerHTML = `<img src="${uploadedAvatarBase64}" style="width:100%; height:100%; border-radius:50%; object-fit:cover;">`;
                    };
                };
                reader.readAsDataURL(input.files[0]);
            }
        }

        async function updateProfile(e) {
            e.preventDefault();
            if (!currentUser) return;
            const btn = document.getElementById('saveProfileBtn');
            btn.disabled = true;
            btn.innerHTML = '<span>جاري الحفظ...</span> ⏳';

            const bio = document.getElementById('inputBio').value.trim();
            const track = document.getElementById('inputTrack').value;
            const portfolio_url = document.getElementById('inputPortfolio').value.trim();

            const { error } = await supabaseClient.from('profiles').update({
                bio, track, portfolio_url, avatar_url: uploadedAvatarBase64
            }).eq('id', currentUser.id);

            if (error) {
                alert('❌ تعذر حفظ التعديلات: ' + error.message);
            } else {
                alert('✅ تم حفظ التعديلات وصورتك الشخصية في بروفايلك بنجاح!');
                document.getElementById('barUserTrack').innerText = track;
            }
            btn.disabled = false;
            btn.innerHTML = '<span>حفظ التعديلات في البروفايل</span><span>💾</span>';
        }

        async function loadAdminMembers() {
            const container = document.getElementById('adminMembersList');
            const { data: members, error } = await supabaseClient.from('profiles').select('*');
            if (error || !members) {
                container.innerHTML = 'تعذر جلب الأعضاء.';
                return;
            }
            container.innerHTML = '';
            members.forEach(m => {
                const item = document.createElement('div');
                item.className = 'member-row-item';
                item.innerHTML = `
                    <div>
                        <strong>${m.full_name || 'بدون اسم'}</strong><br>
                        <span style="font-size: 0.78rem; color: var(--text-muted);">التخصص: ${m.track || 'غير محدد'} | الرتبة: ${m.role}</span>
                    </div>
                    <div style="display:flex; gap:5px; align-items:center;">
                        <select id="track_${m.id}" style="padding:4px 8px; font-size:0.8rem;">
                            <option value="تصوير وإضاءة" ${m.track==='تصوير وإضاءة'?'selected':''}>تصوير وإضاءة</option>
                            <option value="مونتاج وموشن جرافيك" ${m.track==='مونتاج وموشن جرافيك'?'selected':''}>مونتاج</option>
                            <option value="إنتاج برامج وبودكاست" ${m.track==='إنتاج برامج وبودكاست'?'selected':''}>بودكاست</option>
                            <option value="تصميم وهوية بصرية" ${m.track==='تصميم وهوية بصرية'?'selected':''}>تصميم</option>
                            <option value="كتابة وصحافة إعلامية" ${m.track==='كتابة وصحافة إعلامية'?'selected':''}>كتابة</option>
                        </select>
                        <button onclick="changeMemberTrack('${m.id}')" style="background:var(--accent-primary); border:none; color:#fff; padding:5px 10px; border-radius:6px; cursor:pointer; font-size:0.75rem;">تحديث</button>
                    </div>
                `;
                container.appendChild(item);
            });
        }

        async function changeMemberTrack(userId) {
            const newTrack = document.getElementById(`track_${userId}`).value;
            const { error } = await supabaseClient.from('profiles').update({ track: newTrack }).eq('id', userId);
            if (error) {
                alert('خطأ في التحديث');
            } else {
                alert('✅ تم نقل العضو للمسار الجديد بنجاح!');
                loadAdminMembers();
            }
        }

        async function logout() {
            await supabaseClient.auth.signOut();
            window.location.reload();
        }

        window.addEventListener('DOMContentLoaded', async () => {
            const { data: { session } } = await supabaseClient.auth.getSession();
            if (session && session.user) {
                loadUserProfile(session.user);
            }
        });

        window.switchPage = function(pageId, btnElement) {
            document.querySelectorAll('.page-section').forEach(sec => sec.classList.remove('active'));
            document.querySelectorAll('.nav-btn').forEach(btn => btn.classList.remove('active'));
            document.getElementById(pageId).classList.add('active');
            btnElement.classList.add('active');
            window.scrollTo({ top: 0, behavior: 'smooth' });

            if(pageId === 'archivePage') { loadSheetIdeas(); }
            if(pageId === 'adminPage') { loadAdminMembers(); }
        };

        function getYouTubeEmbedUrl(url) {
            if (!url) return '';
            const match = url.match(/^.*(youtu.be\/|v\/|u\/\w\/|embed\/|watch\?v=|\&v=)([^#\&\?]*).*/);
            return (match && match[2].length === 11) ? `https://www.youtube.com/embed/${match[2]}` : '';
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
                await fetch(SCRIPT_URL, { method: 'POST', mode: 'no-cors', headers: { 'Content-Type': 'application/json' }, body: JSON.stringify(data) });
                alert('✅ تم حفظ الفكرة في السحابة بنجاح!');
                this.reset();
                document.getElementById('authorName').value = document.getElementById('profileDisplayName').innerText;
                switchPage('archivePage', document.querySelectorAll('.nav-btn')[3]);
            } catch (error) {
                alert('❌ تعذر الحفظ.');
            } finally {
                submitBtn.disabled = false;
                submitBtn.innerHTML = '<span>حفظ الفكرة في السحابة</span><span>🚀</span>';
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
                container.innerHTML = ideas.length === 0 ? '<div style="text-align: center; color: var(--text-muted); padding: 20px;">لا توجد أفكار مسجلة.</div>' : '';

                ideas.reverse().forEach((idea) => {
                    const embedUrl = getYouTubeEmbedUrl(idea.videoUrl || idea.video);
                    const card = document.createElement('div');
                    card.className = 'idea-card';
                    card.innerHTML = `
                        <div class="idea-header"><div class="idea-title">${idea.title || 'بدون عنوان'}</div><div class="idea-author">المقترح: ${idea.author || 'مجهول'}</div></div>
                        <div class="idea-body">${idea.desc || idea.description || ''}</div>
                        ${idea.imageUrl || idea.image ? `<div style="margin-top: 10px;"><img src="${idea.imageUrl || idea.image}" style="width:100%; max-height:220px; object-fit:cover; border-radius:8px;" onerror="this.style.display='none'"></div>` : ''}
                        ${embedUrl ? `<div class="video-wrapper"><iframe src="${embedUrl}" allowfullscreen></iframe></div>` : ''}
                    `;
                    container.appendChild(card);
                });
            } catch (error) {
                container.innerHTML = '<div style="text-align: center; color: #f85149; padding: 20px;">تعذر جلب الأرشيف.</div>';
            }
        }
    </script>
</body>
</html>
