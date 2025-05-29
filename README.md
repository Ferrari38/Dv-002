<html lang="th">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>สรุปรายได้ประจำวัน</title>
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

    <label>รายได้จาก GRAB (บาท):</label>
    <input type="number" id="grab" />

    <label>รายได้จาก BOLT (บาท):</label>
    <input type="number" id="bolt" />

    <label>ทิป (บาท):</label>
    <input type="number" id="tip" />
    
    <label>ค่าน้ำมัน (บาท):</label>
    <input type="number" id="electricity" />

    <label>รายจ่ายอื่นๆ (บาท):</label>
    <input type="number" id="otherExpense" />

    <label>ระยะทางที่ใช้ (กม.):</label>
    <input type="number" id="distance" />

    <button onclick="calculate()">คำนวณ</button>

    <div class="result" id="result"></div>
  </div>

  <script>
    function calculate() {
      const date = document.getElementById('date').value;
      const grab = parseFloat(document.getElementById('grab').value) || 0;
      const boltOriginal = parseFloat(document.getElementById('bolt').value) || 0;
      const electricity = parseFloat(document.getElementById('electricity').value) || 0;
      const other = parseFloat(document.getElementById('otherExpense').value) || 0;
      const distance = parseFloat(document.getElementById('distance').value) || 0;
      const tip = parseFloat(document.getElementById('tip').value) || 0;

      const boltAfterCommission = boltOriginal * 0.82; // หัก 18%
      const totalIncome = grab + boltAfterCommission;
      const maintenance = totalIncome * 0.10;
      const totalExpense = maintenance + electricity + other;
      const netIncome = totalIncome - totalExpense + tip;
      const costPerKm = distance > 0 ? (netIncome / distance).toFixed(2) : 0;

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
        ระยะทางที่ใช้: ${distance} กม.<br>
        บาทต่อกิโลเมตร: ${costPerKm} บาท/กม.
      `;

      document.getElementById('result').innerHTML = resultHTML;
    }
  </script>
</body>
</html>
