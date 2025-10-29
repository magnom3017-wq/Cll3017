<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>عرض حساباتي</title>
<style>
  body {
    font-family: Arial, sans-serif;
    background-color: #f2f2f2;
    margin: 20px;
  }
  .container {
    display: flex;
    flex-wrap: wrap;
    gap: 15px;
    justify-content: center;
  }
  .card {
    background-color: #ffffff;
    border-radius: 8px;
    box-shadow: 0 2px 5px rgba(0,0,0,0.2);
    width: 150px;
    text-align: center;
    padding: 15px;
    cursor: pointer;
    transition: transform 0.2s;
  }
  .card:hover {
    transform: scale(1.05);
  }
  .card img {
    width: 100px;
    height: 100px;
    object-fit: contain;
    margin-bottom: 10px;
  }
  .app-name {
    font-size: 16px;
    color: #333;
  }
</style>
</head>
<body>

<h1 style="text-align:center;">حساباتي</h1>
<div class="container">
  <a href="https://www.facebook.com/yourprofile" class="card" target="_blank" title="فيسبوك">
    <img src="https://upload.wikimedia.org/wikipedia/commons/5/51/Facebook_f_logo_%282019%29.svg" alt="Facebook Logo">
    <div class="app-name">فيسبوك</div>
  </a>
  
  <a href="https://www.twitter.com/yourprofile" class="card" target="_blank" title="تويتر">
    <img src="https://upload.wikimedia.org/wikipedia/fr/c/c8/Twitter_Bird.svg" alt="Twitter Logo">
    <div class="app-name">تويتر</div>
  </a>
  
  <a href="https://www.instagram.com/yourprofile" class="card" target="_blank" title="إنستغرام">
    <img src="https://upload.wikimedia.org/wikipedia/commons/e/e7/Instagram_logo_2016.svg" alt="Instagram Logo">
    <div class="app-name">إنستغرام</div>
  </a>
  
  <!-- أضف المزيد من الحسابات بنفس الطريقة -->
  
</div>

</body>
</html>
