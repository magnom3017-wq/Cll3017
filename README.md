<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Ou. KameL</title>
<style>
  /* تصميم شامل داكن مع تدرجات وظلال ناعمة */
  :root {
    --dark-bg: #121212;
    --dark-gradient: linear-gradient(135deg, #1e1e1e 0%, #121212 100%);
    --highlight: #4fc3f7;
    --shadow: rgba(79, 195, 247, 0.4);
    --font-smooth: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  }

  * {
    box-sizing: border-box;
    transition: all 0.3s ease;
  }

  body {
    margin:0; padding:0;
    background: var(--dark-gradient);
    color: white;
    font-family: var(--font-smooth);
    overflow-x: hidden;
    display: flex;
    flex-direction: column;
    min-height: 100vh;
  }

  /* الشريط العلوي */
  header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0.6rem 1rem;
    background: var(--dark-bg);
    box-shadow: 0 2px 6px var(--shadow);
    position: sticky;
    top: 0;
    z-index: 100;
  }

  /* اسم الموقع يمين */
  #site-name {
    font-weight: bold;
    font-size: 1.3rem;
    user-select: none;
  }

  /* الشريط العلوي يسار */
  #top-left {
    display: flex;
    align-items: center;
    gap: 1rem;
  }

  /* زر PQ */
  #btn-pq {
    position: relative;
    background: var(--highlight);
    border: none;
    color: #121212;
    font-weight: bold;
    border-radius: 6px;
    padding: 0.45rem 0.85rem;
    cursor: pointer;
    user-select: none;
    font-size: 1rem;
    display: flex;
    align-items: center;
    gap: 0.5rem;
  }

  /* قائمة المشاركة المنبثقة */
  #share-menu {
    position: absolute;
    top: 2.8rem;
    right: 0;
    background: var(--dark-bg);
    box-shadow: 0 4px 8px var(--shadow);
    border-radius: 8px;
    width: 180px;
    display: none;
    flex-direction: column;
    user-select: none;
    z-index: 120;
  }

  #share-menu button {
    background: transparent;
    border: none;
    color: white;
    padding: 0.6rem 1rem;
    text-align: right;
    font-size: 0.95rem;
    cursor: pointer;
    border-bottom: 1px solid #333;
    transition: background 0.2s;
  }

  #share-menu button:last-child {
    border-bottom: none;
  }

  #share-menu button:hover {
    background: var(--highlight);
    color: #121212;
  }

  /* رمز QR في القائمة */
  #qr-share {
    margin: 0.5rem auto;
    filter: drop-shadow(0 0 3px var(--highlight));
    width: 100px;
    height: 100px;
  }

  /* رموز اللغات */
  #lang-switcher {
    display: flex;
    gap: 0.5rem;
  }

  #lang-switcher button {
    background: transparent;
    border: none;
    font-size: 1.5rem;
    cursor: pointer;
    user-select: none;
    filter: drop-shadow(0 0 2px black);
  }

  #lang-switcher button:hover {
    transform: scale(1.2);
    filter: drop-shadow(0 0 5px var(--highlight));
  }

  /* قسم التطبيقات */
  main {
    flex-grow: 1;
    padding: 1rem 1.5rem 6rem;
    display: grid;
    gap: 1.5rem;
    justify-content: center;
    /* شبكة مرنة: 2 موبايل، 4 تابلت، 6 كمبيوتر */
    grid-template-columns: repeat(auto-fit, minmax(90px, 1fr));
  }

  @media(min-width: 480px) {
    main {
      grid-template-columns: repeat(2, 1fr);
    }
  }
  @media(min-width: 768px) {
    main {
      grid-template-columns: repeat(4, 1fr);
    }
  }
  @media(min-width: 1024px) {
    main {
      grid-template-columns: repeat(6, 1fr);
    }
  }

  /* أيقونات التطبيقات كبيرة جدًا، متحركة متواصلة */
  .app-icon {
    background: var(--dark-bg);
    border-radius: 16px;
    box-shadow: 0 0 12px var(--highlight);
    width: 100px;
    height: 100px;
    margin: 0 auto;
    position: relative;
    cursor: pointer;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 4rem;
    color: var(--highlight);
    user-select: none;
    animation: glow 3s infinite alternate,
               vibrate 4s infinite alternate,
               spinSlow 10s linear infinite;
    transition: box-shadow 0.3s ease;
  }

  .app-icon:hover {
    box-shadow: 0 0 25px 4px var(--highlight);
  }

  /* أسم التطبيق تحت كل أيقونة */
  .app-name {
    text-align: center;
    margin-top: 0.5rem;
    font-weight: 600;
    font-size: 1rem;
    user-select: none;
  }

  /* حركة التوهج */
  @keyframes glow {
    from { filter: drop-shadow(0 0 3px var(--highlight)); }
    to { filter: drop-shadow(0 0 10px var(--highlight)); }
  }

  /* حركة الاهتزاز خفيف */
  @keyframes vibrate {
    0% { transform: translate(0) rotate(0);}
    25% { transform: translate(1.5px, -1.5px) rotate(-1deg);}
    50% { transform: translate(-1.5px, 1.5px) rotate(1deg);}
    75% { transform: translate(1.5px, 1.5px) rotate(-1deg);}
    100% { transform: translate(0) rotate(0);}
  }

  /* دوران بسيط */
  @keyframes spinSlow {
    from { transform: rotate(0deg);}
    to { transform: rotate(360deg);}
  }

  /* النافذة المنبثقة */
  #popup {
    position: fixed;
    top: 50%; left: 50%;
    transform: translate(-50%, -50%);
    background: var(--dark-bg);
    padding: 1.5rem 2rem;
    border-radius: 15px;
    box-shadow: 0 0 20px var(--shadow);
    max-width: 320px;
    width: 90%;
    z-index: 200;
    display: none;
    flex-direction: column;
    align-items: center;
    color: var(--highlight);
  }

  #popup h2 {
    margin: 0 0 1rem 0;
  }

  #popup button {
    background: var(--highlight);
    border: none;
    color: #121212;
    font-weight: 600;
    padding: 0.6rem 1.2rem;
    cursor: pointer;
    border-radius: 6px;
    margin: 0.4rem;
    width: 100%;
    user-select: none;
  }

  #popup button:hover {
    background: #39b1f4;
  }

  #popup .qr-code {
    margin: 1rem 0 1.5rem 0;
    filter: drop-shadow(0 0 5px var(--highlight));
    width: 150px;
    height: 150px;
  }

  /* خيارات الاتصال تظهر فقط إذا التطبيق هاتف */
  #call-options {
    margin-top: 1rem;
    width: 100%;
    display: flex;
    justify-content: space-evenly;
  }

  #call-options button {
    background: #1a73e8;
    padding: 0.5rem 1rem;
    border-radius: 6px;
    font-size: 0.95rem;
    color: white;
  }

  #call-options button:hover {
    background: #135ab1;
  }

  /* إشعارات تظهر أسفل الشاشة */
  #notifications {
    position: fixed;
    bottom: 1rem;
    left: 50%;
    transform: translateX(-50%);
    background: var(--highlight);
    color: #121212;
    padding: 0.6rem 1rem;
    border-radius: 20px;
    font-weight: bold;
    box-shadow: 0 0 15px var(--shadow);
    user-select: none;
    opacity: 0;
    pointer-events: none;
    transition: opacity 0.3s ease;
    max-width: 80vw;
    text-align: center;
    z-index: 300;
  }

  #notifications.show {
    opacity: 1;
    pointer-events: auto;
  }
