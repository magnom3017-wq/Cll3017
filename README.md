<!DOCTYPE html><html lang="ar" dir="rtl"><head><meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1"><title>مكتبتي — عالم الكتب بين يديك</title><link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;700&display=swap" rel="stylesheet"><style>*{box-sizing:border-box}body{font-family:"Cairo",sans-serif;margin:0;padding:20px;min-height:100vh;background:#111210;color:#fff;direction:rtl;overflow-x:hidden}header{display:flex;flex-direction:column;align-items:center;gap:6px;margin-bottom:18px}h1{margin:0;font-size:28px}h2{margin:0;font-weight:400;color:#d7c9b0;font-size:13px}#themeToggle{position:fixed;left:18px;top:18px;background:rgba(255,255,255,0.06);border:0;padding:10px;border-radius:50%;cursor:pointer;color:#fff;font-size:18px;backdrop-filter:blur(6px)}.search-wrap{max-width:980px;margin:0 auto;padding:8px 12px}.search-container{position:relative;text-align:right}.search-input{width:100%;padding:14px 16px;border-radius:30px;border:0;font-size:15px;background:linear-gradient(180deg,rgba(255,255,255,0.03),rgba(255,255,255,0.02));color:#fff;outline:none;box-shadow:inset 0 1px 0 rgba(255,255,255,0.02)}#suggestions{position:absolute;right:0;left:0;margin-top:10px;background:rgba(255,255,255,0.03);backdrop-filter:blur(6px);border-radius:12px;padding:8px;display:none;max-height:260px;overflow:auto;border:1px solid rgba(255,255,255,0.04)}.s-item{display:flex;gap:10px;align-items:center;padding:8px;border-radius:8px;cursor:pointer;transition:background .15s}.s-item:hover{background:rgba(255,255,255,0.03)}.s-item img{width:44px;height:56px;border-radius:6px;object-fit:cover;flex-shrink:0}.categories{display:flex;gap:8px;flex-wrap:wrap;justify-content:center;margin-top:14px}.cat-btn{background:transparent;border:1px solid rgba(255,255,255,0.06);color:#fff;padding:8px 14px;border-radius:20px;cursor:pointer;font-weight:700}.cat-btn.active{background:#b88956;color:#111;border:1px solid rgba(255,255,255,0.06)}.grid{display:flex;flex-wrap:wrap;gap:18px;justify-content:center;margin-top:20px}.card{width:200px;background:linear-gradient(180deg,rgba(255,255,255,0.03),rgba(255,255,255,0.02));padding:12px;border-radius:12px;cursor:pointer;transition:transform .18s,box-shadow .18s;border:1px solid rgba(255,255,255,0.03)}.card:hover{transform:translateY(-6px);box-shadow:0 14px 36px rgba(0,0,0,0.6)}.card img{width:100%;height:260px;object-fit:cover;border-radius:8px}.card h3{margin:8px 0 0 0;font-size:15px;color:#fff;text-align:center}.popup{position:fixed;inset:0;display:none;align-items:center;justify-content:center;z-index:999;background:linear-gradient(180deg,rgba(2,2,2,0.6),rgba(2,2,2,0.85))}.popup .box{width:92%;max-width:720px;background:linear-gradient(180deg,#1a1a1a,#0d0d0d);border-radius:12px;padding:18px;border:1px solid rgba(255,255,255,0.04);display:flex;gap:12px;align-items:flex-start}.pop-cover{width:140px;height:190px;border-radius:6px;object-fit:cover;flex-shrink:0}.pop-info{flex:1;color:#fff}.pop-title{font-size:18px;margin:0 0 8px 0}.pop-actions{display:flex;gap:10px;margin-top:12px}.btn{padding:10px 16px;border-radius:10px;border:0;cursor:pointer;font-weight:700}.btn.read{background:#fff;color:#111}.btn.dl{background:linear-gradient(90deg,#b88956,#70502f);color:#fff}.close-x{background:transparent;border:0;color:#fff;font-size:22px;margin-left:8px;cursor:pointer}.footer-note{margin-top:26px;color:#cdbfa6;font-size:13px;text-align:center}@media(max-width:520px){.card{width:95%}.card img{height:220px}.pop-cover{display:none}.popup .box{flex-direction:column;align-items:center}}</style></head><body>
<button id="themeToggle" title="تبديل الوضع">🌙</button>
<header>
  <h1>📚 مكتبتي</h1>
  <h2>🌟 عالم الكتب بين يديك</h2>
</header>

<div class="search-wrap">
  <div class="search-container">
    <input id="search" class="search-input" placeholder="اكتب اسم الكتاب للبحث..." autocomplete="off">
    <div id="suggestions"></div>
  </div>

  <div class="categories" id="cats">
    <button class="cat-btn active" data-cat="all">الكل</button>
    <button class="cat-btn" data-cat="novels">روايات</button>
    <button class="cat-btn" data-cat="science">علمية</button>
    <button class="cat-btn" data-cat="history">تاريخية</button>
  </div>

  <div class="grid" id="grid"></div>

  <p class="footer-note">🌍 الموقع يعتمد على أمثلة تجريبية — يمكنك استبدال الكتب بروابطك لاحقًا.</p>
</div>

<!-- النافذة المنبثقة -->
<div id="popup" class="popup" onclick="if(event.target===this)closePopup()">
  <div class="box" role="dialog" aria-modal="true">
    <img id="popCover" class="pop-cover" src="" alt="غلاف">
    <div class="pop-info">
      <button class="close-x" onclick="closePopup()">✖</button>
      <h3 id="popTitle" class="pop-title"></h3>
      <div id="popDesc" style="color:#d7c9b0;font-size:13px"></div>
      <div class="pop-actions">
        <button id="readBtn" class="btn read">📖 قراءة</button>
        <button id="dlBtn" class="btn dl">⬇️ تحميل</button>
      </div>
    </div>
  </div>
</div>

<script>
/* --- بيانات تجريبية: استبدلها بروابطك لاحقًا --- */
const books=[
{title:"الخيميائي — باولو كويلو",category:"novels",pdf:"https://www.w3.org/WAI/ER/tests/xhtml/testfiles/resources/pdf/dummy.pdf",cover:"https://via.placeholder.com/400x600?text=الخيميائي"},
{title:"الكون — كارل ساغان",category:"science",pdf:"https://www.w3.org/WAI/ER/tests/xhtml/testfiles/resources/pdf/dummy.pdf",cover:"https://via.placeholder.com/400x600?text=الكون"},
{title:"العرب قبل الإسلام — جواد علي",category:"history",pdf:"https://www.w3.org/WAI/ER/tests/xhtml/testfiles/resources/pdf/dummy.pdf",cover:"https://via.placeholder.com/400x600?text=العرب+قبل+الإسلام"},
{title:"تعليم البرمجة",category:"science",pdf:"https://www.w3.org/WAI/ER/tests/xhtml/testfiles/resources/pdf/dummy.pdf",cover:"https://via.placeholder.com/400x600?text=برمجة"},
{title:"قصص الأطفال المختارة",category:"novels",pdf:"https://www.w3.org/WAI/ER/tests/xhtml/testfiles/resources/pdf/dummy.pdf",cover:"https://via.placeholder.com/400x600?text=قصص+الأطفال"}
];

const grid=document.getElementById('grid'), suggestions=document.getElementById('suggestions'), search=document.getElementById('search'), popup=document.getElementById('popup'), popCover=document.getElementById('popCover'),popTitle=document.getElementById('popTitle'),popDesc=document.getElementById('popDesc'),readBtn=document.getElementById('readBtn'),dlBtn=document.getElementById('dlBtn');
let currentBook=null;

function renderGrid(filter='all'){
  grid.innerHTML='';
  books.forEach((b,i)=>{
    if(filter==='all'||b.category===filter){
      const div=document.createElement('div');div.className='card';div.dataset.index=i;
      div.innerHTML=`<img loading="lazy" src="${b.cover}" alt="${b.title}"><h3>${b.title}</h3>`;
      div.onclick=()=>openPopup(i);
      grid.appendChild(div);
    }
  });
}
function openPopup(i){
  currentBook=books[i];
  popCover.src=currentBook.cover;
  popTitle.textContent=currentBook.title;
  popDesc.textContent=`الفئة: ${currentBook.category}`;
  readBtn.onclick=()=>{window.open('reader.html?pdf='+encodeURIComponent(currentBook.pdf)+'&title='+encodeURIComponent(currentBook.title),'_blank');};
  dlBtn.onclick=()=>{window.open(currentBook.pdf,'_blank');};
  popup.style.display='flex';
  setTimeout(()=>popup.querySelector('.box').style.transform='translateY(0)',80);
}
function closePopup(){popup.style.display='none';}
renderGrid();

/* الفلاتر */
document.getElementById('cats').addEventListener('click',e=>{if(e.target.classList.contains('cat-btn')){document.querySelectorAll('.cat-btn').forEach(b=>b.classList.remove('active'));e.target.classList.add('active');renderGrid(e.target.dataset.cat);}});

/* البحث واقتراحات */
search.addEventListener('input',function(){
  const q=this.value.trim().toLowerCase();
  suggestions.innerHTML='';if(!q){suggestions.style.display='none';return;}
  const matched=books.filter(b=>b.title.toLowerCase().includes(q));
  if(!matched.length){suggestions.style.display='none';return;}
  matched.forEach((b,i)=>{const item=document.createElement('div');item.className='s-item';item.innerHTML=`<img src="${b.cover}" alt=""><div style="text-align:right"><div style="font-weight:700">${b.title}</div><div style="font-size:12px;color:#cdbfa6">${b.category}</div></div>`;item.onclick=()=>{search.value=b.title;suggestions.style.display='none';displaySearchResult(b.title);};suggestions.appendChild(item);});
  suggestions.style.display='block';
});
document.addEventListener('click',e=>{if(!e.target.closest('.search-container'))suggestions.style.display='none';});

/* عند اختيار اقتراح أو بحث كامل */
function displaySearchResult(title){
  grid.innerHTML='';const filtered=books.filter(b=>b.title===title);if(!filtered.length) return;
  filtered.forEach((b,i)=>{const div=document.createElement('div');div.className='card';div.innerHTML=`<img loading="lazy" src="${b.cover}" alt="${b.title}"><h3>${b.title}</h3>`;div.onclick=()=>openPopup(books.indexOf(b));grid.appendChild(div);});
}

/* زر تبديل الوضع (يحافظ محليًا) */
const themeBtn=document.getElementById('themeToggle');const saved=localStorage.getItem('mk-theme');if(saved==='dark'||!saved){document.body.style.background='#0f0f0f';}else{document.body.style.background='#fff';document.body.style.color='#111';}themeBtn.onclick=()=>{if(document.body.dataset.light==='1'){document.body.dataset.light='0';document.body.style.background='#0f0f0f';document.body.style.color='#fff';localStorage.setItem('mk-theme','dark');themeBtn.textContent='🌙';}else{document.body.dataset.light='1';document.body.style.background='#fff';document.body.style.color='#111';localStorage.setItem('mk-theme','light');themeBtn.textContent='☀️';}};</script>
</body></html>
لا شيء
