<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>4K Smart Home Control Dashboard</title>
    <!-- Font & Icons -->
    <link href="https://fonts.googleapis.com/css2?family=Kanit:wght@300;400;500;600&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Kanit', sans-serif;
        }

        body {
            background: radial-gradient(circle at 10% 20%, #1a1c2e 0%, #0d0e15 90%);
            color: #ffffff;
            min-height: 100vh;
            padding: 2rem;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .dashboard {
            width: 100%;
            max-width: 1100px;
            background: rgba(255, 255, 255, 0.03);
            backdrop-filter: blur(20px);
            -webkit-backdrop-filter: blur(20px);
            border: 1px solid rgba(255, 255, 255, 0.08);
            border-radius: 28px;
            padding: 2.5rem;
            box-shadow: 0 30px 60px rgba(0, 0, 0, 0.6);
        }

        /* Header */
        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 2rem;
            padding-bottom: 1rem;
            border-bottom: 1px solid rgba(255, 255, 255, 0.08);
        }

        .header h1 {
            font-size: 1.8rem;
            font-weight: 600;
            background: linear-gradient(90deg, #00f2fe, #4facfe);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .status-summary {
            background: rgba(0, 242, 254, 0.1);
            border: 1px solid rgba(0, 242, 254, 0.3);
            color: #00f2fe;
            padding: 0.5rem 1.2rem;
            border-radius: 50px;
            font-size: 0.9rem;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .section-title {
            font-size: 1.1rem;
            color: #a0aec0;
            margin-bottom: 1.2rem;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        /* Light Cards Grid */
        .grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(190px, 1fr));
            gap: 1.2rem;
            margin-bottom: 2.5rem;
        }

        .card {
            background: rgba(255, 255, 255, 0.04);
            border: 1px solid rgba(255, 255, 255, 0.08);
            border-radius: 20px;
            padding: 1.4rem;
            transition: all 0.3s ease;
            position: relative;
        }

        .card.active {
            background: rgba(0, 242, 254, 0.08);
            border-color: rgba(0, 242, 254, 0.4);
            box-shadow: 0 10px 25px rgba(0, 242, 254, 0.15);
        }

        .card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1.2rem;
        }

        .icon-box {
            width: 48px;
            height: 48px;
            border-radius: 14px;
            background: rgba(255, 255, 255, 0.06);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.3rem;
            color: #718096;
            transition: 0.3s;
        }

        .card.active .icon-box {
            background: #00f2fe;
            color: #0f111a;
            box-shadow: 0 0 18px #00f2fe;
        }

        /* Toggle Switch */
        .switch {
            position: relative;
            display: inline-block;
            width: 48px;
            height: 26px;
        }

        .switch input {
            opacity: 0;
            width: 0;
            height: 0;
        }

        .slider {
            position: absolute;
            cursor: pointer;
            top: 0; left: 0; right: 0; bottom: 0;
            background-color: rgba(255, 255, 255, 0.15);
            transition: .4s;
            border-radius: 34px;
        }

        .slider:before {
            position: absolute;
            content: "";
            height: 18px;
            width: 18px;
            left: 4px;
            bottom: 4px;
            background-color: white;
            transition: .4s;
            border-radius: 50%;
        }

        input:checked + .slider {
            background-color: #00f2fe;
        }

        input:checked + .slider:before {
            transform: translateX(22px);
        }

        .card-title {
            font-size: 1rem;
            font-weight: 500;
            margin-bottom: 0.2rem;
        }

        .card-status {
            font-size: 0.8rem;
            color: #718096;
        }

        .card.active .card-status {
            color: #00f2fe;
        }

        /* Air Conditioner Section */
        .ac-card {
            background: rgba(255, 255, 255, 0.04);
            border: 1px solid rgba(255, 255, 255, 0.08);
            border-radius: 24px;
            padding: 1.8rem 2.2rem;
            display: flex;
            flex-wrap: wrap;
            gap: 2rem;
            align-items: center;
            justify-content: space-between;
            transition: 0.3s;
        }

        .ac-card.active {
            border-color: rgba(0, 230, 118, 0.4);
            box-shadow: 0 10px 30px rgba(0, 230, 118, 0.12);
        }

        .ac-info {
            display: flex;
            align-items: center;
            gap: 1.2rem;
        }

        .ac-icon {
            width: 56px;
            height: 56px;
            border-radius: 16px;
            background: rgba(255, 255, 255, 0.06);
            color: #718096;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.6rem;
            transition: 0.3s;
        }

        .ac-card.active .ac-icon {
            background: #00e676;
            color: #0d0e15;
            box-shadow: 0 0 20px #00e676;
        }

        .ac-temp-control {
            display: flex;
            align-items: center;
            gap: 1.2rem;
        }

        .temp-btn {
            width: 42px;
            height: 42px;
            border-radius: 50%;
            border: 1px solid rgba(255, 255, 255, 0.15);
            background: rgba(255, 255, 255, 0.05);
            color: white;
            font-size: 1.1rem;
            cursor: pointer;
            transition: 0.2s;
        }

        .temp-btn:hover {
            background: rgba(255, 255, 255, 0.2);
        }

        .temp-display {
            font-size: 2.2rem;
            font-weight: 600;
            min-width: 80px;
            text-align: center;
        }
    </style>
</head>
<body>

    <div class="dashboard">
        <!-- Header -->
        <div class="header">
            <h1><i class="fa-solid fa-house-signal"></i> Smart Lighting & Climate</h1>
            <div class="status-summary">
                <i class="fa-solid fa-bolt"></i>
                <span id="active-count">เปิดอยู่ 0/5 จุด</span>
            </div>
        </div>

        <!-- 5 Light Switches -->
        <div class="section-title">
            <i class="fa-solid fa-lightbulb"></i> ระบบไฟส่องสว่าง (5 จุด)
        </div>
        <div class="grid">
            <!-- Light 1 -->
            <div class="card" id="card-light1">
                <div class="card-header">
                    <div class="icon-box"><i class="fa-solid fa-lightbulb"></i></div>
                    <label class="switch">
                        <input type="checkbox" onchange="toggleLight('light1', this.checked)">
                        <span class="slider"></span>
                    </label>
                </div>
                <div class="card-title">ห้องนั่งเล่น</div>
                <div class="card-status" id="status-light1">ปิดใช้งาน</div>
            </div>

            <!-- Light 2 -->
            <div class="card" id="card-light2">
                <div class="card-header">
                    <div class="icon-box"><i class="fa-solid fa-bed"></i></div>
                    <label class="switch">
                        <input type="checkbox" onchange="toggleLight('light2', this.checked)">
                        <span class="slider"></span>
                    </label>
                </div>
                <div class="card-title">ห้องนอนใหญ่</div>
                <div class="card-status" id="status-light2">ปิดใช้งาน</div>
            </div>

            <!-- Light 3 -->
            <div class="card" id="card-light3">
                <div class="card-header">
                    <div class="icon-box"><i class="fa-solid fa-utensils"></i></div>
                    <label class="switch">
                        <input type="checkbox" onchange="toggleLight('light3', this.checked)">
                        <span class="slider"></span>
                    </label>
                </div>
                <div class="card-title">ห้องครัว</div>
                <div class="card-status" id="status-light3">ปิดใช้งาน</div>
            </div>

            <!-- Light 4 -->
            <div class="card" id="card-light4">
                <div class="card-header">
                    <div class="icon-box"><i class="fa-solid fa-bath"></i></div>
                    <label class="switch">
                        <input type="checkbox" onchange="toggleLight('light4', this.checked)">
                        <span class="slider"></span>
                    </label>
                </div>
                <div class="card-title">ห้องน้ำ</div>
                <div class="card-status" id="status-light4">ปิดใช้งาน</div>
            </div>

            <!-- Light 5 -->
            <div class="card" id="card-light5">
                <div class="card-header">
                    <div class="icon-box"><i class="fa-solid fa-tree"></i></div>
                    <label class="switch">
                        <input type="checkbox" onchange="toggleLight('light5', this.checked)">
                        <span class="slider"></span>
                    </label>
                </div>
                <div class="card-title">ระเบียงหน้าบ้าน</div>
                <div class="card-status" id="status-light5">ปิดใช้งาน</div>
            </div>
        </div>

        <!-- Air Conditioner -->
        <div class="section-title">
            <i class="fa-solid fa-snowflake"></i> ระบบปรับอากาศ
        </div>
        <div class="ac-card" id="ac-card">
            <div class="ac-info">
                <div class="ac-icon"><i class="fa-solid fa-wind"></i></div>
                <div>
                    <div class="card-title" style="font-size: 1.2rem;">เครื่องปรับอากาศ (Inverter)</div>
                    <div class="card-status" id="ac-status">สถานะ: ปิดใช้งาน</div>
                </div>
            </div>

            <div style="display: flex; align-items: center; gap: 1.5rem;">
                <div class="ac-temp-control">
                    <button class="temp-btn" onclick="changeTemp(-1)"><i class="fa-solid fa-minus"></i></button>
                    <div class="temp-display"><span id="ac-temp">25</span>°C</div>
                    <button class="temp-btn" onclick="changeTemp(1)"><i class="fa-solid fa-plus"></i></button>
                </div>

                <label class="switch" style="margin-left: 1rem;">
                    <input type="checkbox" onchange="toggleAC(this.checked)">
                    <span class="slider"></span>
                </label>
            </div>
        </div>
    </div>

    <!-- JavaScript Control logic -->
    <script>
        const lightStates = {
            light1: false,
            light2: false,
            light3: false,
            light4: false,
            light5: false
        };

        let acState = false;
        let acTemp = 25;

        function toggleLight(id, isOn) {
            lightStates[id] = isOn;
            const card = document.getElementById(`card-${id}`);
            const status = document.getElementById(`status-${id}`);
            
            if (isOn) {
                card.classList.add('active');
                status.innerText = 'เปิดใช้งาน';
            } else {
                card.classList.remove('active');
                status.innerText = 'ปิดใช้งาน';
            }
            updateSummary();
        }

        function updateSummary() {
            const activeCount = Object.values(lightStates).filter(v => v).length;
            document.getElementById('active-count').innerText = `เปิดอยู่ ${activeCount}/5 จุด`;
        }

        function toggleAC(isOn) {
            acState = isOn;
            const card = document.getElementById('ac-card');
            const status = document.getElementById('ac-status');

            if (isOn) {
                card.classList.add('active');
                status.innerText = 'สถานะ: กำลังทำงาน (Cool Mode)';
            } else {
                card.classList.remove('active');
                status.innerText = 'สถานะ: ปิดใช้งาน';
            }
        }

        function changeTemp(delta) {
            if (!acState) return;
            acTemp = Math.min(Math.max(18, acTemp + delta), 30);
            document.getElementById('ac-temp').innerText = acTemp;
        }
    </script>
</body>
</html>
