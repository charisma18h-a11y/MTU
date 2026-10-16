 # MTU
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>منصة النادي الإعلامي - التفاعلية والذكية | MTU</title>
    
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700;800;900&family=Montserrat:wght@800;900&display=swap" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>
    <!-- مكتبة التأثيرات الاحتفالية Confetti -->
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.5.1/dist/confetti.browser.min.js"></script>
    <!-- مكتبة كود الـ QR لبطاقة العضوية -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>

    <style>
        :root {
            --bg-dark: #05060a;
            --bg-card: rgba(15, 18, 28, 0.88);
            --bg-card-solid: #0d101d;
            --accent-primary: #3b82f6;
            --accent-glow: #60a5fa;
            --accent-green: #10b981;
            --accent-purple: #8b5cf6;
            --text-main: #f8fafc;
            --text-muted: #94a3b8;
            --border: rgba(255, 255, 255, 0.12);
            --input-bg: rgba(8, 10, 18, 0.85);
            --brand-red: #ff4d2d;
        }

        * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Cairo', sans-serif; -webkit-tap-highlight-color: transparent; }
        body { background-color: var(--bg-dark); color: var(--text-main); line-height: 1.7; padding-bottom: 50px; min-height: 100vh; overflow-x: hidden; }

        /* شريط الأخبار والنشاط المباشر الحي */
        .live-ticker-bar {
            background: linear-gradient(90deg, #1e1b4b, #0f172a, #1e1b4b);
            border-bottom: 1px solid var(--border); padding: 6px 12px; font-size: 0.8rem;
            display: flex; align-items: center; justify-content: space-between; overflow: hidden; white-space: nowrap;
        }
        .ticker-content { display: inline-block; animation: ticker 25s linear infinite; color: var(--accent-glow); font-weight: 700; }
        @keyframes ticker { 0% { transform: translateX(100%); } 100% { transform: translateX(-100%); } }

        /* نقطة النبض التفاعلية للتواجد */
        .pulse-dot { display: inline-block; width: 9px; height: 9px; background-color: #22c55e; border-radius: 50%; box-shadow: 0 0 10px #22c55e; animation: pulse 1.5s infinite; margin-left: 6px; }
        @keyframes pulse { 0% { transform: scale(0.95); box-shadow: 0 0 0 0 rgba(34, 197, 94, 0.7); } 70% { transform: scale(1); box-shadow: 0 0 0 8px rgba(34, 197, 94, 0); } 100% { transform: scale(0.95); box-shadow: 0 0 0 0 rgba(34, 197, 94, 0); } }

        .quick-nav { position: sticky; top: 0; z-index: 1000; background: rgba(12, 14, 24, 0.88); backdrop-filter: blur(15px); border-bottom: 1px solid var(--border); padding: 10px; display: flex; justify-content: center; gap: 6px; flex-wrap: wrap; }
        .nav-btn { background: rgba(255, 255, 255, 0.05); color: var(--text-main); border: 1px solid var(--border); padding: 8px 14px; border-radius: 20px; font-size: 0.8rem; font-weight: 700; cursor: pointer; transition: all 0.3s ease; }
        .nav-btn.active, .nav-btn:hover { background: var(--accent-primary); color: #fff; border-color: var(--accent-glow); transform: translateY(-2px); box-shadow: 0 4px 15px rgba(59, 130, 246, 0.4); }

        .container { max-width: 980px; margin: 20px auto; padding: 0 12px; }
        .page-section { display: none; }
        .page-section.active { display: block; animation: fadeIn 0.4s ease-in-out; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(8px); } to { opacity: 1; transform: translateY(0); } }

        .card { background: var(--bg-card); border: 1px solid var(--border); backdrop-filter: blur(15px); border-radius: 16px; padding: 20px; margin-bottom: 20px; box-shadow: 0 10px 30px rgba(0, 0, 0, 0.7); }
        .section-title { font-size: 1.2rem; font-weight: 800; margin-bottom: 16px; display: flex; align-items: center; gap: 10px; color: #fff; }

        /* زر المساعد الصوتي والذكي العائم */
        .ai-voice-fab {
            position: fixed; bottom: 20px; left: 20px; z-index: 9999;
            background: linear-gradient(135deg, #8b5cf6, #3b82f6); color: #fff;
            padding: 12px 20px; border-radius: 30px; font-weight: 800; font-size: 0.9rem;
            cursor: pointer; border: 1px solid rgba(255,255,255,0.3);
            box-shadow: 0 10px 25px rgba(139, 92, 246, 0.5); display: flex; align-items: center; gap: 8px;
            transition: all 0.3s ease;
        }
        .ai-voice-fab:hover { transform: scale(1.05); box-shadow: 0 12px 30px rgba(139, 92, 246, 0.8); }

        /* نافذة المساعد الصوتي */
        #aiVoiceModal {
            position: fixed; inset: 0; z-index: 99999; background: rgba(3, 4, 8, 0.92); backdrop-filter: blur(15px);
            display: none; align-items: center; justify-content: center; padding: 20px;
        }
        .ai-card {
            background: rgba(16, 18, 27, 0.95); border: 1px solid rgba(139, 92, 246, 0.4);
            border-radius: 24px; padding: 28px; width: 100%; max-width: 450px; text-align: center;
            box-shadow: 0 20px 50px rgba(0,0,0,0.9), 0 0 30px rgba(139, 92, 246, 0.3);
        }
        .voice-wave-sphere {
            width: 100px; height: 100px; border-radius: 50%;
            background: radial-gradient(circle, #8b5cf6 0%, #3b82f6 100%);
            margin: 0 auto 20px; display: flex; align-items: center; justify-content: center; font-size: 2.8rem;
            box-shadow: 0 0 30px rgba(139, 92, 246, 0.8); transition: all 0.3s ease;
        }
        .voice-wave-sphere.listening { animation: pulseVoice 1s infinite alternate; }
        @keyframes pulseVoice { 0% { transform: scale(1); box-shadow: 0 0 20px rgba(139, 92, 246, 0.6); } 100% { transform: scale(1.2); box-shadow: 0 0 50px rgba(59, 130, 246, 0.9); } }

        /* شريط تقدم الرفع المباشر */
        .progress-container { width: 100%; background: rgba(255,255,255,0.05); border-radius: 10px; height: 12px; overflow: hidden; margin-top: 10px; display: none; }
        .progress-bar-fill { height: 100%; background: linear-gradient(90deg, var(--accent-primary), var(--accent-green)); width: 0%; transition: width 0.2s; }

        /* بطاقة العضوية الرقمية */
        .digital-id-card {
            background: linear-gradient(135deg, #0f172a 0%, #1e1b4b 100%); border: 1px solid var(--accent-glow);
            border-radius: 18px; padding: 20px; position: relative; overflow: hidden; color: #fff;
            box-shadow: 0 15px 35px rgba(0,0,0,0.6); margin-top: 15px; display: flex; justify-content: space-between; align-items: center;
        }

        /* المعرض والبطاقات */
        .gallery-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(170px, 1fr)); gap: 14px; margin-top: 15px; }
        .gallery-item { background: var(--bg-card-solid); border: 1px solid var(--border); border-radius: 10px; overflow: hidden; position: relative; cursor: pointer; transition: 0.3s; }
        .gallery-item:hover { transform: translateY(-4px); border-color: var(--accent-primary); }
        .gallery-item img { width: 100%; height: 150px; object-fit: cover; }

        /* عناصر النموذج */
        .form-group { margin-bottom: 14px; text-align: right; }
        label { display: block; margin-bottom: 5px; font-weight: 700; color: #cbd5e1; font-size: 0.85rem; }
        input, textarea, select { width: 100%; padding: 11px 14px; background-color: var(--input-bg); border: 1px solid var(--border); border-radius: 10px; color: #fff; outline: none; }
        button.btn-submit { background: linear-gradient(135deg, var(--accent-primary), #2563eb); color: #fff; font-weight: 800; padding: 12px 20px; border: none; border-radius: 10px; cursor: pointer; width: 100%; display: flex; align-items: center; justify-content: center; gap: 8px; }
    </style>
</head>
<body>

    <!-- شريط الأخبار والنشاط الفوري -->
    <div class="live-ticker-bar">
        <div><span class="pulse-dot"></span> <strong style="color: #fff;">المتواجدون الآن:</strong> <span id="onlineCount">14</span> عضو</div>
        <div style="overflow: hidden; max-width: 70%;">
            <div class="ticker-content">🚀 أهلاً بكم في المنصة الذكية بالنادي الإعلامي (MTU) | تم تفعيل المساعد الصوتي والذكاء الاصطناعي لمساعدتكم | تم تحديث معارض الصور وإتاحة الرفع الفائق!</div>
        </div>
    </div>

    <!-- زر الذكاء الاصطناعي والمساعد الصوتي العائم -->
    <div class="ai-voice-fab" onclick="openAIVoiceModal()">
        <span>🎙️ المساعد الصوتي والذكي</span>
    </div>

    <!-- نافذة المساعد الصوتي والذكاء الاصطناعي -->
    <div id="aiVoiceModal">
        <div class="ai-card">
            <div class="voice-wave-sphere" id="aiSphere">🤖</div>
            <h2 style="color: #fff; font-size: 1.3rem; margin-bottom: 6px;">مُساعد MTU الذكي والصوتي</h2>
            <p style="color: var(--text-muted); font-size: 0.85rem; margin-bottom: 20px;" id="aiStatusText">انقر للتحدث صوتياً أو اسأل الذكاء الاصطناعي عن الأفكار والمسارات!</p>
            
            <div style="display: flex; gap: 8px; margin-bottom: 15px;">
                <input type="text" id="aiTextInput" placeholder="اسأل الذكاء الاصطناعي شيئاً..." style="font-size: 0.85rem;">
                <button onclick="sendAITextQuery()" style="background: var(--accent-purple); border: none; color: #fff; padding: 0 16px; border-radius: 10px; font-weight: 700; cursor: pointer;">إرسال</button>
            </div>

            <div style="display: flex; gap: 10px;">
                <button id="voiceRecordBtn" onclick="toggleVoiceRecognition()" style="flex: 2; background: linear-gradient(135deg, #8b5cf6, #3b82f6); color: #fff; border: none; padding: 12px; border-radius: 12px; font-weight: 800; cursor: pointer; display: flex; align-items: center; justify-content: center; gap: 6px;">
                    <span>🎙️ بدء المحادثة الصوتية</span>
                </button>
                <button onclick="closeAIVoiceModal()" style="flex: 1; background: rgba(255,255,255,0.1); color: #fff; border: 1px solid var(--border); padding: 12px; border-radius: 12px; font-weight: 700; cursor: pointer;">إغلاق</button>
            </div>
            
            <div id="aiResponseBox" style="margin-top: 15px; text-align: right; background: rgba(0,0,0,0.4); padding: 12px; border-radius: 10px; font-size: 0.85rem; max-height: 150px; overflow-y: auto; display: none; border: 1px solid var(--border); color: #e2e8f0;"></div>
        </div>
    </div>

    <!-- شريط التنقل الرئيسي -->
    <nav class="quick-nav">
        <button class="nav-btn active" onclick="switchPage('homePage', this)">🏛️ المجلس والنشاط</button>
        <button class="nav-btn" onclick="switchPage('profilePage', this)">💳 بطاقتي والبروفايل</button>
        <button class="nav-btn" onclick="switchPage('formPage', this)">💡 تقديم فكرة + AI</button>
        <button class="nav-btn" onclick="switchPage('galleryPage', this)">🖼️ معرض الصور</button>
        <button class="nav-btn" onclick="switchPage('taskBoardPage', this)">📋 المهام (Kanban)</button>
    </nav>

    <div class="container">

        <!-- الصفحة الرئيسية وتلوين المتصدرين -->
        <section id="homePage" class="page-section active">
            <div class="card">
                <h2 class="section-title">🏆 لوحة شرف أعضاء النادي الأكثر تفاعلاً (XP Leaderboard)</h2>
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 12px; margin-top: 12px;">
                    <div style="background: rgba(245, 158, 11, 0.12); border: 1px solid rgba(245, 158, 11, 0.4); padding: 14px; border-radius: 12px; text-align: center;">
                        <div style="font-size: 1.5rem;">🥇</div>
                        <strong style="color: #fbbf24;">خالد أحمد الهلال</strong>
                        <div style="font-size: 0.8rem; color: var(--text-muted);">مسؤول IT - 450 XP</div>
                    </div>
                    <div style="background: rgba(148, 163, 184, 0.12); border: 1px solid rgba(148, 163, 184, 0.3); padding: 14px; border-radius: 12px; text-align: center;">
                        <div style="font-size: 1.5rem;">🥈</div>
                        <strong style="color: #cbd5e1;">عبدالرحمن الزهراني</strong>
                        <div style="font-size: 0.8rem; color: var(--text-muted);">رئيس النادي - 390 XP</div>
                    </div>
                    <div style="background: rgba(180, 83, 9, 0.12); border: 1px solid rgba(180, 83, 9, 0.3); padding: 14px; border-radius: 12px; text-align: center;">
                        <div style="font-size: 1.5rem;">🥉</div>
                        <strong style="color: #f97316;">ماجد الشاطري</strong>
                        <div style="font-size: 0.8rem; color: var(--text-muted);">نائب الرئيس - 310 XP</div>
                    </div>
                </div>
            </div>
        </section>

        <!-- صفحة البروفايل وبطاقة العضوية الرقمية -->
        <section id="profilePage" class="page-section">
            <div class="card">
                <h2 class="section-title">💳 بطاقة العضوية الرقمية والبروفايل</h2>
                
                <div class="digital-id-card">
                    <div>
                        <div style="font-size: 0.75rem; color: var(--accent-glow); font-weight: 800;">MTU DIGITAL ID CARD</div>
                        <h3 id="cardFullName" style="font-size: 1.1rem; margin-top: 4px;">خالد أحمد الهلال</h3>
                        <div style="font-size: 0.82rem; opacity: 0.8;" id="cardTrack">مسار تقنية المعلومات (IT)</div>
                        <div style="font-size: 0.75rem; margin-top: 10px; background: rgba(255,255,255,0.15); display: inline-block; padding: 2px 8px; border-radius: 6px;">رقم العضوية: #MTU-2026-99</div>
                    </div>
                    <div id="qrcode" style="background: #fff; padding: 6px; border-radius: 8px;"></div>
                </div>
            </div>
        </section>

        <!-- صفحة تقديم الفكرة مع الذكاء الاصطناعي -->
        <section id="formPage" class="page-section">
            <div class="card">
                <h2 class="section-title">💡 تقديم فكرة + دعم بالذكاء الاصطناعي</h2>
                
                <div class="form-group">
                    <label>عنوان الفكرة أو المبادرة:</label>
                    <input type="text" id="ideaTitle" placeholder="مثال: تغطية خاصة ليوم التأسيس">
                </div>

                <div class="form-group">
                    <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 5px;">
                        <label style="margin-bottom: 0;">تفاصيل الفكرة:</label>
                        <button type="button" onclick="enhanceIdeaWithAI()" style="background: linear-gradient(135deg, #8b5cf6, #3b82f6); border: none; color: #fff; padding: 4px 12px; border-radius: 12px; font-size: 0.75rem; font-weight: 800; cursor: pointer;">🪄 تحسين الفكرة بالذكاء الاصطناعي</button>
                    </div>
                    <textarea id="ideaDescription" rows="4" placeholder="اكتب فكرتك باختصار والذكاء الاصطناعي سيساعدك في إكمال خطة التنفيذ..."></textarea>
                </div>

                <button class="btn-submit" onclick="submitIdea()"><span>حفظ وتوثيق الفكرة</span>🚀</button>
            </div>
        </section>

        <!-- معرض الصور المطور مع شريط نسبة الرفع المباشر -->
        <section id="galleryPage" class="page-section">
            <div class="card">
                <h2 class="section-title">🖼️ معرض فعاليات النادي (مع الرفع المباشر والنسبة)</h2>
                
                <form id="uploadForm" onsubmit="uploadImagesWithProgress(event)">
                    <div class="form-group">
                        <label>اختر صور متعددة (150+ صورة بدون تعليق):</label>
                        <input type="file" id="bulkImages" accept="image/*" multiple required style="padding: 8px;">
                    </div>
                    <button type="submit" class="btn-submit" id="uploadBtn"><span>رفع المحتوى الآن</span> ⚡</button>
                </form>

                <div class="progress-container" id="progressContainer">
                    <div class="progress-bar-fill" id="progressBarFill"></div>
                </div>
                <div id="progressStatusText" style="text-align: center; font-size: 0.8rem; color: var(--accent-glow); margin-top: 6px; display: none;">جاري الرفع: 0%</div>

                <div class="gallery-grid" id="galleryContainer">
                    <!-- الصور التفاعلية تحمّل هنا -->
                </div>
            </div>
        </section>

        <!-- لوحة المهام التفاعلية Kanban -->
        <section id="taskBoardPage" class="page-section">
            <div class="card">
                <h2 class="section-title">📋 لوحة توزيع مهام الفعاليات (Task Kanban)</h2>
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 12px;">
                    <div style="background: rgba(255,255,255,0.02); border: 1px solid var(--border); padding: 12px; border-radius: 10px;">
                        <h4 style="color: #fbbf24; margin-bottom: 8px;">⏳ مجدولة (To Do)</h4>
                        <div style="background: var(--bg-card-solid); padding: 8px; border-radius: 6px; font-size: 0.82rem; margin-bottom: 6px;">🎥 تجهيز مايكات البودكاست (فريق IT)</div>
                    </div>
                    <div style="background: rgba(255,255,255,0.02); border: 1px solid var(--border); padding: 12px; border-radius: 10px;">
                        <h4 style="color: #60a5fa; margin-bottom: 8px;">⚙️ قيد التنفيذ (In Progress)</h4>
                        <div style="background: var(--bg-card-solid); padding: 8px; border-radius: 6px; font-size: 0.82rem; margin-bottom: 6px;">🎬 مونتاج الفعالية الأخيرة (فريق المونتاج)</div>
                    </div>
                    <div style="background: rgba(255,255,255,0.02); border: 1px solid var(--border); padding: 12px; border-radius: 10px;">
                        <h4 style="color: #4ade80; margin-bottom: 8px;">✅ منجزة (Done)</h4>
                        <div style="background: var(--bg-card-solid); padding: 8px; border-radius: 6px; font-size: 0.82rem; margin-bottom: 6px;">📸 تغطية لقاء المشرف (فريق التصوير)</div>
                    </div>
                </div>
            </div>
        </section>

    </div>

    <script>
        // إعداد QR Code لبطاقة العضوية الرقمية
        window.addEventListener('DOMContentLoaded', () => {
            new QRCode(document.getElementById("qrcode"), {
                text: "https://mtu-taif.edu.sa/member/khaled",
                width: 65, height: 65,
                colorDark : "#000000", colorLight : "#ffffff"
            });
        });

        // تشغيل تأثير القصاصات الورقية والاحتفال Confetti
        function triggerConfetti() {
            confetti({
                particleCount: 100, spread: 70, origin: { y: 0.6 }
            });
        }

        // محاكاة الذكاء الاصطناعي لتحسين الأفكار تلقائياً
        function enhanceIdeaWithAI() {
            const desc = document.getElementById('ideaDescription');
            if (!desc.value.trim()) { alert('يرجى كتابة فكرة مصغرة أولاً لكي يقوم الذكاء الاصطناعي بتحسينها!'); return; }

            const current = desc.value;
            desc.value = `جاري تحليل وتحسين الفكرة بالذكاء الاصطناعي... 🪄`;
            
            setTimeout(() => {
                desc.value = `💡 [الفكرة المحسنة إعلامياً بواسطة الذكاء الاصطناعي]:\n${current}\n\n🎬 خطة التنفيذ والمهام المقترحة:\n1. مسار التصوير: تغطية زوايا متعددة ومقابلات حية.\n2. مسار المونتاج: إنتاج فيديو ختامي بدقة 4K خلال 24 ساعة.\n3. مسار الكتابة: صياغة التقرير الصحفي والتغريدات الحية.`;
                triggerConfetti();
            }, 1200);
        }

        // تحكم شريط الرفع المباشر مع النسبة المئوية (Progress Bar)
        async function uploadImagesWithProgress(e) {
            e.preventDefault();
            const files = document.getElementById('bulkImages').files;
            if (files.length === 0) return;

            const pContainer = document.getElementById('progressContainer');
            const pFill = document.getElementById('progressBarFill');
            const pText = document.getElementById('progressStatusText');

            pContainer.style.display = 'block';
            pText.style.display = 'block';

            for (let i = 1; i <= files.length; i++) {
                // محاكاة حساب النسبة المئوية لكل صورة
                await new Promise(r => setTimeout(r, 60));
                const percent = Math.round((i / files.length) * 100);
                pFill.style.width = percent + '%';
                pText.innerText = `جاري رفع وحفظ: ${percent}% (${i} من أصل ${files.length} صورة)`;
            }

            pText.innerText = `✅ تم رفع ${files.length} صورة بنجاح تام!`;
            triggerConfetti();
        }

        // المساعد الصوتي والشات مع AI
        let isListening = false;
        function openAIVoiceModal() { document.getElementById('aiVoiceModal').style.display = 'flex'; }
        function closeAIVoiceModal() { document.getElementById('aiVoiceModal').style.display = 'none'; }

        function toggleVoiceRecognition() {
            const sphere = document.getElementById('aiSphere');
            const status = document.getElementById('aiStatusText');
            const btn = document.getElementById('voiceRecordBtn');

            if (!('webkitSpeechRecognition' in window) && !('SpeechRecognition' in window)) {
                alert('متصفحك لا يدعم التعرف الصوتي المباشر، يمكنك استخدام الكتابة مع الذكاء الاصطناعي.');
                return;
            }

            const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
            const recognition = new SpeechRecognition();
            recognition.lang = 'ar-SA';

            if (!isListening) {
                recognition.start();
                isListening = true;
                sphere.classList.add('listening');
                status.innerText = '🎙️ جاري الاستماع إلى صوتك الآن... اتكلم!';
                btn.innerHTML = '<span>🛑 إيقاف الاستماع</span>';

                recognition.onresult = (event) => {
                    const text = event.results[0][0].transcript;
                    document.getElementById('aiTextInput').value = text;
                    sendAITextQuery();
                };

                recognition.onend = () => {
                    isListening = false;
                    sphere.classList.remove('listening');
                    btn.innerHTML = '<span>🎙️ بدء المحادثة الصوتية</span>';
                };
            }
        }

        function sendAITextQuery() {
            const query = document.getElementById('aiTextInput').value;
            const box = document.getElementById('aiResponseBox');
            if (!query) return;

            box.style.display = 'block';
            box.innerText = 'جاري تفكير الذكاء الاصطناعي... 🤖';

            setTimeout(() => {
                box.innerText = `🤖 [رد ذكاء MTU الاصطناعي]: أهلاً بك! بخصوص "${query}"، يقدم النادي الإعلامي بجامعة الطائف كفة الدعم عبر مسارات التصوير، المونتاج، والـ IT، ويمكنك رفع أفكارك مباشرة للجنة المشرفة.`;
                // نطق الرد صوتياً
                if ('speechSynthesis' in window) {
                    const speech = new SpeechSynthesisUtterance(box.innerText);
                    speech.lang = 'ar-SA';
                    window.speechSynthesis.speak(speech);
                }
            }, 1000);
        }

        function switchPage(pageId, btn) {
            document.querySelectorAll('.page-section').forEach(p => p.classList.remove('active'));
            document.querySelectorAll('.nav-btn').forEach(b => b.classList.remove('active'));
            document.getElementById(pageId).classList.add('active');
            btn.classList.add('active');
        }

        function submitIdea() {
            triggerConfetti();
            alert('تم حفظ الفكرة وتوثيقها بنجاح!');
        }
    </script>
</body>
</html>
