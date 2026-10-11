<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>توقيت الدراسة وحاسبة التناوب - مدرسة بنايش بلبشير</title>
    <style>
        :root {
            --primary-color: #1b5e20;
            --secondary-color: #2e7d32;
            --accent-color: #e8f5e9;
            --text-color: #333;
            --bg-color: #f4f6f8;
            --white: #ffffff;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-color);
            padding: 15px;
            line-height: 1.6;
        }

        .container {
            max-width: 900px;
            margin: 0 auto;
            background: var(--white);
            border-radius: 12px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
            overflow: hidden;
            padding: 20px;
        }

        header {
            text-align: center;
            margin-bottom: 20px;
            border-bottom: 2px solid var(--accent-color);
            padding-bottom: 15px;
        }

        header h3 {
            font-size: 1rem;
            color: #555;
            margin-bottom: 5px;
        }

        header h1 {
            font-size: 1.3rem;
            color: var(--primary-color);
            margin-top: 5px;
        }

        .rotation-calculator {
            background-color: #f0f7f4;
            border: 2px solid var(--secondary-color);
            border-radius: 10px;
            padding: 15px;
            margin-bottom: 25px;
            text-align: center;
        }

        .rotation-calculator h3 {
            color: var(--primary-color);
            margin-bottom: 10px;
            font-size: 1.1rem;
        }

        .calculator-controls {
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 10px;
            margin-bottom: 15px;
            flex-wrap: wrap;
        }

        .calculator-controls label {
            font-weight: bold;
        }

        .calculator-controls input[type="date"] {
            padding: 8px 12px;
            border-radius: 6px;
            border: 1px solid #ccc;
            font-size: 1rem;
        }

        .result-box {
            display: flex;
            justify-content: space-around;
            gap: 10px;
            margin-top: 10px;
            flex-wrap: wrap;
        }

        .result-card {
            flex: 1;
            min-width: 220px;
            background: var(--white);
            padding: 12px;
            border-radius: 8px;
            box-shadow: 0 2px 6px rgba(0,0,0,0.08);
            border-top: 4px solid var(--primary-color);
        }

        .result-card.morning {
            border-top-color: #2196F3;
        }

        .result-card.afternoon {
            border-top-color: #FF9800;
        }

        .result-card h4 {
            font-size: 0.95rem;
            color: #666;
            margin-bottom: 5px;
        }

        .result-card .group-name {
            font-size: 1.3rem;
            font-weight: bold;
            color: var(--primary-color);
        }

        .tabs {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin-bottom: 20px;
        }

        .tab-btn {
            background-color: #e0e0e0;
            border: none;
            padding: 10px 25px;
            font-size: 1.05rem;
            font-weight: bold;
            border-radius: 30px;
            cursor: pointer;
            transition: all 0.3s ease;
            color: #555;
        }

        .tab-btn.active {
            background-color: var(--primary-color);
            color: var(--white);
            box-shadow: 0 4px 10px rgba(27, 94, 32, 0.3);
        }

        .schedule-section {
            display: none;
        }

        .schedule-section.active {
            display: block;
        }

        .table-responsive {
            overflow-x: auto;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            margin-bottom: 15px;
            text-align: center;
            background: var(--white);
        }

        th, td {
            border: 1px solid #ddd;
            padding: 10px 6px;
            font-size: 0.9rem;
        }

        th {
            background-color: var(--primary-color);
            color: var(--white);
        }

        tr:nth-child(even) {
            background-color: #fafafa;
        }

        .highlight-tuesday {
            background-color: #e8f5e9;
            font-weight: bold;
        }

        .note-box {
            background-color: var(--accent-color);
            border-right: 5px solid var(--primary-color);
            padding: 10px 12px;
            border-radius: 4px;
            font-size: 0.95rem;
            color: #1b5e20;
            margin-top: 10px;
        }

        footer {
            text-align: center;
            margin-top: 25px;
            font-size: 0.85rem;
            color: #777;
            border-top: 1px solid #eee;
            padding-top: 10px;
        }
    </style>
