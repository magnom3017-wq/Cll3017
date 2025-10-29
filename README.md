<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Ou. KameL</title>
<style>
  *{margin:0;padding:0;box-sizing:border-box;font-family:"Poppins",sans-serif;}
  body{background:#0d0d0d;color:#fff;display:flex;flex-direction:column;align-items:center;min-height:100vh;padding:20px;position:relative;}
  header{width:100%;display:flex;justify-content:space-between;align-items:center;margin-bottom:30px}
  .site-name{font-size:1.8em;font-weight:700;color:#00bfff;}
  .top-left{display:flex;align-items:center;gap:10px}
  button{background:#1a1a1a;color:#fff;border:none;outline:none;padding:10px 14px;border-radius:10px;cursor:pointer;transition:.3s;font-weight:700;font-size:16px;}
  button:hover{background:#333;}
  .lang-icon{font-size:22px;cursor:pointer;transition:.3s;}
  .lang-icon:hover{transform:scale(1.2);}
  .apps-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:20px;max-width:480px;width:100%;}
  .app-card{background:#1a1a1a;border-radius:20px;padding:20px;text-align:center;transition:.5s;cursor:pointer;position:relative;overflow:hidden;}
  .app-card:hover{background:#222;}
  .app-card img{width:80px;height:80px;object-fit:contain;margin-bottom:10px;animation:float 3s ease-in-out infinite;}
  .app-card p{font-size:1.1em;font-weight:600;}
  @keyframes float{
    0%,100%{transform:translateY(0px) rotate(0deg);}
    50%{transform:translateY(-10px) rotate(5deg);}
  }
  .modal{position:fixed;top:0;left:0;width:100%;height:100%;background:rgba(0,0,0,.7);display:flex;justify-content:center;align-items:center;visibility:hidden;opacity:0;transition:.3s;z-index:100;}
  .modal.active{visibility:visible;opacity:1;}
  .modal-content{background:#1a1a1a;padding:25px;border-radius:20px;text-align:center;width:300px;position:relative;box-shadow:0 0 20px #00bfff;}
  .modal-content h3{margin-bottom:15px;color:#00bfff;font-size:1.4em;}
  .modal-content button{margin:8px 0;width:100%;padding:10px;border-radius:12px;font-weight:600;}
  .qr{margin-top:15px;}
  .qr img{width:140px;height:140px;}
  .notification{position:fixed;bottom:20px;left:50%;transform:translateX(-50%);background:#00bfff;color:#0d0d0d;padding:12px 20px;border-radius:25px;font-weight:600;opacity:0;transition:.5s;pointer-events:none;z-index:200;}
  @media(min-width:768px){.apps-grid{grid-template-columns:repeat(4,1fr);}}
  @media(min-width:1024px){.apps-grid{grid-template-columns:repeat(6,1fr);}}
</style>
</head>
<body>

<header>
  <div class="top-left">
    <button id="shareBtn">PQ</button>
    <span class="lang-icon" data-lang="ar">🇩🇿</span>
    <span class="lang-icon" data-lang="fr">🇫🇷</span>
    <span class="lang-icon" data-lang="en">🇬🇧</span>
  </div>
  <div class="site-name">Ou. KameL</div>
</header>

<section class="apps-grid" id="apps"></section>

<div class="modal" id="modal">
  <div class="modal-content">
    <h3 id="appName"></h3>
    <button id="openApp">فتح التطبيق</button>
    <button id="copyLink">📋 نسخ الرابط</button>
    <div class="qr" id="qrCode"></div>
    <button onclick="closeModal()">إغلاق</button>
  </div>
</div>

<div class="notification" id="notification"></div>

<script src="https://cdn.jsdelivr.net/npm/qrcodejs/qrcode.min.js"></script>
<script>
const apps=[
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

function showNotification(msg){
  const notif=document.getElementById("notification");
  notif.textContent=msg;
  notif.style.opacity="1";
  setTimeout(()=>{notif.style.opacity="0";},2000);
}

function openModal(app){
  appName.textContent=app.name;
  currentLink=app.link;
  modal.classList.add("active");
  qrDiv.innerHTML="";
  new QRCode(qrDiv,{text:app.link,width:140,height:140});
}

function closeModal(){modal.classList.remove("active");}

openApp.onclick=()=>window.open(currentLink,"_blank");
copyLink.onclick=()=>{
  navigator.clipboard.writeText(currentLink);
  showNotification("تم نسخ الرابط ✅");
};

document.getElementById("shareBtn").onclick=async()=>{
  const shareData={title:"Ou. KameL",text:"كل حساباتي وروابطي في مكان واحد 👇",url:window.location.href};
  try{
    await navigator.share(shareData);
  }catch(err){
    navigator.clipboard.writeText(window.location.href);
    showNotification("تم نسخ رابط الموقع ✅");
  }
};

document.querySelectorAll(".lang-icon").forEach(el=>{
  el.onclick=()=>showNotification("تم اختيار اللغة: "+el.dataset.lang);
});
</script>
</body>
</html>
