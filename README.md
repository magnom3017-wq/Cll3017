<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>حساباتي - بطاقات متحركة</title>
<style>
  body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background: #121212;
    margin: 0;
    padding: 20px;
    color: #ececec;
  }
  h1 {
    text-align: center;
    margin-bottom: 30px;
    color: #00bcd4;
  }
  .container {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 20px;
  }
  .card {
    width: 160px;
    height: 200px;
    perspective: 1000px;
    cursor: pointer;
  }
  .inner-card {
    position: relative;
    width: 100%;
    height: 100%;
    border-radius: 15px;
    box-shadow: 0 6px 18px rgba(0,0,0,0.5);
    background: linear-gradient(135deg, #1a1a1a, #2c2c2c);
    transform-style: preserve-3d;
    transition: transform 0.8s cubic-bezier(0.4, 0, 0.2, 1);
  }
  .card:hover .inner-card {
    transform: rotateY(180deg);
  }
  .front, .back {
    position: absolute;
    width: 100%;
    height: 100%;
    border-radius: 15px;
    backface-visibility: hidden;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 15px;
  }
  .front {
    background: linear-gradient(135deg, #00bcd4, #0097a7);
    color: #fff;
  }
  .back {
    background: #262626;
    color: #00bcd4;
    transform: rotateY(180deg);
    text-align: center;
    font-size: 14px;
  }
  .front img {
    width: 70px;
    margin-bottom: 15px;
  }
  .app-name {
    font-weight: bold;
    font-size: 18px;
  }
  .url {
    word-break: break-word;
    margin-top: 10px;
  }
  a {
    text-decoration: none;
    color: inherit;
  }
  @media(max-width:600px){
    .container {
      flex-direction: column;
      align-items: center;
    }
  }
</style>
</head>
<body>

<h1>حساباتي الإجتماعية</h1>
<div class="container">

  <a href="https://www.youtube.com/@kamola3017" target="_blank" class="card" title="يوتيوب">
    <div class="inner-card">
      <div class="front">
        <img src="https://upload.wikimedia.org/wikipedia/commons/4/42/YouTube_icon_%282013-2017%29.png" alt="YouTube Logo"/>
        <div class="app-name">يوتيوب</div>
      </div>
      <div class="back">
        https://www.youtube.com/@kamola3017
      </div>
    </div>
  </a>

  <a href="https://www.tiktok.com/@kamola.3017?_t=ZS-90xX5Zlt75T&_r=1" target="_blank" class="card" title="تيك توك">
    <div class="inner-card">
      <div class="front">
        <img src="https://upload.wikimedia.org/wikipedia/commons/a/a9/TikTok_logo.svg" alt="TikTok Logo" style="width: 60px;"/>
        <div class="app-name">تيك توك</div>
      </div>
      <div class="back">
        https://www.tiktok.com/@kamola.3017
      </div>
    </div>
  </a>

  <a href="https://www.snapchat.com/add/kamola252903?share_id=ToNKEy4L3oA&locale=ar" target="_blank" class="card" title="سناب شات">
    <div class="inner-card">
      <div class="front">
        <img src="https://upload.wikimedia.org/wikipedia/en/thumb/c/c4/Snapchat_logo.svg/1024px-Snapchat_logo.svg.png" alt="Snapchat Logo" style="width: 70px;"/>
        <div class="app-name">سناب شات</div>
      </div>
      <div class="back">
        kamola252903
      </div>
    </div>
  </a>

  <a href="https://facebook.com/share/1DtUpF5Pwy/" target="_blank" class="card" title="فيسبوك">
    <div class="inner-card">
      <div class="front">
        <img src="https://upload.wikimedia.org/wikipedia/commons/0/05/Facebook_Logo_(2019).png" alt="Facebook Logo" style="width: 60px;"/>
        <div class="app-name">فيسبوك</div>
      </div>
      <div class="back">
        https://facebook.com/share/1DtUpF5Pwy/
      </div>
    </div>
  </a>

  <a href="https://www.instagram.com/kamola_463?igsh=ZWVybThwa2ZhZzB0" target="_blank" class="card" title="إنستغرام">
    <div class="inner-card">
      <div class="front">
        <img src="https://upload.wikimedia.org/wikipedia/commons/e/e7/Instagram_logo_2016.svg" alt="Instagram Logo" style="width: 60px;"/>
        <div class="app-name">إنستغرام</div>
      </div>
      <div class="back">
        kamola_463
      </div>
    </div>
  </a>

  <a href="https://t.me/ou_kamel" target="_blank" class="card" title="تليجرام">
    <div class="inner-card">
      <div class="front">
        <img src="https://upload.wikimedia.org/wikipedia/commons/8/82/Telegram_logo.svg" alt="Telegram Logo" style="width: 60px;"/>
        <div class="app-name">تليجرام</div>
      </div>
      <div class="back">
        https://t.me/ou_kamel
      </div>
    </div>
  </a>

</div>

</body>
</html>