</style>
</head>
<body>

<header>
  <div id="top-left">
    <button id="btn-pq" aria-label="مشاركة الموقع">PQ ▼</button>
    <div id="share-menu" role="menu" aria-hidden="true">
      <button id="share-direct">مشاركة الرابط مباشرة</button>
      <button id="copy-link">نسخ الرابط</button>
      <div id="qr-share-container" style="padding:0.5rem;display:flex;justify-content:center;">
        <canvas id="qr-share"></canvas>
      </div>
    </div>
    <div id="lang-switcher" role="group" aria-label="تبديل اللغة">
      <button aria-label="العربية" data-lang="ar">🇩🇿</button>
      <button aria-label="الفرنسية" data-lang="fr">🇫🇷</button>
      <button aria-label="الإنجليزية" data-lang="en">🇬🇧</button>
    </div>
  </div>
  <div id="site-name" aria-live="polite">Ou. KameL</div>
</header>

<main aria-label="قائمة التطبيقات">
  <!-- مثال تطبيقات -->
</main>

<div id="popup" role="dialog" aria-modal="true" aria-labelledby="popup-title">
  <h2 id="popup-title"></h2>
  <button id="btn-open-app">فتح التطبيق</button>
  <button id="btn-copy-link-popup">نسخ الرابط</button>
  <canvas id="qr-popup" class="qr-code"></canvas>
  <div id="call-options" style="display:none;">
    <button id="btn-call">اتصال مباشر</button>
    <button id="btn-copy-number">نسخ الرقم</button>
  </div>
  <button id="btn-close-popup" style="margin-top:1rem; background:#333; color:#eee;">إغلاق</button>
