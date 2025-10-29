<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Ou. KameL</title>
  <style>
    *{margin:0;padding:0;box-sizing:border-box;font-family:"Poppins",sans-serif}
    body{background:#0d0d0d;color:#fff;display:flex;flex-direction:column;align-items:center;min-height:100vh;padding:20px}
    header{width:100%;display:flex;justify-content:space-between;align-items:center;margin-bottom:30px}
    .site-name{font-size:1.6em;font-weight:700;color:#00bfff}
    .top-left{display:flex;align-items:center;gap:10px}
    button,select{background:#1a1a1a;color:#fff;border:none;outline:none;padding:8px 14px;border-radius:10px;cursor:pointer;transition:.3s}
    button:hover,select:hover{background:#333}
    .apps-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:20px;max-width:400px;width:100%}
    .app-card{background:#1a1a1a;border-radius:15px;padding:20px;text-align:center;transition:.3s;cursor:pointer}
    .app-card:hover{background:#333}
    .app-card img{width:60px;height:60px;object-fit:contain;margin-bottom:10px}
    .modal{position:fixed;top:0;left:0;width:100%;height:100%;background:rgba(0,0,0,.7);display:flex;justify-content:center;align-items:center;visibility:hidden;opacity:0;transition:.3s}
    .modal.active{visibility:visible;opacity:1}
    .modal-content{background:#1a1a1a;padding:25px;border-radius:15px;text-align:center;width:280px}
    .modal-content h3{margin-bottom:15px;color:#00bfff}
    .modal-content button{margin:8px 0;width:100%}
    .qr{margin-top:15px}
    .qr img{width:130px;height:130px}
    @media (min-width:768px){.apps-grid{grid-template-columns:repeat(4,1fr)}}
    @media (min-width:1024px){.apps-grid{grid-template-columns:repeat(6,1fr)}}
  </style>
</head>
<body>
  <header>
    <div class="top-left">
      <button id="shareBtn">🔗 مشاركة</button>
      <select id="langSelect">
        <option value="ar">العربية</option>
        <option value="fr">Français</option>
        <option value="en">English</option>
      </select>
    </div>
    <div class="site-name">Ou. KameL</div>
  </header>

  <section class="apps-grid" id="apps">
    <!-- App icons -->
  </section>

  <!-- Modal -->
  <div class="modal" id="modal">
    <div class="modal-content">
      <h3 id="appName"></h3>
      <button id="openApp">فتح التطبيق</button>
      <button id="copyLink">📋 نسخ الرابط</button>
      <div class="qr" id="qrCode"></div>
      <button onclick="closeModal()">إغلاق</button>
    </div>
  </div>

  <script src="https://cdn.jsdelivr.net/npm/qrcodejs/qrcode.min.js"></script>
  <script>
    const apps = [
      {name:"Facebook", icon:"https://cdn-icons-png.flaticon.com/512/733/733547.png", link:"https://www.facebook.com/share/1DtUpF5Pwy/"},
      {name:"Instagram", icon:"https://cdn-icons-png.flaticon.com/512/2111/2111463.png", link:"https://www.instagram.com/kamola_463?igsh=ZWVybThwa2ZhZzB0"},
      {name:"WhatsApp", icon:"https://cdn-icons-png.flaticon.com/512/733/733585.png", link:"https://wa.me/213776274508"},
      {name:"Telegram", icon:"https://cdn-icons-png.flaticon.com/512/2111/2111644.png", link:"https://t.me/ou_kamel"},
      {name:"Snapchat", icon:"https://cdn-icons-png.flaticon.com/512/2111/2111688.png", link:"https://www.snapchat.com/add/kamola252903?share_id=ToNKEy4L3oA&locale=ar-EG"},
      {name:"TikTok", icon:"https://cdn-icons-png.flaticon.com/512/3046/3046126.png", link:"https://www.tiktok.com/@kamola.3017?_t=ZS-90xX5Zlt75T&_r=1"},
      {name:"YouTube", icon:"https://cdn-icons-png.flaticon.com/512/1384/1384060.png", link:"https://www.youtube.com/@kamola3017"},
      {name:"Messenger", icon:"https://cdn-icons-png.flaticon.com/512/2111/2111680.png", link:"https://m.me/シシ"},
      {name:"Email", icon:"https://cdn-icons-png.flaticon.com/512/732/732200.png", link:"mailto:magnom3017@gmail.com"},
      {name:"Phone", icon:"https://cdn-icons-png.flaticon.com/512/597/597177.png", link:"tel:0776274508"}
    ];

    const appsContainer=document.getElementById("apps");
    apps.forEach(app=>{
      const card=document.createElement("div");
      card.className="app-card";
      card.innerHTML=`<img src="${app.icon}" alt="${app.name}"><p>${app.name}</p>`;
      card.onclick=()=>openModal(app);
      appsContainer.appendChild(card);
    });

    const modal=document.getElementById("modal");
    const appName=document.getElementById("appName");
    const openApp=document.getElementById("openApp");
    const copyLink=document.getElementById("copyLink");
    const qrDiv=document.getElementById("qrCode");
    let currentLink="";

    function openModal(app){
      appName.textContent=app.name;
      currentLink=app.link;
      modal.classList.add("active");
      qrDiv.innerHTML="";
      new QRCode(qrDiv,{text:app.link,width:130,height:130});
    }

    function closeModal(){modal.classList.remove("active")}

    openApp.onclick=()=>window.open(currentLink,"_blank");
    copyLink.onclick=()=>{
      navigator.clipboard.writeText(currentLink);
      alert("تم نسخ الرابط ✅");
    };

    // Share Button
    document.getElementById("shareBtn").onclick=async()=>{
      const shareData={title:"Ou. KameL",text:"كل حساباتي وروابطي في مكان واحد 👇",url:window.location.href};
      try{
        await navigator.share(shareData);
      }catch(err){
        navigator.clipboard.writeText(window.location.href);
        alert("تم نسخ رابط الموقع ✅");
      }
    };

    // Language Selector (placeholder)
    document.getElementById("langSelect").onchange=(e)=>{
      alert("تم اختيار اللغة: "+e.target.value);
    };
  </script>
</body>
</html>
