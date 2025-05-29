<html lang="th">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>สรุปรายได้ประจำวัน💰</title>
  <style>
    body {
      font-family: sans-serif;
      padding: 20px;
      background: #f2f2f2;
    }
    .container {
      background: white;
      padding: 20px;
      border-radius: 10px;
      max-width: 500px;
      margin: auto;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }
    input, button, select {
      width: 100%;
      padding: 10px;
      margin: 10px 0;
      font-size: 16px;
    }
    .result {
      margin-top: 20px;
      background: #e6ffe6;
      padding: 15px;
      border-radius: 5px;
      color: #006600;
    }
  </style>
</head>
<body>
  <div class="container">
    <h2>คำนวณรายได้ประจำวัน</h2>
    <label>วันที่:</label>
    <input type="date" id="date" />

    <h2>📥 รายรับ</h2>
    <label>รายได้จาก GRAB (บาท):</label>
    <input type="number" id="grab" />

    <label>รายได้จาก BOLT (บาท):</label>
    <input type="number" id="bolt" />

    <label>ทิป (บาท):</label>
    <input type="number" id="tip" />

    <h2>📤 รายจ่าย</h2>
    <label>ค่าน้ำมัน (บาท):</label>
    <input type="number" id="electricity" />

    <label>รายจ่ายอื่นๆ (บาท):</label>
    <input type="number" id="otherExpense" />

    <h2>🛻 เลขไมล์รถ</h2>
    <label>เริ่มงาน (กม.):</label>
    <input type="number" id="distanceStart" />

    <label>เลิกงาน (กม.):</label>
    <input type="number" id="distanceEnd" />
    
    <button onclick="calculate()">คำนวณ</button>

    <div class="result" id="result"></div>
  </div>

  <script>n
    function calculate() {
      const date = document.getElementById('date').value;
      const grab = parseFloat(document.getElementById('grab').value) || 0;
      const boltOriginal = parseFloat(document.getElementById('bolt').value) || 0;
      const electricity = parseFloat(document.getElementById('electricity').value) || 0;
      const other = parseFloat(document.getElementById('otherExpense').value) || 0;
      const distanceStart = parseFloat(document.getElementById('distanceStart').value) || 0;
      const distanceEnd = parseFloat(document.getElementById('distanceEnd').value) || 0;
      const tip = parseFloat(document.getElementById('tip').value) || 0;

      const boltAfterCommission = boltOriginal * 0.82; // หัก 18%
      const totalIncome = grab + boltAfterCommission;
      const maintenance = totalIncome * 0.10;
      const totalExpense = maintenance + electricity + other;
      const netIncome = totalIncome - totalExpense + tip;
      const costPerKm = distance > 0 ? (netIncome / distance).toFixed(2) : 0;
      const netIncomekeep netIncome + maintenance;
    
      const resultHTML = `
        <strong>สรุปผลวันที่: ${date}</strong><br><br>
        รายได้ GRAB: ${grab.toFixed(2)} บาท<br>
        รายได้ BOLT (หลังหัก 18%): ${boltAfterCommission.toFixed(2)} บาท<br>
        รวมรายได้: ${totalIncome.toFixed(2)} บาท<br>
        ค่าซ่อม 10%: ${maintenance.toFixed(2)} บาท<br>
        ค่าน้ำมัน: ${electricity.toFixed(2)} บาท<br>
        รายจ่ายอื่น ๆ: ${other.toFixed(2)} บาท<br>
        ทิป: ${tip.toFixed(2)} บาท<br>
        รายได้สุทธิ (หลังหักค่าใช้จ่าย + บวกทิป): ${netIncome.toFixed(2)} บาท<br><br>
        รวมค่าซ่อม (รายได้สุทธิ + ค่าซ่อม):${netIncomekeep.toFixed(2)} บาท<br>
        ระยะทางที่ใช้: ${distance} กม.<br>
        บาทต่อกิโลเมตร: ${costPerKm} บาท/กม.
      `;

      document.getElementById('result').innerHTML = resultHTML;
    }
  </script>
</body>
</html>


