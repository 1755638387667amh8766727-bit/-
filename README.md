# -<!DOCTYPE html>
<html lang="ar" dir="rtl" id="htmlTag">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>ahmed عمك</title>
  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }
    body {
      background: #f5f7fa;
      padding: 20px;
      direction: rtl;
    }
    .container {
      max-width: 600px;
      margin: 40px auto;
      background: white;
      padding: 30px;
      border-radius: 12px;
      box-shadow: 0 4px 20px rgba(0,0,0,0.1);
    }
    h1, h2 {
      text-align: center;
      margin-bottom: 20px;
      color: #2c3e50;
    }
    input, select, button {
      width: 100%;
      padding: 12px;
      margin: 10px 0;
      border: 1px solid #ccc;
      border-radius: 8px;
      font-size: 16px;
    }
    button {
      background: #4285f4;
      color: white;
      border: none;
      cursor: pointer;
      font-weight: bold;
      transition: background 0.3s;
    }
    button:hover {
      background: #3367d6;
    }
    .hidden {
      display: none;
    }
    .app-header {
      background: #3498db;
      color: white;
      padding: 15px;
      text-align: center;
      border-radius: 8px;
      margin-bottom: 20px;
      font-size: 20px;
      font-weight: bold;
    }
    .options {
      display: flex;
      gap: 15px;
      margin: 20px 0;
    }
    .option-btn {
      flex: 1;
      background: #2ecc71;
    }
    .option-btn.sell {
      background: #e74c3c;
    }
    .item-form {
      margin-top: 20px;
    }
    .item-list {
      margin-top: 20px;
    }
    .item {
      background: #ecf0f1;
      padding: 10px;
      margin: 8px 0;
      border-radius: 6px;
      display: flex;
      justify-content: space-between;
    }
    .lang-switcher {
      text-align: center;
      margin: 15px 0;
    }
    .lang-btn {
      background: #95a5a6;
      margin: 0 5px;
      padding: 8px 12px;
      display: inline-block;
      border-radius: 6px;
      cursor: pointer;
    }
    .lang-btn.active {
      background: #34495e;
      color: white;
    }
  </style>
