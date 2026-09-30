
=============================
هذه نسخة PWA أولية تعمل من المتصفح ويمكن تثبيتها كتطبيق على الهاتف عندما تُرفع إلى استضافة HTTPS.

الموجود:
- GPS لتحديد موقع المستخدم.
- تسجيل بيانات السائق ورقم الهاتف.
- زر اتصال بالسائق.
- تحديد وقت الرحلة.
- حفظ طلبات الرحلات على الجهاز.
- فتح إحداثيات GPS في خرائط Google.

ملاحظة:
هذه نسخة محلية أولى؛ بيانات السائقين والطلبات محفوظة على نفس الجهاز فقط.
للنسخة التالية يمكن إضافة قاعدة بيانات، حسابات للسائقين، لوحة إدارة، ومشاركة الطلبات بين هاتف الراكب والسائق.     <!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>تكسي الضلوعية</title>
    <style>
        body { font-family: Tahoma, sans-serif; background-color: #f4f7f6; margin: 0; padding: 20px; color: #333; }
        .container { max-width: 450px; margin: 0 auto; background: #ffffff; padding: 20px; border-radius: 12px; box-shadow: 0 4px 15px rgba(0,0,0,0.1); }
        header { text-align: center; border-bottom: 2px solid #eee; padding-bottom: 15px; margin-bottom: 20px; }
        header h1 { color: #007bff; margin: 0 0 5px 0; }
        .card { background: #f9f9f9; border: 1px solid #e0e0e0; padding: 15px; border-radius: 8px; margin-bottom: 20px; }
        label { display: block; margin-bottom: 5px; font-weight: bold; font-size: 14px; }
        input, select { width: 100%; padding: 10px; margin-bottom: 12px; border: 1px solid #ccc; border-radius: 6px; box-sizing: border-box; }
        button { background: #28a745; color: white; padding: 12px; width: 100%; border: none; border-radius: 6px; font-size: 16px; font-weight: bold; cursor: pointer; }
        ul { padding-right: 20px; margin: 10px 0 0 0; }
        li { margin: 8px 0; background: #fff; padding: 8px 12px; border-radius: 5px; border: 1px solid #ddd; }
    </style>
</head>
<body>
<div class="container">
    <header>
        <h1>🚕 تكسي الضلوعية</h1>
        <p>سجل رقمك وخط سيرك بكل سهولة</p>
    </header>
    <div class="card">
        <h3>🚖 تسجيل السواق</h3>
        <label>رقم الهاتف:</label>
        <input type="tel" id="driverPhone" placeholder="مثال: 07800000000">
        <label>خط السير:</label>
        <select id="driverRoute">
            <option value="بغداد">بغداد</option>
            <option value="تكريت">تكريت</option>
            <option value="سليمانية">سليمانية</option>
            <option value="سامراء">سامراء</option>
        </select>
        <button onclick="saveDriver()">حفظ وتسجيل الرقم</button>
    </div>
    <div class="card">
        <h3>📋 قائمة السواق المتاحين:</h3>
        <ul id="driversList"><li style="color: #777;">جاري التحميل...</li></ul>
    </div>
</div>
<script>
    window.onload = displayDrivers;
    function saveDriver() {
        let phone = document.getElementById('driverPhone').value;
        let route = document.getElementById('driverRoute').value;
        if(!phone) { alert("يرجى إدخال رقم الهاتف!"); return; }
        let drivers = JSON.parse(localStorage.getItem('allDrivers')) || [];
        drivers.push({ phone: phone, route: route });
        localStorage.setItem('allDrivers', JSON.stringify(drivers));
        document.getElementById('driverPhone').value = '';
        displayDrivers();
        alert("تم تسجيل السائق بنجاح ✅");
    }
    function displayDrivers() {
        let list = document.getElementById('driversList');
        list.innerHTML = '';
        let drivers = JSON.parse(localStorage.getItem('allDrivers')) || [];
        if(drivers.length === 0) { list.innerHTML = '<li style="color: #777;">لا يوجد سائقين.</li>'; return; }
        drivers.forEach(d => {
            let li = document.createElement('li');
            li.innerHTML = `📞 <strong>${d.phone}</strong> - خط: <span style="color: #007bff;">${d.route}</span>`;
            list.appendChild(li);
        });
    }
</script>
</body>
</html>