<!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>คำนวณรายรับ-รายจ่าย (เวอร์ชันเต็ม)</title>
  <style>
    body {
      font-family: sans-serif;
      padding: 20px;
      max-width: 800px;
      margin: auto;
    }
    input {
      width: 100%;
      margin-bottom: 10px;
      padding: 8px;
    }
    button {
      padding: 10px 15px;
      margin: 5px 5px 5px 0;
    }
    .result {
      margin-top: 20px;
      background-color: #f9f9f9;
      padding: 15px;
      border: 1px solid #ccc;
    }
  </style>
</head>
<body>
  <h1>เครื่องคำนวณรายรับ-รายจ่าย</h1>
  <h2>📥 รายรับ</h2>
  <input id="grab" type="number" placeholder="รายรับจาก GRAB">
  <input id="bolt" type="number" placeholder="รายรับจาก BOLT">
  <input id="indriver" type="number" placeholder="รายรับจาก INDRIVER">
  <input id="maxim" type="number" placeholder="รายรับจาก MAXIM">
  <input id="lineman" type="number" placeholder="รายรับจาก LINEMAN">
  <input id="outside" type="number" placeholder="รายรับจากงานนอก">

  <h2>📤 รายจ่าย</h2>
  <input id="electricity" type="number" placeholder="ค่าไฟ">
  <input id="expense" type="number" placeholder="ค่าใช้จ่ายอื่น ๆ">

  <h2>🛻 เลขไมล์รถ</h2>
  <input id="start_day" type="number" placeholder="เริ่มงานกะเช้า">
  <input id="end_day" type="number" placeholder="จบงานกะเช้า">

  <h3>หรือ ขับกะกลางคืน (ข้ามวัน)</h3>
  <input id="night_00" type="number" placeholder="เมื่อวาน 0.00น.">
  <input id="night_end" type="number" placeholder="จบงานเมื่อวานตอนเช้า">
  <input id="night_start" type="number" placeholder="เริ่มงานเมื่อวานตอนเย็น">
  <input id="today_00" type="number" placeholder="เมื่อวาน 24.00น./วันนี้ 0.00น.">

  <div style="margin-top:20px;">
    <button onclick="calculate()">คำนวณ</button>
    <button onclick="resetForm()">รีเซ็ต</button>
    <button onclick="saveImage()">บันทึกรูปภาพ</button>
  </div>

  <div class="result" id="result"></div>

  <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
  <script>
    function calculate() {
      const income = ["grab", "bolt", "indriver", "maxim", "lineman", "outside"]
        .map(id => parseFloat(document.getElementById(id).value) || 0)
        .reduce((a, b) => a + b, 0);

      const expenses = ["electricity", "expense"]
        .map(id => parseFloat(document.getElementById(id).value) || 0)
        .reduce((a, b) => a + b, 0);

      let distance = 0;
      const startDay = parseFloat(document.getElementById('start_day').value);
      const endDay = parseFloat(document.getElementById('end_day').value);

      if (!isNaN(startDay) && !isNaN(endDay)) {
        distance = endDay - startDay;
      } else {
        const night00 = parseFloat(document.getElementById('night_00').value) || 0;
        const nightEnd = parseFloat(document.getElementById('night_end').value) || 0;
        const nightStart = parseFloat(document.getElementById('night_start').value) || 0;
        const today00 = parseFloat(document.getElementById('today_00').value) || 0;
        distance = (nightEnd - night00) + (today00 - nightStart);
      }

      const netIncome = income - expenses;
      const costPerKm = distance > 0 ? (expenses / distance).toFixed(2) : '0';

      document.getElementById('result').innerHTML = `
        <strong>รวมยอดที่ต้องโอน:</strong> ${netIncome.toFixed(2)} บาท<br>
        <strong>ระยะทางที่ใช้:</strong> ${distance.toFixed(2)} กม.<br>
        <strong>บาทต่อกิโลเมตร:</strong> ${costPerKm} บาท/km
      `;
    }

    function resetForm() {
      document.querySelectorAll('input').forEach(input => input.value = '');
      document.getElementById('result').innerHTML = '';
    }

    function saveImage() {
      html2canvas(document.body).then(canvas => {
        const link = document.createElement('a');
        link.download = 'result.png';
        link.href = canvas.toDataURL();
        link.click();
      });
    }
  </script>
</body>
</html>