</head>
<body>

    <div class="container">
        <header>
            <h3>الجمهورية الجزائرية الديمقراطية الشعبية</h3>
            <h3>وزارة التربية الوطنية - مديرية التربية لولاية غليزان</h3>
            <h3>مدرسة الشهيد: بنايش بلبشير غليزان</h3>
            <h1>جدول التوقيت ودليل تناوب يوم الثلاثاء</h1>
        </header>

        <div class="rotation-calculator">
            <h3>🔍 دليلك لمعرفة توقيت يوم الثلاثاء بالضبط</h3>
            <p style="font-size: 0.85rem; color: #555; margin-bottom: 10px;">اختر تاريخ يوم الثلاثاء لمعرفة من يدرس صباحاً ومن يدرس مساءً:</p>
            
            <div class="calculator-controls">
                <label for="tuesdayDate">اختر تاريخ الثلاثاء:</label>
                <input type="date" id="tuesdayDate" onchange="calculateTuesdayRotation()">
            </div>

            <div class="result-box">
                <div class="result-card morning">
                    <h4>الفترة الصباحية (08:00 - 12:30)</h4>
                    <div class="group-name" id="morningGroup">الفوج (ب)</div>
                </div>
                <div class="result-card afternoon">
                    <h4>الفترة المسائية (12:30 - 17:00)</h4>
                    <div class="group-name" id="afternoonGroup">الفوج (أ)</div>
                </div>
            </div>
        </div>

        <div class="tabs">
            <button class="tab-btn active" onclick="switchTab('groupA', event)">الجدول الكامل: الفوج (أ)</button>
            <button class="tab-btn" onclick="switchTab('groupB', event)">الجدول الكامل: الفوج (ب)</button>
        </div>

        <div id="groupA" class="schedule-section active">
            <div class="table-responsive">
                <table>
                    <thead>
                        <tr>
                            <th>الفترة</th>
                            <th>الأحد</th>
                            <th>الإثنين</th>
                            <th>الثلاثاء</th>
                            <th>الأربعاء</th>
                            <th>الخميس</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td><strong>صباحا</strong></td>
                            <td>08:00 إلى 10:30</td>
                            <td>08:00 إلى 10:30</td>
                            <td class="highlight-tuesday">08:00 إلى 12:30<br><small>(بالتناوب)</small></td>
                            <td>08:00 إلى 10:30</td>
                            <td>08:00 إلى 10:30</td>
                        </tr>
                        <tr>
                            <td><strong>مساءا</strong></td>
                            <td>13:00 إلى 15:00</td>
                            <td>13:00 إلى 15:00</td>
                            <td class="highlight-tuesday">12:30 إلى 17:00<br><small>(بالتناوب)</small></td>
                            <td>15:00 إلى 17:00</td>
                            <td>15:00 إلى 17:00</td>
                        </tr>
                    </tbody>
                </table>
            </div>
            <div class="note-box">
                <strong>ملاحظة:</strong> السنة الأولى والثانية والثالثة يوم الخميس من 11:00 إلى 14:00
            </div>
        </div>

        <div id="groupB" class="schedule-section">
            <div class="table-responsive">
                <table>
                    <thead>
                        <tr>
                            <th>الفترة</th>
                            <th>الأحد</th>
                            <th>الإثنين</th>
                            <th>الثلاثاء</th>
                            <th>الأربعاء</th>
                            <th>الخميس</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td><strong>صباحا</strong></td>
                            <td>10:30 إلى 13:00</td>
                            <td>10:30 إلى 13:00</td>
                            <td class="highlight-tuesday">08:00 إلى 12:30<br><small>(بالتناوب)</small></td>
                            <td>10:30 إلى 13:00</td>
                            <td>08:00 إلى 10:30</td>
                        </tr>
                        <tr>
                            <td><strong>مساءا</strong></td>
                            <td>15:00 إلى 17:00</td>
                            <td>15:00 إلى 17:00</td>
                            <td class="highlight-tuesday">12:30 إلى 17:00<br><small>(بالتناوب)</small></td>
                            <td>13:00 إلى 15:00</td>
                            <td>13:00 إلى 15:00</td>
                        </tr>
                    </tbody>
                </table>
            </div>
            <div class="note-box">
                <strong>ملاحظة:</strong> السنة الأولى والثانية والثالثة يوم الخميس من 08:00 إلى 11:00
            </div>
        </div>

        <footer>
            مدرسة الشهيد بنايش بلبشير غليزان &copy; 2026
        </footer>
    </div>

    <script>
        const baseTuesday = new Date(2026, 9, 13);

        function initDate() {
            const dateInput = document.getElementById('tuesdayDate');
            const today = new Date();
            const dayOfWeek = today.getDay();
            let distanceToTuesday = (2 - dayOfWeek + 7) % 7;
            
            const nextTuesday = new Date(today);
            nextTuesday.setDate(today.getDate() + distanceToTuesday);
            
            const yyyy = nextTuesday.getFullYear();
            const mm = String(nextTuesday.getMonth() + 1).padStart(2, '0');
            const dd = String(nextTuesday.getDate()).padStart(2, '0');
            dateInput.value = `${yyyy}-${mm}-${dd}`;
            
            calculateTuesdayRotation();
        }

        function calculateTuesdayRotation() {
            const selectedDateVal = document.getElementById('tuesdayDate').value;
            if (!selectedDateVal) return;

            const selectedDate = new Date(selectedDateVal);
            const diffTime = selectedDate.getTime() - baseTuesday.getTime();
            const diffDays = Math.round(diffTime / (1000 * 3600 * 24));
            const diffWeeks = Math.floor(diffDays / 7);

            if (Math.abs(diffWeeks) % 2 === 0) {
                document.getElementById('morningGroup').innerText = "الفوج (ب)";
                document.getElementById('afternoonGroup').innerText = "الفوج (أ)";
            } else {
                document.getElementById('morningGroup').innerText = "الفوج (أ)";
                document.getElementById('afternoonGroup').innerText = "الفوج (ب)";
            }
        }

        function switchTab(groupName, event) {
            const sections = document.querySelectorAll('.schedule-section');
            sections.forEach(sec => sec.classList.remove('active'));

            const buttons = document.querySelectorAll('.tab-btn');
            buttons.forEach(btn => btn.classList.remove('active'));

            document.getElementById(groupName).classList.add('active');
            event.currentTarget.classList.add('active');
        }

        window.onload = initDate;
    </script>

</body>
</html>