</head>
<body>

  <!-- صفحة تسجيل الدخول -->
  <div id="loginPage" class="container">
    <h1>تسجيل الدخول</h1>
    <p style="text-align:center; margin-bottom:20px;">(محاكاة تسجيل الدخول بـ Google)</p>
    <input type="text" id="nameInput" placeholder="أدخل اسمك" />
    <input type="email" id="emailInput" placeholder="أدخل بريدك الإلكتروني" />
    <input type="password" id="passInput" placeholder="كلمة المرور" />
    <button onclick="login()">تسجيل الدخول</button>
  </div>

  <!-- صفحة الترحيب -->
  <div id="welcomePage" class="container hidden">
    <h1>مرحبًا بك، <span id="displayName"></span>!</h1>
    <button onclick="goToLangPage()">الانتقال إلى التطبيق</button>
  </div>

  <!-- صفحة اختيار اللغة والدولة -->
  <div id="langPage" class="container hidden">
    <h1>اختر إعداداتك</h1>
    
    <label>الدولة:</label>
    <input type="text" id="countryInput" placeholder="ما هي دولتك؟" />

    <label>اللغة:</label>
    <div class="lang-switcher">
      <div class="lang-btn active" data-lang="ar">العربية</div>
      <div class="lang-btn" data-lang="en">English</div>
      <div class="lang-btn" data-lang="it">Italiano</div>
    </div>

    <button onclick="saveLangAndGoToApp()">تأكيد والانتقال</button>
  </div>

  <!-- صفحة التطبيق الرئيسية -->
  <div id="appPage" class="container hidden">
    <div class="app-header">ahmed عمك</div>

    <div class="options">
      <button class="option-btn" onclick="setMode('buy')">شراء</button>
      <button class="option-btn sell" onclick="setMode('sell')">بيع</button>
    </div>

    <div class="item-form">
      <input type="text" id="itemName" placeholder="اسم العنصر (أكل أو جهاز)" />
      <select id="itemType">
        <option value="food">أكل</option>
        <option value="device">جهاز</option>
      </select>
      <input type="number" id="itemPrice" placeholder="السعر" min="0" step="0.1" />
      <button onclick="addItem()">إضافة</button>
    </div>

    <div class="item-list" id="itemList">
      <!-- سيتم عرض العناصر هنا -->
    </div>
  </div>

  <script>
    // الترجمات
    const translations = {
      ar: {
        loginTitle: "تسجيل الدخول",
        namePlaceholder: "أدخل اسمك",
        emailPlaceholder: "أدخل بريدك الإلكتروني",
        passPlaceholder: "كلمة المرور",
        loginBtn: "تسجيل الدخول",
        welcome: "مرحبًا بك،",
        nextBtn: "الانتقال إلى التطبيق",
        settingsTitle: "اختر إعداداتك",
        countryPlaceholder: "ما هي دولتك؟",
        confirmBtn: "تأكيد والانتقال",
        appTitle: "ahmed عمك",
        buy: "شراء",
        sell: "بيع",
        itemName: "اسم العنصر (أكل أو جهاز)",
        food: "أكل",
        device: "جهاز",
        price: "السعر",
        addBtn: "إضافة"
      },
      en: {
        loginTitle: "Login",
        namePlaceholder: "Enter your name",
        emailPlaceholder: "Enter your email",
        passPlaceholder: "Password",
        loginBtn: "Login",
        welcome: "Welcome,",
        nextBtn: "Go to App",
        settingsTitle: "Choose your settings",
        countryPlaceholder: "What is your country?",
        confirmBtn: "Confirm & Go",
        appTitle: "ahmed 3amk",
        buy: "Buy",
        sell: "Sell",
        itemName: "Item name (Food or Device)",
        food: "Food",
        device: "Device",
        price: "Price",
        addBtn: "Add"
      },
      it: {
        loginTitle: "Accedi",
        namePlaceholder: "Inserisci il tuo nome",
        emailPlaceholder: "Inserisci la tua email",
        passPlaceholder: "Password",
        loginBtn: "Accedi",
        welcome: "Benvenuto,",
        nextBtn: "Vai all'app",
        settingsTitle: "Scegli le tue impostazioni",
        countryPlaceholder: "Qual è il tuo paese?",
        confirmBtn: "Conferma e vai",
        appTitle: "ahmed amk",
        buy: "Compra",
        sell: "Vendi",
        itemName: "Nome articolo (Cibo o Dispositivo)",
        food: "Cibo",
        device: "Dispositivo",
        price: "Prezzo",
        addBtn: "Aggiungi"
      }
    };

    let currentUser = null;
    let currentLang = 'ar';
    let currentMode = 'buy'; // 'buy' or 'sell'

    // تبديل اللغة
    document.querySelectorAll('.lang-btn').forEach(btn => {
      btn.addEventListener('click', () => {
        document.querySelectorAll('.lang-btn').forEach(b => b.classList.remove('active'));
        btn.classList.add('active');
        currentLang = btn.dataset.lang;
        updateLanguage();
      });
    });

    function updateLanguage() {
      const t = translations[currentLang];
      document.getElementById('htmlTag').setAttribute('lang', currentLang);
      document.dir = (currentLang === 'ar') ? 'rtl' : 'ltr';
      
      // تحديث النصوص (يمكنك توسيع هذا حسب الحاجة)
      if (document.getElementById('loginPage').classList.contains('hidden') === false) {
        document.querySelector('#loginPage h1').innerText = t.loginTitle;
        document.getElementById('nameInput').placeholder = t.namePlaceholder;
        document.getElementById('emailInput').placeholder = t.emailPlaceholder;
        document.getElementById('passInput').placeholder = t.passPlaceholder;
        document.querySelector('#loginPage button').innerText = t.loginBtn;
      }
    }

    function login() {
      const name = document.getElementById('nameInput').value.trim();
      const email = document.getElementById('emailInput').value.trim();
      if (!name || !email) {
        alert('الرجاء إدخال الاسم والبريد الإلكتروني');
        return;
      }
      currentUser = { name, email };
      localStorage.setItem('user', JSON.stringify(currentUser));
      document.getElementById('displayName').innerText = name;
      showPage('welcomePage');
    }

    function goToLangPage() {
      showPage('langPage');
    }

    function saveLangAndGoToApp() {
      const country = document.getElementById('countryInput').value.trim();
      if (!country) {
        alert('الرجاء إدخال دولتك');
        return;
      }
      localStorage.setItem('userSettings', JSON.stringify({ country, lang: currentLang }));
      showPage('appPage');
      loadItems();
    }

    function setMode(mode) {
      currentMode = mode;
      loadItems(); // إعادة تحميل العناصر حسب الوضع
    }

    function addItem() {
      const name = document.getElementById('itemName').value.trim();
      const type = document.getElementById('itemType').value;
      const price = parseFloat(document.getElementById('itemPrice').value);
      if (!name || isNaN(price)) {
        alert('الرجاء ملء جميع الحقول بشكل صحيح');
        return;
      }

      const item = { name, type, price, mode: currentMode };
      let items = JSON.parse(localStorage.getItem('items') || '[]');
      items.push(item);
      localStorage.setItem('items', JSON.stringify(items));
      document.getElementById('itemName').value = '';
      document.getElementById('itemPrice').value = '';
      loadItems();
    }

    function loadItems() {
      const items = JSON.parse(localStorage.getItem('items') || '[]');
      const filtered = items.filter(item => item.mode === currentMode);
      const listEl = document.getElementById('itemList');
      listEl.innerHTML = '';
      filtered.forEach(item => {
        const div = document.createElement('div');
        div.className = 'item';
        const typeText = item.type === 'food' ? 
          (currentLang === 'ar' ? 'أكل' : currentLang === 'it' ? 'Cibo' : 'Food') :
          (currentLang === 'ar' ? 'جهاز' : currentLang === 'it' ? 'Dispositivo' : 'Device');
        div.innerHTML = `<strong>${item.name}</strong> - ${typeText} - ${item.price} ${currentLang === 'ar' ? 'ريال' : 'Currency'}`;
        listEl.appendChild(div);
      });
    }

    function showPage(pageId) {
      document.querySelectorAll('.container').forEach(p => p.classList.add('hidden'));
      document.getElementById(pageId).classList.remove('hidden');
    }

    // عند التحميل: تحقق إذا كان المستخدم مسجلاً
    window.onload = () => {
      const savedUser = localStorage.getItem('user');
      const savedSettings = localStorage.getItem('userSettings');
      if (savedUser && savedSettings) {
        currentUser = JSON.parse(savedUser);
        const settings = JSON.parse(savedSettings);
        currentLang = settings.lang;
        document.querySelectorAll('.lang-btn').forEach(btn => {
          if (btn.dataset.lang === currentLang) btn.classList.add('active');
          else btn.classList.remove('active');
        });
        updateLanguage();
        showPage('appPage');
        loadItems();
      } else {
        showPage('loginPage');
      }
    };
  </script>
</body>
</html>
