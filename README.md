<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>مكتبة الكتب</title>
<style>
body{font-family:Arial,sans-serif;background:#111;color:#fff;padding:20px;}
.grid{display:flex;flex-wrap:wrap;gap:12px;justify-content:center;margin-top:20px}
.card{width:30%;max-width:200px;background:#222;padding:12px;border-radius:12px;cursor:pointer;text-align:center;}
.card:hover{background:#333;transform:translateY(-6px);}
.popup{position:fixed;inset:0;background:rgba(0,0,0,0.85);display:none;justify-content:center;align-items:center;z-index:999;}
.popup .box{background:#111;padding:20px;border-radius:12px;width:80%;max-width:700px;display:flex;flex-direction:column;align-items:center;}
.popup iframe{width:100%;height:60vh;border:0;margin-top:10px;}
button{padding:8px 12px;margin:5px;border:none;border-radius:8px;cursor:pointer;}
.btn-close{background:#444;color:#fff;}
.btn-dl{background:linear-gradient(90deg,#b88956,#70502f);color:#fff;}
</style>
</head>
<body>

<h2 style="text-align:center;">مكتبة الكتب</h2>
<div class="grid" id="grid"></div>

<div id="popup" class="popup">
  <div class="box">
    <h3 id="bookTitle"></h3>
    <iframe id="pdfFrame"></iframe>
    <div>
      <button class="btn-close" onclick="closePopup()">إغلاق</button>
      <a id="downloadBtn" href="#" target="_blank"><button class="btn-dl">تحميل الكتاب</button></a>
    </div>
  </div>
</div>

<script>
const books = [
  {
    title: "لاب الغني و لاب الفقير",
    category: "novels",
    pdf: "https://www.dropbox.com/scl/fi/nqkr8rn3roy9fb4vqjnlr/1UaGTQGy_M8fpxl03u2rcHA6G2uRDZeUz.pdf?rlkey=m2xuife3zdn2h2xv1xa6wi4qy&st=77ro8sn1&dl=1",
    cover: "https://via.placeholder.com/400x600?text=لاب+الغني+و+لاب+الفقير"
  }
];

const grid = document.getElementById('grid');
const popup = document.getElementById('popup');
const bookTitle = document.getElementById('bookTitle');
const pdfFrame = document.getElementById('pdfFrame');
const downloadBtn = document.getElementById('downloadBtn');

books.forEach((b,i)=>{
  const div=document.createElement('div');
  div.className='card';
  div.innerHTML=`<h3>${b.title}</h3>`;
  div.onclick=()=>openPopup(i);
  grid.appendChild(div);
});

function openPopup(i){
  bookTitle.textContent=books[i].title;
  pdfFrame.src=books[i].pdf;
  downloadBtn.href=books[i].pdf;
  popup.style.display='flex';
}

function closePopup(){
  popup.style.display='none';
  pdfFrame.src='';
}
</script>

</body>
</html>
