 # MTU
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    
    <!-- وسم إثبات الملكية لـ Google Search Console -->
    <meta name="google-site-verification" content="_tKWW0ai4kGwcfk6Vww3dS0Yr0gQhIMxOKaG0Goc7Cs" />

    <!-- وسوم الـ SEO والأرشفة في محرك بحث قوقل -->
    <title>منصة النادي الإعلامي - جامعة الطائف</title>
    <meta name="description" content="المنصة الرسمية للنادي الإعلامي بجامعة الطائف - تقديم الأفكار، الأرشيف، وإدارة الأعضاء والمسارات الإعلامية.">
    <meta name="keywords" content="النادي الإعلامي, جامعة الطائف, منصة النادي الإعلامي, MTU, Taif University">
    <meta name="author" content="خالد أحمد الهلال">

    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700;800;900&family=Montserrat:wght@800;900&display=swap" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>
    <style>
        :root {
            --bg-dark: #07070a;
            --bg-deep: #030305;
            --bg-card: rgba(15, 17, 26, 0.94);
            --bg-card-solid: #10121a;
            --accent-primary: #3b82f6;
            --accent-glow: #60a5fa;
            --text-main: #f8fafc;
            --text-muted: #94a3b8;
            --border: rgba(255, 255, 255, 0.12);
            --input-bg: rgba(8, 10, 18, 0.85);
            --brand-red: #ff4d2d;
            --admin-color: #238636;
            --board-color: #8b5cf6;
        }

        * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Cairo', sans-serif; -webkit-tap-highlight-color: transparent; }

        body {
            background-color: var(--bg-dark); color: var(--text-main); line-height: 1.7; padding-bottom: 40px; min-height: 100vh; overflow-x: hidden; width: 100%; position: relative;
        }

        .bg-video-container {
            position: fixed; top: 0; left: 0; width: 100vw; height: 100vh; z-index: -99; overflow: hidden; pointer-events: none; background: #000;
        }
        .bg-video-container video {
            position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%); min-width: 100%; min-height: 100%; width: auto; height: auto; object-fit: cover;
            filter: brightness(0.5) contrast(1.1);
        }
        .bg-overlay {
            position: fixed; top: 0; left: 0; width: 100vw; height: 100vh; background: rgba(5, 5, 7, 0.7); z-index: -98; pointer-events: none;
        }

        #welcomeScreen {
            position: fixed; inset: 0; z-index: 999999; 
            background: radial-gradient(circle at 20% 20%, rgba(59, 130, 246, 0.18) 0%, transparent 40%),
                        radial-gradient(circle at 80% 80%, rgba(255, 77, 45, 0.15) 0%, transparent 40%),
                        radial-gradient(circle at 50% 50%, rgba(139, 92, 246, 0.12) 0%, transparent 60%),
                        #05060a;
            display: flex; flex-direction: column; align-items: center; justify-content: center; padding: 20px; text-align: center; transition: all 0.5s cubic-bezier(0.4, 0, 0.2, 1); overflow-y: auto;
        }

        .auth-card {
            position: relative; z-index: 2;
            background: rgba(16, 18, 27, 0.85); 
            border: 1px solid rgba(255, 255, 255, 0.15); 
            backdrop-filter: blur(20px); -webkit-backdrop-filter: blur(20px);
            border-radius: 20px; padding: 32px 24px; width: 100%; max-width: 440px; 
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.8), 0 0 30px rgba(59, 130, 246, 0.15); 
            margin-top: 15px; text-align: right;
        }

        .mtu-logo-container { display: inline-flex; align-items: center; justify-content: center; margin-bottom: 8px; position: relative; }
        .mtu-logo-text { font-family: 'Montserrat', sans-serif; font-size: 3.2rem; font-weight: 900; letter-spacing: -1px; color: #ffffff; line-height: 1; display: flex; align-items: flex-start; position: relative; text-shadow: 0 0 20px rgba(255,255,255,0.2); }
        .mtu-dot { width: 14px; height: 14px; background-color: var(--brand-red); border-radius: 50%; display: inline-block; margin-left: 2px; margin-top: 2px; box-shadow: 0 0 15px rgba(255, 77, 45, 0.9); }

        .quick-nav {
            position: sticky; top: 0; z-index: 1000; background: rgba(15, 15, 20, 0.85); backdrop-filter: blur(12px); border-bottom: 1px solid var(--border); padding: 10px 12px; display: flex; justify-content: center; gap: 6px; width: 100%; flex-wrap: wrap;
        }

        .nav-btn {
            background: rgba(255, 255, 255, 0.05); color: var(--text-main); border: 1px solid var(--border); padding: 8px 12px; border-radius: 20px; font-size: 0.78rem; font-weight: 700; cursor: pointer; transition: all 0.3s ease; display: inline-flex; align-items: center; justify-content: center; gap: 5px; text-align: center; white-space: nowrap;
        }

        .nav-btn:hover, .nav-btn.active {
            background: var(--accent-primary); color: #ffffff; border-color: var(--accent-glow); transform: translateY(-2px); box-shadow: 0 4px 15px rgba(59, 130, 246, 0.4);
        }

        header { position: relative; text-align: center; padding: 25px 15px 15px; background: rgba(18, 18, 24, 0.65); border-bottom: 1px solid var(--border); backdrop-filter: blur(12px); }
        .site-badge { background: rgba(59, 130, 246, 0.15); color: var(--accent-glow); padding: 6px 20px; border-radius: 30px; font-size: 0.9rem; font-weight: 700; display: inline-block; border: 1px solid rgba(59, 130, 246, 0.3); }

        .container { max-width: 950px; margin: 20px auto; padding: 0 12px; width: 100%; }
        .page-section { display: none; }
        .page-section.active { display: block; }

        .card { background: var(--bg-card); border: 1px solid var(--border); backdrop-filter: blur(12px); border-radius: 14px; padding: 18px 14px; margin-bottom: 20px; box-shadow: 0 10px 30px -10px rgba(0, 0, 0, 0.8); }
        .section-title { font-size: 1.15rem; font-weight: 800; margin-bottom: 16px; display: flex; align-items: center; gap: 10px; color: var(--text-main); }
        .section-title span.icon { background: var(--accent-primary); color: #ffffff; width: 30px; height: 30px; border-radius: 8px; display: inline-flex; align-items: center; justify-content: center; }

        .stats-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(180px, 1fr)); gap: 12px; margin-bottom: 20px; }
        .stat-card { background: rgba(255,255,255,0.03); border: 1px solid var(--border); padding: 15px; border-radius: 12px; text-align: center; }
        .stat-num { font-size: 1.8rem; font-weight: 900; color: var(--accent-glow); margin-top: 5px; }
        .stat-label { font-size: 0.8rem; color: var(--text-muted); font-weight: 700; }

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
        @media (min-width: 600px) { .form-row { grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); } }
        .form-group { margin-bottom: 14px; text-align: right; }
        label { display: block; margin-bottom: 5px; font-weight: 700; color: #cbd5e1; font-size: 0.85rem; }
        input, textarea, select { width: 100%; padding: 11px 14px; background-color: var(--input-bg); border: 1px solid var(--border); border-radius: 10px; color: var(--text-main); font-size: 0.9rem; outline: none; transition: border-color 0.3s ease; }
        input:focus, select:focus, textarea:focus { border-color: var(--accent-glow); box-shadow: 0 0 10px rgba(96, 165, 250, 0.2); }
        
        button.btn-submit { background: linear-gradient(135deg, var(--accent-primary), #2563eb); color: #ffffff; font-weight: 800; font-size: 0.95rem; padding: 12px 20px; border: none; border-radius: 10px; cursor: pointer; width: 100%; display: flex; align-items: center; justify-content: center; gap: 8px; box-shadow: 0 4px 15px rgba(37, 99, 235, 0.35); }

        .member-row-item { background: rgba(255,255,255,0.03); border: 1px solid var(--border); padding: 12px; border-radius: 8px; margin-bottom: 8px; display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 10px; }

        .archive-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 15px; flex-wrap: wrap; gap: 10px; }
        .archive-counter { background: rgba(59, 130, 246, 0.15); color: var(--accent-glow); padding: 4px 12px; border-radius: 16px; font-size: 0.78rem; font-weight: 700; border: 1px solid rgba(59, 130, 246, 0.3); }
        .archive-grid { display: flex; flex-direction: column; gap: 15px; }
        .idea-card { background: var(--bg-card-solid); border: 1px solid var(--border); border-radius: 12px; padding: 16px; position: relative; }
        .idea-header { display: flex; justify-content: space-between; margin-bottom: 8px; flex-wrap: wrap; gap: 6px; align-items: center; }
        .idea-title { font-size: 1.05rem; font-weight: 800; color: #fff; }
        .idea-author { font-size: 0.75rem; color: var(--accent-glow); background: rgba(59, 130, 246, 0.12); padding: 2px 10px; border-radius: 15px; }
        .idea-body { color: #cbd5e1; font-size: 0.88rem; margin-bottom: 12px; }
        .idea-details-meta { display: flex; gap: 12px; font-size: 0.78rem; color: var(--text-muted); background: rgba(255,255,255,0.02); padding: 8px 12px; border-radius: 8px; margin-bottom: 10px; flex-wrap: wrap; }
        .status-badge { font-size: 0.72rem; padding: 3px 8px; border-radius: 6px; font-weight: 700; }
        .status-pending { background: rgba(245, 158, 11, 0.15); color: #fbbf24; border: 1px solid rgba(245, 158, 11, 0.3); }
        .status-approved { background: rgba(34, 197, 94, 0.15); color: #4ade80; border: 1px solid rgba(34, 197, 94, 0.3); }

        .albums-bar { display: flex; gap: 8px; overflow-x: auto; padding-bottom: 10px; margin-bottom: 15px; }
        .album-chip { background: rgba(255,255,255,0.05); border: 1px solid var(--border); color: var(--text-muted); padding: 6px 14px; border-radius: 20px; font-size: 0.8rem; font-weight: 700; cursor: pointer; white-space: nowrap; transition: 0.2s; }
        .album-chip.active, .album-chip:hover { background: var(--accent-primary); color: #fff; border-color: var(--accent-glow); }

        .gallery-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(180px, 1fr)); gap: 15px; margin-top: 15px; }
        .gallery-item { background: var(--bg-card-solid); border: 1px solid var(--border); border-radius: 10px; overflow: hidden; transition: transform 0.3s ease; position: relative; }
        .gallery-item:hover { transform: translateY(-4px); border-color: var(--accent-primary); }
        .gallery-item img { width: 100%; height: 160px; object-fit: cover; display: block; }
        .delete-img-btn { position: absolute; top: 6px; left: 6px; background: rgba(248,81,73,0.8); color: #fff; border: none; width: 26px; height: 26px; border-radius: 50%; cursor: pointer; font-size: 0.75rem; display: flex; align-items: center; justify-content: center; }

        .like-btn { background: rgba(255,255,255,0.05); border: 1px solid var(--border); color: #fff; padding: 4px 12px; border-radius: 20px; font-size: 0.8rem; cursor: pointer; transition: 0.2s ease; display: inline-flex; align-items: center; gap: 5px; }
        .like-btn:hover { background: rgba(59,130,246,0.2); border-color: var(--accent-primary); }

        .video-wrapper { position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; border-radius: 8px; margin-top: 10px; }
        .video-wrapper iframe { position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: none; }
        .auth-switch { text-align: center; margin-top: 14px; font-size: 0.85rem; color: var(--text-muted); display: flex; flex-direction: column; gap: 8px; }
        .auth-switch a { color: var(--accent-glow); cursor: pointer; font-weight: 700; }
        .error-msg { color: #f85149; font-size: 0.8rem; text-align: center; margin-top: 8px; }
        footer { text-align: center; color: var(--text-muted); font-size: 0.8rem; padding-top: 20px; border-top: 1px solid var(--border); margin-top: 25px; }

        #clubRegModal {
            position: fixed; inset: 0; z-index: 9999999; 
            background: rgba(3, 4, 8, 0.92); backdrop-filter: blur(15px); 
            display: flex; flex-direction: column; align-items: center; justify-content: center; padding: 20px; text-align: center;
        }

        #customSuccessModal {
            position: fixed; inset: 0; z-index: 99999999;
            background: rgba(3, 4, 8, 0.85); backdrop-filter: blur(12px); -webkit-backdrop-filter: blur(12px);
            display: none; align-items: center; justify-content: center; padding: 20px;
            animation: fadeInModal 0.3s cubic-bezier(0.16, 1, 0.3, 1);
        }
        @keyframes fadeInModal {
            from { opacity: 0; transform: scale(0.92); }
            to { opacity: 1; transform: scale(1); }
        }
        .modal-card {
            background: rgba(16, 18, 27, 0.95); border: 1px solid rgba(59, 130, 246, 0.3);
            border-radius: 20px; padding: 30px 24px; text-align: center; max-width: 380px; width: 100%;
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.8), 0 0 30px rgba(34, 197, 94, 0.2);
        }
        .success-circle-icon {
            width: 70px; height: 70px; background: rgba(34, 197, 94, 0.15); border: 2px solid #22c55e;
            color: #22c55e; border-radius: 50%; display: flex; align-items: center; justify-content: center;
            font-size: 2.2rem; margin: 0 auto 16px; box-shadow: 0 0 20px rgba(34, 197, 94, 0.4);
        }
        .modal-title { font-size: 1.2rem; font-weight: 800; color: #fff; margin-bottom: 8px; }
        .modal-desc { font-size: 0.9rem; color: var(--text-muted); margin-bottom: 20px; line-height: 1.5; }
        .modal-close-btn {
            background: linear-gradient(135deg, var(--accent-primary), #2563eb);
            color: #fff; border: none; padding: 10px 24px; border-radius: 12px; font-weight: 800;
            font-size: 0.9rem; cursor: pointer; width: 100%; transition: 0.2s ease;
        }
        .modal-close-btn:hover { transform: translateY(-2px); box-shadow: 0 4px 15px rgba(59, 130, 246, 0.4); }
    </style>
</head>
<body>

    <div class="bg-video-container">
        <video autoplay loop muted playsinline preload="auto">
            <source src="background.mp4" type="video/mp4">
            <source src="https://assets.mixkit.co/videos/preview/mixkit-abstract-technology-mesh-network-30230-large.mp4" type="video/mp4">
        </video>
    </div>
    <div class="bg-overlay"></div>

    <div id="customSuccessModal">
        <div class="modal-card">
            <div class="success-circle-icon" id="modalIcon">✓</div>
            <div class="modal-title" id="modalTitle">تمت العملية بنجاح!</div>
            <div class="modal-desc" id="modalDesc">تم رفع البيانات وتحديث المنصة بنجاح.</div>
            <button class="modal-close-btn" onclick="closeSuccessModal()">موافق</button>
        </div>
    </div>

    <div id="welcomeScreen">
        <div class="mtu-logo-container"><div class="mtu-logo-text">MTU<span class="mtu-dot"></span></div></div>
        <span class="site-badge" style="margin-top: 4px; background: rgba(59, 130, 246, 0.2);">منصة النادي الإعلامي</span>
        <h1 id="authMainTitle" style="font-size: 1.25rem; margin-top: 12px; color: #fff; font-weight: 800;">تسجيل الدخول للمنصة</h1>
        
        <div class="auth-card">
            <form id="authForm" onsubmit="handleSupabaseAuth(event)">
                <div class="form-group" id="fullNameGroup" style="display: none;">
                    <label>الاسم الرباعي:</label>
                    <input type="text" id="authFullName" placeholder="اكتب اسمك الرباعي هنا" oninput="checkBoardIdentity(this.value)">
                    <div id="boardNotice" style="display: none; font-size: 0.8rem; color: #8b5cf6; margin-top: 5px; font-weight: bold; background: rgba(139, 92, 246, 0.15); padding: 6px 10px; border-radius: 6px; border: 1px solid rgba(139, 92, 246, 0.3);">
                        🌟 أهلاً بك! تطابق اسمك مع الهيكلة الإدارية، وتم إعفاؤك من المسارات.
                    </div>
                </div>
                
                <div class="form-group" id="phoneGroup" style="display: none;">
                    <label>رقم الجوال:</label>
                    <input type="tel" id="authPhone" placeholder="05XXXXXXXX">
                </div>

                <div class="form-group" id="trackGroup" style="display: none;">
                    <label>اختر مسارك الرئيسي في النادي:</label>
                    <select id="authTrack">
                        <option value="تصوير وإضاءة">📷 تصوير وإضاءة</option>
                        <option value="مونتاج وموشن جرافيك">🎬 مونتاج وموشن جرافيك</option>
                        <option value="إنتاج برامج وبودكاست">🎙️ إنتاج برامج وبودكاست</option>
                        <option value="تصميم وهوية بصرية">🎨 تصميم وهوية بصرية</option>
                        <option value="كتابة وصحافة إعلامية">✍️ كتابة وصحافة إعلامية</option>
                        <option value="تقنية المعلومات (IT)">💻 تقنية المعلومات (IT)</option>
                    </select>
                </div>
                <div class="form-group"><label>البريد الإلكتروني:</label><input type="email" id="authEmail" placeholder="name@example.com" required></div>
                <div class="form-group"><label>كلمة المرور:</label><input type="password" id="authPassword" placeholder="••••••••" required></div>
                <button type="submit" class="btn-submit" id="authBtn"><span id="authBtnText">دخول المنصة</span><span>🚀</span></button>
                <div id="authError" class="error-msg"></div>
            </form>

            <div class="auth-switch">
                <div><span id="switchText">ليس لديك حساب على المنصة؟</span> <a onclick="toggleAuthMode()" id="switchLink">إنشاء حساب جديد</a></div>
                <hr style="border: 0; border-top: 1px solid var(--border); margin: 8px 0;">
                <div>
                    <button type="button" onclick="openClubRegisterModal()" style="background: rgba(59, 130, 246, 0.15); border: 1px solid var(--accent-primary); color: var(--accent-glow); padding: 10px 15px; border-radius: 10px; width: 100%; font-weight: 700; cursor: pointer; font-size: 0.85rem; display: flex; align-items: center; justify-content: center; gap: 6px;">
                        <span>📝 التسجيل في النادي الإعلامي (طلب عضوية)</span>
                    </button>
                </div>
            </div>
        </div>
    </div>

    <div id="clubRegModal" style="display: none;">
        <div class="mtu-logo-container"><div class="mtu-logo-text">MTU<span class="mtu-dot"></span></div></div>
        <span class="site-badge" style="margin-top: 5px;">استمارة طلب انضمام للنادي الإعلامي</span>
        
        <div class="auth-card" style="max-width: 500px; max-height: 85vh; overflow-y: auto;">
            <form id="clubRegisterForm" onsubmit="submitClubRegistration(event)">
                <div class="form-group">
                    <label>الاسم الرباعي:</label>
                    <input type="text" id="regFullName" placeholder="الاسم الرباعي كما هو معتمد" required>
                </div>
                <div class="form-row">
                    <div class="form-group">
                        <label>البريد الجامعي:</label>
                        <input type="email" id="regUnivEmail" placeholder="sXXXXX@tu.edu.sa" required>
                    </div>
                    <div class="form-group">
                        <label>الرقم الجامعي:</label>
                        <input type="text" id="regUnivId" placeholder="44XXXXXXXX" required>
                    </div>
                </div>
                <div class="form-row">
                    <div class="form-group">
                        <label>رقم الجوال:</label>
                        <input type="tel" id="regPhone" placeholder="05XXXXXXXX" required>
                    </div>
                    <div class="form-group">
                        <label>اختر مسارك المفضل:</label>
                        <select id="regTrack">
                            <option value="تصوير وإضاءة">📷 تصوير وإضاءة</option>
                            <option value="مونتاج وموشن جرافيك">🎬 مونتاج وموشن جرافيك</option>
                            <option value="إنتاج برامج وبودكاست">🎙️ إنتاج برامج وبودكاست</option>
                            <option value="تصميم وهوية بصرية">🎨 تصميم وهوية بصرية</option>
                            <option value="كتابة وصحافة إعلامية">✍️ كتابة وصحافة إعلامية</option>
                            <option value="تقنية المعلومات (IT)">💻 تقنية المعلومات (IT)</option>
                        </select>
                    </div>
                </div>
                <div class="form-group">
                    <label>نبذة عنك (مهاراتك واهتماماتك):</label>
                    <textarea id="regBio" placeholder="اكتب نبذة مختصرة عن شغفك..." rows="3" required></textarea>
                </div>
                <div style="display: flex; gap: 10px;">
                    <button type="submit" class="btn-submit" id="regSubmitBtn" style="flex: 2;"><span>إرسال طلب الانضمام</span><span>📩</span></button>
                    <button type="button" onclick="closeClubRegisterModal()" style="background: rgba(248,81,73,0.2); border: 1px solid rgba(248,81,73,0.4); color: #f85149; border-radius: 8px; padding: 10px 15px; font-weight: 700; cursor: pointer; flex: 1;">إلغاء</button>
                </div>
                <div id="regError" class="error-msg"></div>
            </form>
        </div>
    </div>

    <!-- شريط التنقل العلوي مع زر المساعد الذكي المضاف -->
    <nav class="quick-nav">
        <button class="nav-btn active" onclick="switchPage('homePage', this)">🏛️ المجلس</button>
        <button class="nav-btn" onclick="switchPage('profilePage', this)">👤 بروفايلي</button>
        <button class="nav-btn" onclick="switchPage('formPage', this)">💡 تقديم فكرة</button>
        <button class="nav-btn" onclick="switchPage('archivePage', this)">📁 الأرشيف</button>
        <button class="nav-btn" onclick="switchPage('galleryPage', this)">🖼️ معرض الصور</button>
        <button class="nav-btn" onclick="switchPage('aiAssistantPage', this)">🤖 المساعد الذكي</button>
        <button class="nav-btn" id="adminNavBtn" style="display: none; background: rgba(35, 134, 54, 0.2); border-color: var(--admin-color);" onclick="switchPage('adminPage', this)">⚙️ المشرف</button>
        <button class="nav-btn" onclick="logout()" style="background: rgba(248, 81, 73, 0.15); border-color: rgba(248, 81, 73, 0.3); color: #f85149;">🚪 خروج</button>
    </nav>

    <header>
        <div class="mtu-logo-container" style="margin-bottom: 3px;"><div class="mtu-logo-text" style="font-size: 2.2rem;">MTU<span class="mtu-dot" style="width: 10px; height: 10px;"></span></div></div>
        <br><span class="site-badge">النادي الإعلامي</span>
    </header>

    <div class="container">

        <div class="card" style="padding: 12px 20px; display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 10px;">
            <div>👤 أهلاً بك: <strong id="barUserName" style="color: var(--accent-glow);">...</strong></div>
            <div>المسار: <span id="barUserTrack" style="background: rgba(59,130,246,0.15); padding: 2px 10px; border-radius: 10px; border: 1px solid rgba(59,130,246,0.3);">عضو</span></div>
            <div>الرتبة: <span id="barUserRole" style="background: rgba(35,134,54,0.15); padding: 2px 10px; border-radius: 10px; color: #4ade80;">عضو</span></div>
        </div>

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

        <!-- صفحة معرض الصور -->
        <section id="galleryPage" class="page-section">
            <div class="card">
                <h2 class="section-title"><span class="icon">🖼️</span>معرض صور فعاليات النادي</h2>
                
                <div style="background: rgba(255,255,255,0.03); border: 1px solid var(--border); padding: 15px; border-radius: 12px; margin-bottom: 20px;">
                    <h3 style="font-size: 0.95rem; margin-bottom: 12px; color: var(--accent-glow);">➕ إدارة المعرض (رفع جماعي وإنشاء ألبومات):</h3>
                    
                    <div class="form-row" style="margin-bottom: 10px;">
                        <div class="form-group">
                            <label>إنشاء ألبوم / مجلد جديد:</label>
                            <div style="display: flex; gap: 8px;">
                                <input type="text" id="newAlbumName" placeholder="مثال: ورشة التصوير 2026">
                                <button type="button" onclick="createNewAlbum()" style="background: var(--accent-primary); border: none; color: #fff; padding: 0 15px; border-radius: 8px; font-weight: 700; cursor: pointer; white-space: nowrap;">إنشاء</button>
                            </div>
                        </div>
                        <div class="form-group">
                            <label>اختر الألبوم المستهدف:</label>
                            <select id="targetAlbumSelect">
                                <option value="الفعاليات العامة">الفعاليات العامة (افتراضي)</option>
                            </select>
                        </div>
                    </div>

                    <form id="uploadGalleryForm" onsubmit="uploadMultipleGalleryImages(event)">
                        <div class="form-row">
                            <div class="form-group" style="grid-column: 1 / -1;">
                                <label>اختر صور متعددة من الجهاز (حفظ دائم في سوبابيس):</label>
                                <input type="file" id="galleryImageFiles" accept="image/*" multiple required style="padding: 8px;">
                            </div>
                        </div>
                        <button type="submit" class="btn-submit" id="uploadGalleryBtn"><span>رفع وحفظ الصور المحددة</span><span>🚀</span></button>
                    </form>
                </div>

                <div class="albums-bar" id="albumsBarContainer">
                    <div class="album-chip active" onclick="filterGalleryByAlbum('الكل', this)">📁 الكل</div>
                </div>
                
                <div class="gallery-grid" id="dynamicGalleryContainer">
                    <div style="text-align: center; color: var(--text-muted); grid-column: 1 / -1; padding: 20px;">جاري جلب الصور المحفوظة...</div>
                </div>
            </div>
        </section>

        <!-- صفحة المساعد الذكي المستقلة الكبيرة الجديدة -->
        <section id="aiAssistantPage" class="page-section">
            <div class="card" style="padding: 24px; min-height: 75vh; display: flex; flex-direction: column;">
                <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 15px; flex-wrap: wrap; gap: 10px;">
                    <h2 class="section-title" style="margin-bottom: 0;"><span class="icon">🤖</span>مساعد الذكاء الاصطناعي - النادي الإعلامي</h2>
                    <div style="display: flex; gap: 8px; align-items: center;">
                        <button type="button" id="voiceToggleBtn" onclick="toggleVoiceOutput()" style="background: rgba(59,130,246,0.15); border: 1px solid var(--accent-primary); color: var(--accent-glow); padding: 6px 14px; border-radius: 20px; font-size: 0.8rem; font-weight: 700; cursor: pointer; display: flex; align-items: center; gap: 5px;">
                            🔊 الصوت: <span id="voiceStatusText">مفعل (صوت واضح وفصيح)</span>
                        </button>
                    </div>
                </div>

                <p style="color: var(--text-muted); font-size: 0.85rem; margin-bottom: 15px;">
                    مساعدك الذكي لتطوير الأفكار، مراجعة التقارير، والدعم الفني للمنصة. تحدث بالميكروفون أو اكتب وسأتفاعل معك بشكل حقيقي وفوري!
                </p>

                <!-- أزرار الخدمات السريعة -->
                <div style="display: flex; gap: 8px; overflow-x: auto; padding-bottom: 10px; margin-bottom: 15px;">
                    <button class="nav-btn" onclick="setAiPrompt('اقترح علي فكرة إعلامية مميزة:')">💡 اقتراح فكرة</button>
                    <button class="nav-btn" onclick="setAiPrompt('ساعدني في كتابة تقرير عن:')">📝 كتابة تقرير</button>
                    <button class="nav-btn" onclick="setAiPrompt('عندي مشكلة أو دعم فني في:')">🛠️ دعم فني</button>
                    <button class="nav-btn" onclick="setAiPrompt('كيف حالك وماذا تفعل الآن؟')">👋 محادثة ودية</button>
                </div>

                <!-- صندوق المحادثة الواسع -->
                <div id="aiChatContainer" style="flex: 1; background: rgba(5,6,10,0.6); border: 1px solid var(--border); border-radius: 12px; padding: 15px; height: 420px; overflow-y: auto; display: flex; flex-direction: column; gap: 12px; margin-bottom: 15px;">
                    <div style="background: rgba(59,130,246,0.1); border: 1px solid rgba(59,130,246,0.2); padding: 12px; border-radius: 10px; max-width: 85%; align-self: flex-start; color: #fff; font-size: 0.9rem;">
                        أهلاً بك يا خالد! أنا مساعدك الذكي في منصة النادي الإعلامي بجامعة الطائف. تفضل بطرح أي سؤال أو فكرة وسأجيبك فوراً صوتياً وكتابياً! 🎙️✨
                    </div>
                </div>

                <!-- شريط الإدخال والتحكم الصوتي -->
                <form id="aiChatForm" onsubmit="sendAiMessage(event)" style="display: flex; gap: 10px; align-items: center;">
                    <button type="button" id="micBtn" onclick="toggleSpeechRecognition()" title="التحدث الصوتي المباشر" style="background: rgba(255,255,255,0.05); border: 1px solid var(--border); color: #fff; width: 45px; height: 45px; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 1.2rem; cursor: pointer; transition: 0.3s;">
                        🎙️
                    </button>
                    <input type="text" id="aiInputMessage" placeholder="اكتب رسالتك أو اضغط الميكروفون للتحدث..." style="flex: 1; padding: 12px 16px; border-radius: 12px;">
                    <button type="submit" class="btn-submit" style="width: auto; padding: 12px 22px; border-radius: 12px;">إرسال 🚀</button>
                </form>
            </div>
        </section>

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
                                <option value="تقنية المعلومات (IT)">💻 تقنية المعلومات (IT)</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label>رقم الجوال:</label>
                            <input type="tel" id="inputPhone" placeholder="05XXXXXXXX">
                        </div>
                    </div>
                    <div class="form-group">
                        <label>رابط معرض الأعمال (Portfolio / GitHub):</label>
                        <input type="url" id="inputPortfolio" placeholder="https://github.com/username">
                    </div>
                    <button type="submit" class="btn-submit" id="saveProfileBtn"><span>حفظ التعديلات في البروفايل</span><span>💾</span></button>
                </form>
            </div>
        </section>

        <section id="formPage" class="page-section">
            <div class="card">
                <h2 class="section-title"><span class="icon">💡</span>تقديم فكرة / مشروع جديد</h2>
                <form id="ideaForm" onsubmit="submitIdeaToSupabase(event)">
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
                        <div class="form-group">
                            <label>صورة توضيحية للفكرة (اختر ملف من الجوال):</label>
                            <input type="file" id="ideaImageFile" accept="image/*" style="padding: 8px;">
                        </div>
                        <div class="form-group"><label>رابط فيديو يوتيوب (اختياري):</label><input type="url" id="videoUrl" placeholder="https://youtube.com/..."></div>
                    </div>
                    <button type="submit" class="btn-submit" id="submitBtn"><span>حفظ الفكرة في السحابة</span><span>🚀</span></button>
                </form>
            </div>
        </section>

        <section id="archivePage" class="page-section">
            <div class="archive-header">
                <h2 class="section-title" style="margin-bottom: 0;"><span class="icon">📁</span>أرشيف الفعاليات والمشاريع</h2>
                <span class="archive-counter" id="archiveCount">جاري التحميل...</span>
            </div>

            <div style="margin-bottom: 15px;">
                <input type="text" id="searchIdeaInput" oninput="filterIdeasArchive()" placeholder="🔍 ابحث في الأفكار..." style="background: rgba(15, 17, 26, 0.9); border-color: var(--border);">
            </div>

            <div class="archive-grid" id="archiveContainer"></div>
        </section>

        <section id="adminPage" class="page-section">
            <div class="card">
                <h2 class="section-title"><span class="icon">⚙️</span>لوحة تحكم المشرف وإدارة الأعضاء</h2>
                
                <div class="stats-grid">
                    <div class="stat-card">
                        <div class="stat-label">👥 إجمالي الأعضاء</div>
                        <div class="stat-num" id="statTotalMembers">0</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-label">💡 الأفكار والمشاريع</div>
                        <div class="stat-num" id="statTotalIdeas">0</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-label">🔥 المسار الأكثر طلباً</div>
                        <div class="stat-num" id="statTopTrack" style="font-size: 1.1rem; margin-top: 10px;">...</div>
                    </div>
                </div>

                <div style="background: rgba(255,255,255,0.03); border: 1px solid var(--border); padding: 15px; border-radius: 12px; margin-bottom: 20px;">
                    <h3 style="font-size: 0.95rem; margin-bottom: 10px; color: var(--accent-glow);">📱 إرسال SMS / تنبيه للاجتماع بضغطة زر:</h3>
                    <div class="form-row" style="margin-bottom: 10px;">
                        <div class="form-group">
                            <label>حدد المسار المستهدف بالرسالة:</label>
                            <select id="smsTargetTrack">
                                <option value="جميع المسارات">🌐 جميع المسارات والأعضاء</option>
                                <option value="تصوير وإضاءة">📷 تصوير وإضاءة</option>
                                <option value="مونتاج وموشن جرافيك">🎬 مونتاج وموشن جرافيك</option>
                                <option value="إنتاج برامج وبودكاست">🎙️ إنتاج برامج وبودكاست</option>
                                <option value="تصميم وهوية بصرية">🎨 تصميم وهوية بصرية</option>
                                <option value="كتابة وصحافة إعلامية">✍️ كتابة وصحافة إعلامية</option>
                                <option value="تقنية المعلومات (IT)">💻 تقنية المعلومات (IT)</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label>نص الرسالة (دعوة اجتماع / تنبيه):</label>
                            <input type="text" id="smsMessageText" placeholder="مثال: يرجى حضور اجتماع النادي اليوم...">
                        </div>
                    </div>
                    <div style="display: flex; gap: 10px; flex-wrap: wrap;">
                        <button onclick="sendGroupSMS()" style="background: linear-gradient(135deg, #10b981, #059669); color: #fff; border: none; padding: 10px 18px; border-radius: 8px; font-weight: 800; cursor: pointer; flex: 1;">📱 إرسال SMS جماعي</button>
                        <button onclick="exportMembersToExcel()" style="background: rgba(59, 130, 246, 0.2); border: 1px solid var(--accent-primary); color: var(--accent-glow); padding: 10px 18px; border-radius: 8px; font-weight: 800; cursor: pointer;">📊 تصدير لـ Excel</button>
                    </div>
                </div>

                <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 12px; flex-wrap: wrap; gap: 10px;">
                    <h3 style="font-size: 1rem; color: #fff;">قائمة أعضاء النادي المسجلين:</h3>
                    <select id="filterTrackSelect" onchange="filterMembersList()" style="width: auto; padding: 6px 10px; font-size: 0.82rem;">
                        <option value="الكل">كل المسارات</option>
                        <option value="تصوير وإضاءة">تصوير وإضاءة</option>
                        <option value="مونتاج وموشن جرافيك">مونتاج</option>
                        <option value="إنتاج برامج وبودكاست">بودكاست</option>
                        <option value="تصميم وهوية بصرية">تصميم</option>
                        <option value="كتابة وصحافة إعلامية">كتابة</option>
                        <option value="تقنية المعلومات (IT)">IT</option>
                        <option value="مشرف المنصة">مشرف المنصة</option>
                    </select>
                </div>

                <div id="adminMembersList">جاري جلب الأعضاء...</div>
            </div>
        </section>

        <footer>النادي الإعلامي (MTU) ©️ 2026 | Media Club</footer>
    </div>

    <script>
        const SUPABASE_URL = 'https://hlgvjdknxtywdqjikayz.supabase.co';
        const SUPABASE_ANON_KEY = 'sb_publishable_xw3iN_Cb5eFA125MyBx8TQ_3aTyXjqr';
        const supabaseClient = supabase.createClient(SUPABASE_URL, SUPABASE_ANON_KEY);
        
        const ADMIN_NAMES = ["خالد الهلال", "خالد أحمد الهلال", "حمزه فرج", "حمزة فرج", "د. حمزه فرج", "د. حمزة فرج", "عبدالرحمن الزهراني", "عبدالرحمن علي الزهراني", "ماجد الشاطري"];
        const BOARD_NAMES = ["نواف المالكي", "نواف عبد الله المالكي", "حمد الحارثي", "حمد عايض الحارثي", "عبدالله السواط", "عبد الله مزيد السواط", "عبدالرحمن العتيبي", "عبد الرحمن نجم العتيبي"];

        let currentUser = null;
        let isRegisterMode = false;
        let uploadedAvatarBase64 = '';
        let allMembersData = [];
        let allIdeasData = [];
        let galleryData = [];
        let albumsList = ["الفعاليات العامة"];
        let currentSelectedAlbum = "الكل";

        function showSuccessModal(title, message, icon = '✓') {
            document.getElementById('modalIcon').innerText = icon;
            document.getElementById('modalTitle').innerText = title;
            document.getElementById('modalDesc').innerText = message;
            document.getElementById('customSuccessModal').style.display = 'flex';
        }

        function closeSuccessModal() {
            document.getElementById('customSuccessModal').style.display = 'none';
        }

        function createNewAlbum() {
            const input = document.getElementById('newAlbumName');
            const albumName = input.value.trim();
            if (!albumName) { showSuccessModal('تنبيه', 'يرجى كتابة اسم الألبوم أولاً.', '⚠️'); return; }
            if (albumsList.includes(albumName)) { showSuccessModal('تنبيه', 'هذا الألبوم موجود مسبقاً.', '⚠️'); return; }

            albumsList.push(albumName);
            input.value = '';
            updateAlbumsUI();
            showSuccessModal('تم بنجاح', `تم إنشاء ألبوم "${albumName}" بنجاح!`, '📁');
        }

        function updateAlbumsUI() {
            const selectEl = document.getElementById('targetAlbumSelect');
            const barEl = document.getElementById('albumsBarContainer');
            
            selectEl.innerHTML = '<option value="الفعاليات العامة">الفعاليات العامة (افتراضي)</option>';
            albumsList.forEach(album => {
                if(album !== "الفعاليات العامة") {
                    selectEl.innerHTML += `<option value="${album}">${album}</option>`;
                }
            });

            barEl.innerHTML = `<div class="album-chip ${currentSelectedAlbum==='الكل'?'active':''}" onclick="filterGalleryByAlbum('الكل', this)">📁 الكل</div>`;
            albumsList.forEach(album => {
                barEl.innerHTML += `<div class="album-chip ${currentSelectedAlbum===album?'active':''}" onclick="filterGalleryByAlbum('${album}', this)">📁 ${album}</div>`;
            });
        }

        async function loadGalleryFromSupabase() {
            const container = document.getElementById('dynamicGalleryContainer');
            try {
                const { data, error } = await supabaseClient.from('gallery').select('*');
                if (error) throw error;
                galleryData = data || [];
                
                galleryData.forEach(item => {
                    if (item.album && !albumsList.includes(item.album)) {
                        albumsList.push(item.album);
                    }
                });
                updateAlbumsUI();
                renderGalleryGrid(galleryData);
            } catch (err) {
                container.innerHTML = '<div style="text-align: center; color: var(--text-muted); grid-column: 1 / -1; padding: 20px;">لا توجد صور محفوظة بعد.</div>';
            }
        }

        function renderGalleryGrid(items) {
            const container = document.getElementById('dynamicGalleryContainer');
            container.innerHTML = '';
            
            const filtered = currentSelectedAlbum === 'الكل' ? items : items.filter(i => i.album === currentSelectedAlbum);

            if (filtered.length === 0) {
                container.innerHTML = '<div style="text-align: center; color: var(--text-muted); grid-column: 1 / -1; padding: 20px;">لا توجد صور في هذا الألبوم.</div>';
                return;
            }

            filtered.forEach(item => {
                const card = document.createElement('div');
                card.className = 'gallery-item';
                card.innerHTML = `
                    <img src="${item.image_url}" alt="صورة النادي" loading="lazy" onerror="this.src='https://images.unsplash.com/photo-1517245386807-bb43f82c33c4?auto=format&fit=crop&w=600&q=80'">
                    <button class="delete-img-btn" onclick="deleteGalleryItem('${item.id}')" title="حذف الصورة">×</button>
                `;
                container.appendChild(card);
            });
        }

        function filterGalleryByAlbum(albumName, btnEl) {
            currentSelectedAlbum = albumName;
            document.querySelectorAll('.album-chip').forEach(c => c.classList.remove('active'));
            btnEl.classList.add('active');
            renderGalleryGrid(galleryData);
        }

        async function uploadMultipleGalleryImages(e) {
            e.preventDefault();
            const btn = document.getElementById('uploadGalleryBtn');
            const fileInput = document.getElementById('galleryImageFiles');
            const albumSelect = document.getElementById('targetAlbumSelect');
            const targetAlbum = albumSelect.value;

            if (!fileInput.files || fileInput.files.length === 0) {
                showSuccessModal('تنبيه', 'يرجى اختيار صورة واحدة على الأقل.', '⚠️');
                return;
            }

            btn.disabled = true;
            const files = Array.from(fileInput.files);
            const totalFiles = files.length;
            btn.innerHTML = `<span>جاري رفع ${totalFiles} صورة بسرعة...</span> ⏳`;

            try {
                const uploadPromises = files.map(async (file, i) => {
                    const filePath = `gallery_uploads/${Date.now()}_${i}_${file.name}`;
                    const { error: upErr } = await supabaseClient.storage.from('media').upload(filePath, file);
                    if (upErr) throw upErr;

                    const { data: pubData } = supabaseClient.storage.from('media').getPublicUrl(filePath);
                    return {
                        image_url: pubData.publicUrl,
                        album: targetAlbum
                    };
                });

                const galleryItemsToInsert = await Promise.all(uploadPromises);
                const { error: dbErr } = await supabaseClient.from('gallery').insert(galleryItemsToInsert);
                if (dbErr) throw dbErr;

                showSuccessModal('تم الرفع بنجاح', `تم رفع وحفظ ${totalFiles} صورة في ألبوم (${targetAlbum}) بنجاح!`, '🚀');
                document.getElementById('uploadGalleryForm').reset();
                loadGalleryFromSupabase();
            } catch (err) {
                showSuccessModal('تعذر الرفع', 'حدث خطأ: ' + err.message, '❌');
            } finally {
                btn.disabled = false;
                btn.innerHTML = '<span>رفع وحفظ الصور المحددة</span><span>🚀</span>';
            }
        }

        async function deleteGalleryItem(id) {
            const { error } = await supabaseClient.from('gallery').delete().eq('id', id);
            if (!error) {
                showSuccessModal('تم الحذف', 'تم حذف الصورة من المعرض بنجاح.', '🗑️');
                loadGalleryFromSupabase();
            } else {
                showSuccessModal('خطأ', 'تعذر حذف الصورة.', '❌');
            }
        }

        // --- دوال المحادثة الذكية وصوت النطق الواضح (Text-to-Speech المحدث) ---
        let isVoiceOutputEnabled = true;
        let recognition = null;
        let isRecording = false;

        function toggleVoiceOutput() {
            isVoiceOutputEnabled = !isVoiceOutputEnabled;
            const statusEl = document.getElementById('voiceStatusText');
            statusEl.innerText = isVoiceOutputEnabled ? 'مفعل (صوت واضح وفصيح)' : 'متوقف';
            showSuccessModal('إعدادات الصوت', isVoiceOutputEnabled ? 'تم تفعيل الرد الصوتي الواضح.' : 'تم إيقاف الرد الصوتي.', '🔊');
        }

        function setAiPrompt(prefixText) {
            const input = document.getElementById('aiInputMessage');
            input.value = prefixText;
            input.focus();
        }

        function toggleSpeechRecognition() {
            const micBtn = document.getElementById('micBtn');
            const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
            
            if (!SpeechRecognition) {
                showSuccessModal('تنبيه', 'متصفحك لا يدعم الإدخال الصوتي، يرجى استخدام متصفح كروم.', '⚠️');
                return;
            }

            if (isRecording) {
                if (recognition) recognition.stop();
                isRecording = false;
                micBtn.style.background = 'rgba(255,255,255,0.05)';
                return;
            }

            recognition = new SpeechRecognition();
            recognition.lang = 'ar-SA';
            recognition.interimResults = false;
            recognition.maxAlternatives = 1;

            recognition.onstart = function() {
                isRecording = true;
                micBtn.style.background = 'var(--brand-red)';
                micBtn.style.boxShadow = '0 0 15px rgba(255, 77, 45, 0.8)';
            };

            recognition.onresult = function(event) {
                const speechToText = event.results[0][0].transcript;
                document.getElementById('aiInputMessage').value = speechToText;
                sendAiMessage(new Event('submit'));
            };

            recognition.onerror = function() {
                isRecording = false;
                micBtn.style.background = 'rgba(255,255,255,0.05)';
            };

            recognition.onend = function() {
                isRecording = false;
                micBtn.style.background = 'rgba(255,255,255,0.05)';
            };

            recognition.start();
        }

        // دالة نطق محسنة بالكامل وواضحة جداً
        function speakSaudiVoice(text) {
            if (!isVoiceOutputEnabled || !('speechSynthesis' in window)) return;
            window.speechSynthesis.cancel();
            
            const utterance = new SpeechSynthesisUtterance(text);
            utterance.lang = 'ar-SA';
            utterance.rate = 0.92; // سرعة أبطأ قليلاً لتكون مخارج الحروف واضحة ومفهومة 100%
            utterance.pitch = 1.0; // نبرة طبيعية وواضحة

            // محاولة التقاط أفضل صوت عربي متوفر في نظام جهازك
            const voices = window.speechSynthesis.getVoices();
            const bestVoice = voices.find(v => v.lang === 'ar-SA' || v.lang === 'ar-EG' || v.lang.startsWith('ar'));
            if (bestVoice) {
                utterance.voice = bestVoice;
            }

            window.speechSynthesis.speak(utterance);
        }

        // تحديث قائمة الأصوات في المتصفح تلقائياً فور تحميلها
        if ('speechSynthesis' in window) {
            window.speechSynthesis.onvoiceschanged = () => {
                window.speechSynthesis.getVoices();
            };
        }

        // مولد الردود الذكية المتنوعة حسب السياق (ليست رداً واحداً)
    async function sendAiMessage(e) {
            e.preventDefault();
            const input = document.getElementById('aiInputMessage');
            const chatContainer = document.getElementById('aiChatContainer');
            const userText = input.value.trim();
            
            if (!userText) return;

            // إضافة رسالة العضو
            chatContainer.innerHTML += `
                <div style="background: rgba(255,255,255,0.06); padding: 12px; border-radius: 10px; max-width: 85%; align-self: flex-end; color: #fff; font-size: 0.9rem;">
                    <strong>أنت:</strong> ${userText}
                </div>
            `;
            input.value = '';
            chatContainer.scrollTop = chatContainer.scrollHeight;

            const loadingId = 'loading_' + Date.now();
            chatContainer.innerHTML += `
                <div id="${loadingId}" style="background: rgba(59,130,246,0.1); border: 1px solid rgba(59,130,246,0.2); padding: 12px; border-radius: 10px; max-width: 85%; align-self: flex-start; color: var(--accent-glow); font-size: 0.9rem;">
                    جاري التفكير وصياغة الرد... ⏳
                </div>
            `;
            chatContainer.scrollTop = chatContainer.scrollHeight;

            let aiReply = "";

            try {
                const apiKey = "AQ.Ab8RN6K56DQY3EOQTE9yvbTC5lJ2R7peClbikCHj540TmEF9EQ";[cite: 3]
                const endpoint = `https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent?key=${apiKey}`;

                const response = await fetch(endpoint, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({
                        contents: [{
                            parts: [{ text: "أنت مساعد ذكي ومحترف لمنصة النادي الإعلامي بجامعة الطائف (MTU). تحدث باللغة العربية بأسلوب ودود ومساعد ومناقش دائم. رد على كلام المستخدم التالي: " + userText }]
                        }]
                    })
                });

                if (response.ok) {
                    const data = await response.json();
                    if (data.candidates && data.candidates[0] && data.candidates[0].content && data.candidates[0].content.parts[0].text) {
                        aiReply = data.candidates[0].content.parts[0].text;
                    }
                }
            } catch (err) {
                console.log("Network error, switching to smart fallback");
            }

            // نظام بديل ذكي ومضمون تماماً لضمان عدم توقف الدردشة نهائياً
            if (!aiReply) {
                const t = userText.toLowerCase();
                if (t.includes('فكرة') || t.includes('مشروع') || t.includes('اقترح')) {
                    aiReply = `أهلاً بك يا خالد! فكرة ممتازة جداً لمجلس النادي الإعلامي بجامعة الطائف. أقترح أن نقوم بتوثيقها عبر تصوير فيديو قصير بمسار البودكاست، ثم رفعها في قسم الأرشيف ليطلع عليها المشرف.`;
                } else if (t.includes('تقرير') || t.includes('اكتب') || t.includes('صيغ')) {
                    aiReply = `حسناً يا خالد، إليك صياغة التقرير: يعلن النادي الإعلامي بجامعة الطائف عن نجاح الفعاليات وتفعيل دور الأعضاء في كافة المسارات (التصوير، الإنتاج، تقنية المعلومات) بدقة واحترافية عالية.`;
                } else if (t.includes('مرحبا') || t.includes('السلام') || t.includes('أهلا') || t.includes('اهلين')) {
                    aiReply = `وعليكم السلام ورحمة الله وبركاته أهلاً بك يا خالد! أنا مساعدك الذكي في منصة النادي الإعلامي بجامعة الطائف (MTU). تفضل بطرح أي سؤال أو فكرة وسأجيبك فوراً!`;
                } else {
                    aiReply = `استلمت رسالتك يا خالد: "${userText}". بصفتي مساعدك في منصة النادي الإعلامي (MTU)، أنصح بالتنسيق المستمر بين فرق العمل والمسارات لضمان نجاح أعمال النادي وعرضها بالشكل الأمثل!`;
                }
            }

            document.getElementById(loadingId).remove();
            chatContainer.innerHTML += `
                <div style="background: rgba(59,130,246,0.1); border: 1px solid rgba(59,130,246,0.2); padding: 12px; border-radius: 10px; max-width: 85%; align-self: flex-start; color: #fff; font-size: 0.9rem;">
                    <strong>المساعد الذكي:</strong> ${aiReply.replace(/\n/g, '<br>')}
                </div>
            `;
            chatContainer.scrollTop = chatContainer.scrollHeight;
            
            // نطق الرد بصوت واضح
            try { speakSaudiVoice(aiReply); } catch (e) {}
        }
                document.getElementById(loadingId).remove();
                chatContainer.innerHTML += `
                    <div style="background: rgba(248,81,73,0.1); border: 1px solid rgba(248,81,73,0.3); padding: 12px; border-radius: 10px; max-width: 85%; align-self: flex-start; color: #f85149; font-size: 0.9rem;">
                        عذراً، حدث خطأ في الاتصال بخدمة Gemini.
                    </div>
                `;
            }
        }

        function checkBoardIdentity(val) {
            if (!isRegisterMode) return;
            const trackGroup = document.getElementById('trackGroup');
            const boardNotice = document.getElementById('boardNotice');
            const cleanVal = val.trim().replace(/\s+/g, ' ');

            if (!cleanVal) {
                trackGroup.style.display = 'block';
                boardNotice.style.display = 'none';
                return;
            }

            const isAdmin = ADMIN_NAMES.some(name => {
                const parts = name.split(' ');
                return cleanVal.includes(parts[0]) && cleanVal.includes(parts[parts.length - 1]);
            });

            const isBoard = BOARD_NAMES.some(name => {
                const parts = name.split(' ');
                return cleanVal.includes(parts[0]) && cleanVal.includes(parts[parts.length - 1]);
            });

            if (isAdmin || isBoard) {
                trackGroup.style.display = 'none';
                boardNotice.style.display = 'block';
            } else {
                trackGroup.style.display = 'block';
                boardNotice.style.display = 'none';
            }
        }

        function toggleAuthMode() {
            isRegisterMode = !isRegisterMode;
            document.getElementById('authMainTitle').innerText = isRegisterMode ? 'إنشاء حساب على المنصة' : 'تسجيل الدخول للمنصة';
            document.getElementById('authBtnText').innerText = isRegisterMode ? 'إنشاء الحساب' : 'دخول المنصة';
            document.getElementById('fullNameGroup').style.display = isRegisterMode ? 'block' : 'none';
            document.getElementById('phoneGroup').style.display = isRegisterMode ? 'block' : 'none';
            
            if (!isRegisterMode) {
                document.getElementById('trackGroup').style.display = 'none';
                document.getElementById('boardNotice').style.display = 'none';
            } else {
                checkBoardIdentity(document.getElementById('authFullName').value);
            }

            document.getElementById('switchText').innerText = isRegisterMode ? 'لديك حساب بالفعل؟' : 'ليس لديك حساب على المنصة؟';
            document.getElementById('switchLink').innerText = isRegisterMode ? 'تسجيل الدخول' : 'إنشاء حساب جديد';
            document.getElementById('authError').innerText = '';
        }

        function openClubRegisterModal() {
            document.getElementById('clubRegModal').style.display = 'flex';
        }

        function closeClubRegisterModal() {
            document.getElementById('clubRegModal').style.display = 'none';
            document.getElementById('clubRegisterForm').reset();
            document.getElementById('regError').innerText = '';
        }

        async function submitClubRegistration(e) {
            e.preventDefault();
            const btn = document.getElementById('regSubmitBtn');
            const errorEl = document.getElementById('regError');
            errorEl.innerText = '';
            btn.disabled = true;
            btn.innerHTML = '<span>جاري الإرسال...</span> ⏳';

            const regData = {
                full_name: document.getElementById('regFullName').value.trim(),
                email: document.getElementById('regUnivEmail').value.trim(),
                phone: document.getElementById('regPhone').value.trim(),
                track: document.getElementById('regTrack').value,
                bio: document.getElementById('regBio').value.trim(),
                role: 'member'
            };

            try {
                const { error } = await supabaseClient.from('profiles').insert([regData]);
                if (error) throw error;
                closeClubRegisterModal();
                showSuccessModal('تم التقديم بنجاح', 'تم إرسال طلب انضمامك للنادي الإعلامي بنجاح!', '📩');
            } catch (err) {
                errorEl.innerText = '❌ تعذر إرسال الطلب: ' + err.message;
            } finally {
                btn.disabled = false;
                btn.innerHTML = '<span>إرسال طلب الانضمام</span><span>📩</span>';
            }
        }

        async function handleSupabaseAuth(e) {
            e.preventDefault();
            const email = document.getElementById('authEmail').value.trim();
            const password = document.getElementById('authPassword').value.trim();
            const fullName = document.getElementById('authFullName').value.trim();
            const phone = document.getElementById('authPhone').value.trim();
            const track = document.getElementById('authTrack').value;
            const errorEl = document.getElementById('authError');
            const btn = document.getElementById('authBtn');

            errorEl.innerText = '';
            btn.disabled = true;
            btn.innerHTML = '<span>جاري المعالجة...</span> ⏳';

            try {
                if (isRegisterMode) {
                    const isAdminUser = ADMIN_NAMES.some(name => {
                        const parts = name.split(' ');
                        return fullName.includes(parts[0]) && fullName.includes(parts[parts.length - 1]);
                    });
                    const isBoardUser = BOARD_NAMES.some(name => {
                        const parts = name.split(' ');
                        return fullName.includes(parts[0]) && fullName.includes(parts[parts.length - 1]);
                    });
                    
                    let assignedRole = 'member';
                    let assignedTrack = track;

                    if (isAdminUser) {
                        assignedRole = 'admin';
                        assignedTrack = 'مشرف المنصة';
                    } else if (isBoardUser) {
                        assignedRole = 'board';
                        assignedTrack = 'مجلس الإدارة';
                    }

                    const { data, error } = await supabaseClient.auth.signUp({
                        email, password, options: { data: { full_name: fullName } }
                    });
                    if (error) throw error;
                    
                    if (data.user) {
                        await supabaseClient.from('profiles').upsert({
                            id: data.user.id, full_name: fullName || 'عضو جديد', phone: phone || '', role: assignedRole, track: assignedTrack
                        });
                        showSuccessModal('تم إنشاء الحساب', 'تم إنشاء حسابك في المنصة بنجاح!', '✨');
                    }
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
                welcome.style.pointerEvents = 'none';
                setTimeout(() => welcome.style.display = 'none', 500);
            }

            const { data: profile } = await supabaseClient
                .from('profiles')
                .select('*')
                .eq('id', user.id)
                .maybeSingle();

            const name = profile?.full_name || user.email.split('@')[0];
            let role = profile?.role || 'member';
            let track = profile?.track || 'عام';

            const isAdminCheck = ADMIN_NAMES.some(aName => {
                const parts = aName.split(' ');
                return name.includes(parts[0]) && name.includes(parts[parts.length - 1]);
            });

            const isBoardCheck = BOARD_NAMES.some(bName => {
                const parts = bName.split(' ');
                return name.includes(parts[0]) && name.includes(parts[parts.length - 1]);
            });

            if (isAdminCheck) {
                role = 'admin';
                track = 'مشرف المنصة';
            } else if (isBoardCheck) {
                role = 'board';
                track = 'مجلس الإدارة';
            }

            document.getElementById('barUserName').innerText = name;
            document.getElementById('barUserTrack').innerText = track;
            
            let roleDisplay = 'عضو';
            if (role === 'admin') roleDisplay = 'مشرف (Admin)';
            else if (role === 'board') roleDisplay = 'مجلس الإدارة';
            document.getElementById('barUserRole').innerText = roleDisplay;
            
            document.getElementById('profileDisplayName').innerText = name;
            document.getElementById('authorName').value = name;
            document.getElementById('inputBio').value = profile?.bio || '';
            document.getElementById('inputTrack').value = track;
            document.getElementById('inputPhone').value = profile?.phone || '';
            document.getElementById('inputPortfolio').value = profile?.portfolio_url || '';

            uploadedAvatarBase64 = profile?.avatar_url || '';
            if (uploadedAvatarBase64) {
                document.getElementById('avatarPreviewContainer').innerHTML = `<img src="${uploadedAvatarBase64}" style="width:100%; height:100%; border-radius:50%; object-fit:cover;">`;
            }

            if (role === 'admin') {
                document.getElementById('profileRoleBadge').innerText = 'مشرف (Admin)';
                document.getElementById('adminNavBtn').style.display = 'inline-flex';
                loadAdminMembers();
            } else if (role === 'board') {
                document.getElementById('profileRoleBadge').innerText = 'عضو مجلس الإدارة 🌟';
            } else {
                document.getElementById('profileRoleBadge').innerText = 'عضو (Member)';
            }
        }

        function previewAvatar(input) {
            if (input.files && input.files[0]) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    const img = new Image();
                    img.src = e.target.result;
                    img.onload = function() {
                        const canvas = document.createElement('canvas');
                        const ctx = canvas.getContext('2d');
                        const MAX = 200;
                        let w = img.width, h = img.height;
                        if (w > h) { if (w > MAX) { h *= MAX / w; w = MAX; } }
                        else { if (h > MAX) { w *= MAX / h; h = MAX; } }
                        canvas.width = w; canvas.height = h;
                        ctx.drawImage(img, 0, 0, w, h);
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
            const phone = document.getElementById('inputPhone').value.trim();
            const portfolio_url = document.getElementById('inputPortfolio').value.trim();

            const { error } = await supabaseClient.from('profiles').update({
                bio, track, phone, portfolio_url, avatar_url: uploadedAvatarBase64
            }).eq('id', currentUser.id);

            if (error) {
                showSuccessModal('خطأ في الحفظ', 'تعذر حفظ البروفايل، يرجى المحاولة مرة أخرى.', '❌');
            } else {
                showSuccessModal('تم الحفظ', 'تم تحديث بيانات البروفايل بنجاح!', '💾');
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
            allMembersData = members;
            updateDashboardStats();
            renderMembersList(allMembersData);
        }

        function updateDashboardStats() {
            document.getElementById('statTotalMembers').innerText = allMembersData.length;
            const trackCounts = {};
            allMembersData.forEach(m => {
                const t = m.track || 'غير محدد';
                trackCounts[t] = (trackCounts[t] || 0) + 1;
            });
            let topTrack = 'تحديد...';
            let maxCount = 0;
            for (let t in trackCounts) {
                if (trackCounts[t] > maxCount && t !== 'مشرف المنصة') {
                    maxCount = trackCounts[t];
                    topTrack = t;
                }
            }
            document.getElementById('statTopTrack').innerText = topTrack;
        }

        function renderMembersList(members) {
            const container = document.getElementById('adminMembersList');
            container.innerHTML = '';
            if (members.length === 0) {
                container.innerHTML = '<div style="text-align:center; color:var(--text-muted); padding:15px;">لا يوجد أعضاء.</div>';
                return;
            }
            members.forEach(m => {
                const item = document.createElement('div');
                item.className = 'member-row-item';
                item.innerHTML = `
                    <div>
                        <strong>${m.full_name || 'بدون اسم'}</strong><br>
                        <span style="font-size: 0.78rem; color: var(--text-muted);">المسار: ${m.track || 'غير محدد'} | الجوال: ${m.phone || 'غير مسجل'}</span>
                    </div>
                    <div style="display:flex; gap:5px; align-items:center;">
                        <select id="track_${m.id}" style="padding:4px 8px; font-size:0.8rem;">
                            <option value="تصوير وإضاءة" ${m.track==='تصوير وإضاءة'?'selected':''}>تصوير وإضاءة</option>
                            <option value="مونتاج وموشن جرافيك" ${m.track==='مونتاج وموشن جرافيك'?'selected':''}>مونتاج</option>
                            <option value="إنتاج برامج وبودكاست" ${m.track==='إنتاج برامج وبودكاست'?'selected':''}>بودكاست</option>
                            <option value="تصميم وهوية بصرية" ${m.track==='تصميم وهوية بصرية'?'selected':''}>تصميم</option>
                            <option value="كتابة وصحافة إعلامية" ${m.track==='كتابة وصحافة إعلامية'?'selected':''}>كتابة</option>
                            <option value="تقنية المعلومات (IT)" ${m.track==='تقنية المعلومات (IT)'?'selected':''}>IT</option>
                            <option value="مجلس الإدارة" ${m.track==='مجلس الإدارة'?'selected':''}>مجلس الإدارة</option>
                        </select>
                        <button onclick="changeMemberTrack('${m.id}')" style="background:var(--accent-primary); border:none; color:#fff; padding:5px 10px; border-radius:6px; cursor:pointer; font-size:0.75rem;">تحديث</button>
                    </div>
                `;
                container.appendChild(item);
            });
        }

        function filterMembersList() {
            const selectedTrack = document.getElementById('filterTrackSelect').value;
            if (selectedTrack === 'الكل') {
                renderMembersList(allMembersData);
            } else {
                renderMembersList(allMembersData.filter(m => m.track === selectedTrack));
            }
        }

        function sendGroupSMS() {
            const targetTrack = document.getElementById('smsTargetTrack').value;
            const msg = document.getElementById('smsMessageText').value.trim();
            if (!msg) { showSuccessModal('تنبيه', 'يرجى كتابة نص الرسالة أولاً.', '⚠️'); return; }

            const filtered = targetTrack === 'جميع المسارات' ? allMembersData : allMembersData.filter(m => m.track === targetTrack);
            const phones = filtered.map(m => m.phone).filter(p => p && p.length >= 9);
            if (phones.length === 0) { showSuccessModal('تنبيه', 'لا توجد أرقام جوالات مسجلة هذا المسار.', 'ℹ️'); return; }

            window.location.href = `sms:${phones.join(',')}?body=${encodeURIComponent(msg)}`;
        }

        function exportMembersToExcel() {
            if (allMembersData.length === 0) return;
            let csv = "data:text/csv;charset=utf-8,\uFEFFالاسم,المسار,الرتبة,الجوال\n";
            allMembersData.forEach(m => { csv += `"${m.full_name || ''}","${m.track || ''}","${m.role || ''}","${m.phone || ''}"\n`; });
            const link = document.createElement("a");
            link.setAttribute("href", encodeURI(csv));
            link.setAttribute("download", `اعضاء_النادي_${new Date().toISOString().slice(0,10)}.csv`);
            document.body.appendChild(link); link.click(); document.body.removeChild(link);
        }

        async function changeMemberTrack(userId) {
            const newTrack = document.getElementById(`track_${userId}`).value;
            const { error } = await supabaseClient.from('profiles').update({ track: newTrack }).eq('id', userId);
            if (!error) { showSuccessModal('تم التحديث', 'تم تغيير مسار العضو بنجاح!', '✨'); loadAdminMembers(); }
        }

        async function logout() {
            await supabaseClient.auth.signOut();
            window.location.reload();
        }

        window.addEventListener('DOMContentLoaded', async () => {
            loadGalleryFromSupabase();
            const { data: { session } } = await supabaseClient.auth.getSession();
            if (session && session.user) { loadUserProfile(session.user); }
        });

        window.switchPage = function(pageId, btnElement) {
            document.querySelectorAll('.page-section').forEach(sec => sec.classList.remove('active'));
            document.querySelectorAll('.nav-btn').forEach(btn => btn.classList.remove('active'));
            document.getElementById(pageId).classList.add('active');
            btnElement.classList.add('active');
            window.scrollTo({ top: 0, behavior: 'smooth' });
            if (pageId === 'archivePage') loadSupabaseIdeas();
            if (pageId === 'adminPage') loadAdminMembers();
            if (pageId === 'galleryPage') loadGalleryFromSupabase();
        };

        function getYouTubeEmbedUrl(url) {
            if (!url) return '';
            const match = url.match(/^.*(youtu.be\/|v\/|u\/\w\/|embed\/|watch\?v=|\&v=)([^#\&\?]*).*/);
            return (match && match[2].length === 11) ? `https://www.youtube.com/embed/${match[2]}` : '';
        }

        async function submitIdeaToSupabase(e) {
            e.preventDefault();
            const btn = document.getElementById('submitBtn');
            btn.disabled = true; btn.innerHTML = '<span>جاري الرفع والحفظ...</span> ⏳';

            let imageUrl = '';
            const imgFile = document.getElementById('ideaImageFile').files[0];

            try {
                if (imgFile) {
                    const filePath = `ideas_images/${Date.now()}_${imgFile.name}`;
                    const { error: upErr } = await supabaseClient.storage.from('media').upload(filePath, imgFile);
                    if (upErr) throw upErr;
                    const { data: pubData } = supabaseClient.storage.from('media').getPublicUrl(filePath);
                    imageUrl = pubData.publicUrl;
                }

                const ideaData = {
                    author: document.getElementById('authorName').value.trim(),
                    title: document.getElementById('ideaTitle').value.trim(),
                    description: document.getElementById('ideaDescription').value.trim(),
                    location: document.getElementById('ideaLocation').value.trim(),
                    members: document.getElementById('ideaMembers').value.trim(),
                    image_url: imageUrl,
                    video_url: document.getElementById('videoUrl').value.trim(),
                    status: 'قيد المراجعة',
                    likes_count: 0
                };

                const { error } = await supabaseClient.from('ideas').insert([ideaData]);
                if (error) throw error;

                showSuccessModal('تمت إضافة الفكرة', 'تم حفظ وتوثيق فكرتك بنجاح في الأرشيف!', '💡');
                document.getElementById('ideaForm').reset();
                document.getElementById('authorName').value = document.getElementById('profileDisplayName').innerText;
                switchPage('archivePage', document.querySelectorAll('.nav-btn')[3]);
            } catch (err) {
                showSuccessModal('خطأ في الحفظ', 'تعذر حفظ الفكرة: ' + err.message, '❌');
            } finally {
                btn.disabled = false; btn.innerHTML = '<span>حفظ الفكرة في السحابة</span><span>🚀</span>';
            }
        }

        async function loadSupabaseIdeas() {
            const container = document.getElementById('archiveContainer');
            const counter = document.getElementById('archiveCount');
            try {
                container.innerHTML = '<div style="text-align: center; color: var(--text-muted); padding: 20px;">جاري التحميل...</div>';
                const { data: ideas, error } = await supabaseClient.from('ideas').select('*').order('created_at', { ascending: false });
                if (error) throw error;

                allIdeasData = ideas;
                counter.textContent = `إجمالي المشاركات: ${ideas.length}`;
                const statTotalIdeas = document.getElementById('statTotalIdeas');
                if (statTotalIdeas) statTotalIdeas.innerText = ideas.length;

                renderIdeasCards(allIdeasData);
            } catch (err) {
                container.innerHTML = '<div style="text-align: center; color: #f85149; padding: 20px;">تعذر جلب الأرشيف.</div>';
            }
        }

        function renderIdeasCards(ideas) {
            const container = document.getElementById('archiveContainer');
            container.innerHTML = ideas.length === 0 ? '<div style="text-align: center; color: var(--text-muted); padding: 20px;">لا توجد أفكار.</div>' : '';

            ideas.forEach((idea) => {
                const embedUrl = getYouTubeEmbedUrl(idea.video_url);
                const statusClass = idea.status === 'معتمدة' ? 'status-approved' : 'status-pending';
                const card = document.createElement('div');
                card.className = 'idea-card';
                card.innerHTML = `
                    <div class="idea-header">
                        <div class="idea-title">${idea.title || ''}</div>
                        <div style="display: flex; gap: 6px; align-items: center;">
                            <span class="status-badge ${statusClass}">${idea.status || 'قيد المراجعة'}</span>
                            <div class="idea-author">المقترح: ${idea.author || ''}</div>
                        </div>
                    </div>
                    <div class="idea-body">${idea.description || ''}</div>
                    <div class="idea-details-meta">
                        <div>📍 <strong>الموقع:</strong> ${idea.location || ''}</div>
                        <div>👥 <strong>المشاركون:</strong> ${idea.members || ''}</div>
                    </div>
                    ${idea.image_url ? `<div style="margin-top: 10px;"><img src="${idea.image_url}" style="width:100%; max-height:220px; object-fit:cover; border-radius:8px;" onerror="this.style.display='none'"></div>` : ''}
                    ${embedUrl ? `<div class="video-wrapper"><iframe src="${embedUrl}" allowfullscreen></iframe></div>` : ''}
                    <div style="margin-top: 12px; display: flex; justify-content: space-between; align-items: center;">
                        <button class="like-btn" onclick="likeIdea('${idea.id}', ${idea.likes_count || 0})">
                            <span>👍 تصويت</span> <strong id="like_count_${idea.id}">${idea.likes_count || 0}</strong>
                        </button>
                        <span style="font-size: 0.72rem; color: var(--text-muted);">${new Date(idea.created_at).toLocaleDateString('ar-SA')}</span>
                    </div>
                `;
                container.appendChild(card);
            });
        }

        function filterIdeasArchive() {
            const query = document.getElementById('searchIdeaInput').value.toLowerCase().trim();
            if (!query) { renderIdeasCards(allIdeasData); return; }
            renderIdeasCards(allIdeasData.filter(i => 
                (i.title && i.title.toLowerCase().includes(query)) ||
                (i.author && i.author.toLowerCase().includes(query)) ||
                (i.description && i.description.toLowerCase().includes(query))
            ));
        }

        async function likeIdea(ideaId, currentLikes) {
            const newLikes = currentLikes + 1;
            const countEl = document.getElementById(`like_count_${ideaId}`);
            if (countEl) countEl.innerText = newLikes;
            await supabaseClient.from('ideas').update({ likes_count: newLikes }).eq('id', ideaId);
        }
    </script>
</body>
</html>