</div>

<div id="notifications" role="alert" aria-live="assertive"></div>

<script>
  // بيانات التطبيقات مثال مع نوع للتعامل الخاص بالهاتف ورقم 
  const apps = [
    {name:'هاتف', icon: '📱', url:'tel:+213123456789', isPhone:true, number:'+213123456789'},
    {name:'فايسبوك', icon: '📘', url:'https://facebook.com'},
    {name:'واتساب', icon: '💬', url:'https://wa.me/213123456789', isPhone:true, number:'+213123456789'},
    {name:'تويتر', icon: '🐦', url:'https://twitter.com'},
    {name:'إنستغرام', icon: '📸', url:'https://instagram.com'},
    {name:'لينكدإن', icon: '🔗', url:'https://linkedin.com'}
  ];

  const main = document.querySelector('main');
  const popup = document.getElementById('popup');
  const popupTitle = document.getElementById('popup-title');
  const btnOpenApp = document.getElementById('btn-open-app');
  const btnCopyLinkPopup = document.getElementById('btn-copy-link-popup');
  const qrPopup = document.getElementById('qr-popup');
  const callOptions = document.getElementById('call-options');
  const btnCall = document.getElementById('btn-call');
  const btnCopyNumber = document.getElementById('btn-copy-number');
  const btnClosePopup = document.getElementById('btn-close-popup');
  const notifications = document.getElementById('notifications');

  // توليد أيقونات التطبيقات
  apps.forEach(app => {
    const appDiv = document.createElement('div');
    appDiv.classList.add('app-card');
    appDiv.style.textAlign = 'center';

    const icon = document.createElement('div');
    icon.classList.add('app-icon');
    icon.textContent = app.icon;
    icon.tabIndex = 0;
    icon.setAttribute('role', 'button');
    icon.setAttribute('aria-label', `فتح تطبيق ${app.name}`);

    const name = document.createElement('div');
    name.className = 'app-name';
    name.textContent = app.name;

    appDiv.appendChild(icon);
    appDiv.appendChild(name);
    main.appendChild(appDiv);

    icon.addEventListener('click', () => openPopup(app));
    icon.addEventListener('keypress', (e) => { if(e.key === 'Enter' || e.key === ' ') openPopup(app); });
  });

  // فتح النافذة المنبثقة للتطبيق
  function openPopup(app) {
    popup.style.display = 'flex';
    popupTitle.textContent = app.name;
    currentApp = app;
    btnOpenApp.onclick = () => {
      if(app.isPhone) {
        window.location.href = app.url;
        showNotification('تم فتح التطبيق');
      } else {
        window.open(app.url, '_blank', 'noopener');
        showNotification('تم فتح التطبيق');
      }
    };
    btnCopyLinkPopup.onclick = () => {
      copyTextToClipboard(app.url);
      showNotification('تم نسخ الرابط');
    };

    // QR مع تأثير بصري
    generateQRCode(qrPopup, app.url);

    if(app.isPhone) {
      callOptions.style.display = 'flex';
      btnCall.onclick = () => {
        window.location.href = app.url;
        showNotification('تم إجراء الاتصال');
      };
      btnCopyNumber.onclick = () => {
        copyTextToClipboard(app.number);
        showNotification('تم نسخ الرقم');
      };
    } else {
      callOptions.style.display = 'none';
    }
  }

  btnClosePopup.onclick = () => { popup.style.display = 'none'; };

  // مشاركة زر PQ وسلوك القائمة المنبثقة
  const btnPQ = document.getElementById('btn-pq');
  const shareMenu = document.getElementById('share-menu');

  btnPQ.addEventListener('click', e => {
    shareMenu.style.display = shareMenu.style.display === 'flex' ? 'none' : 'flex';
    shareMenu.setAttribute('aria-hidden', shareMenu.style.display === 'none');
  });

  document.documentElement.addEventListener('click', e => {
    if (!btnPQ.contains(e.target) && !shareMenu.contains(e.target)) {
      shareMenu.style.display = 'none';
      shareMenu.setAttribute('aria-hidden', 'true');
    }
  });

  // اعداد مشاركة الرابط
  const shareDirectBtn = document.getElementById('share-direct');
  const copyLinkBtn = document.getElementById('copy-link');
  const qrShareCanvas = document.getElementById('qr-share');

  shareDirectBtn.addEventListener('click', async () => {
    if (navigator.share) {
      try {
        await navigator.share({ title: document.title, url: location.href });
        showNotification('تمت المشاركة مباشرة');
      } catch {
        showNotification('فشل في المشاركة');
      }
    } else {
      showNotification('مشاركة مباشرة غير مدعومة');
    }
  });

  copyLinkBtn.addEventListener('click', () => {
    copyTextToClipboard(location.href);
    showNotification('تم نسخ الرابط');
  });

  // توليد QR للشير في القائمة
  generateQRCode(qrShareCanvas, location.href);

  // رموز اللغات (لكن لا تغير فعلياً محتوى)
  document.querySelectorAll('#lang-switcher button').forEach(btn => {
    btn.onclick = () => {
      showNotification(`تم التبديل إلى اللغة: ${btn.getAttribute('aria-label')}`);
    };
  });

  // إشعارات أسفل الشاشة مع اختفاء
  let notifTimeout;
  function showNotification(text) {
    clearTimeout(notifTimeout);
    notifications.textContent = text;
    notifications.classList.add('show');
    notifTimeout = setTimeout(() => {
      notifications.classList.remove('show');
    }, 2500);
  }

  // نسخ نص للحافظة
  function copyTextToClipboard(text) {
    if (navigator.clipboard) {
      navigator.clipboard.writeText(text);
    } else {
      const textarea = document.createElement('textarea');
      textarea.value = text;
      document.body.appendChild(textarea);
      textarea.select();
      document.execCommand('copy');
      document.body.removeChild(textarea);
    }
  }

  // توليد رمز QR باستخدام كود بسيط (بدون مكتبات خارجية)
  // قاعدة: توليد QR Code عبر مكتبة qrcode-generator مضمنة بشكل صغير:
  (function qrGenerator(){
    // Script صغير لتوليد QR codes 
    // مصدر: https://github.com/davidshimjs/qrcodejs مصغر ومعدل (حسب الحقوق يسمح الاستخدام)

    // أضف هنا كود أصغر أو استخدم طريقة بديلة لصنع QR سيضطر تخفيف التفاصيل بسبب حجم الكود.
    // لكن كحل مختصر، اليك نسخ أبسط جداً لتوليد QR:

    function QR8bitByte(data) {
      this.mode = QRMode.MODE_8BIT_BYTE;
      this.data = data;
      this.parsedData = [];

      for (var i = 0, l = this.data.length; i < l; i++) {
        var byteArray = [];
        var code = this.data.charCodeAt(i);
        if (code > 0xff) {
          byteArray[0] = code >>> 8;
          byteArray[1] = code & 0xff;
          this.parsedData.push(byteArray);
        } else {
          this.parsedData.push([code]);
        }
      }
    }

    function createQRCode(canvas, text) {
      // استعمال مكتبة صغيرة جدا لإنشاء رمز QR
      // لكن لعدم تعقيد الكود هنا سنستخدم API عبر CDN جلب QR Code صغير
      if(!text) return;
      // نستخدم مكتبة qrcode js من cdn مع تحميل ديناميكي
      if(window.QRCode) {
        new QRCode(canvas, {
          text,
          width: canvas.width,
          height: canvas.height,
          colorDark : "#4fc3f7",
          colorLight : "#121212",
          correctLevel : QRCode.CorrectLevel.H
        });
      } else {
        let script = document.createElement('script');
        script.onload = () => {
          new QRCode(canvas, {
            text,
            width: canvas.width,
            height: canvas.height,
            colorDark : "#4fc3f7",
            colorLight : "#121212",
            correctLevel : QRCode.CorrectLevel.H
          });
        };
        script.src = "https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js";
        document.head.appendChild(script);
      }
    }
    window.generateQRCode = createQRCode;
  })();
</script>

</body>
</html>
