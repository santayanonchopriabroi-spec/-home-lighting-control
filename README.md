<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Home Santayanon</title>
    <!-- Font & Icons -->
    <link href="https://fonts.googleapis.com/css2?family=Kanit:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Kanit', sans-serif;
            -webkit-font-smoothing: antialiased;
            -moz-osx-font-smoothing: grayscale;
        }

        body {
            background: radial-gradient(circle at 50% 20%, #151928 0%, #08090d 100%);
            color: #ffffff;
            min-height: 100vh;
            padding: 2rem 1.5rem;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow-x: hidden;
        }

        .dashboard {
            width: 100%;
            max-width: 1100px;
            background: rgba(255, 255, 255, 0.025);
            backdrop-filter: blur(40px);
            -webkit-backdrop-filter: blur(40px);
            border: 1px solid rgba(255, 255, 255, 0.12);
            border-radius: 32px;
            padding: 2.5rem;
            box-shadow: 0 40px 100px rgba(0, 0, 0, 0.8), 0 0 50px rgba(0, 242, 254, 0.05);
        }

        /* 8K Ultra Header */
        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 2.5rem;
            padding-bottom: 1.5rem;
            border-bottom: 1px solid rgba(255, 255, 255, 0.08);
            flex-wrap: wrap;
            gap: 1rem;
        }

        .header h1 {
            font-size: 2.2rem;
            font-weight: 700;
            background: linear-gradient(135deg, #00f2fe 0%, #4facfe 50%, #ffffff 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            display: flex;
            align-items: center;
            gap: 16px;
            letter-spacing: 0.5px;
            filter: drop-shadow(0 0 15px rgba(0, 242, 254, 0.3));
        }

        .status-summary {
            background: rgba(0, 242, 254, 0.08);
            border: 1px solid rgba(0, 242, 254, 0.3);
            color: #00f2fe;
            padding: 0.6rem 1.4rem;
            border-radius: 50px;
            font-size: 0.95rem;
            font-weight: 500;
            display: flex;
            align-items: center;
            gap: 10px;
            box-shadow: 0 0 20px rgba(0, 242, 254, 0.15);
        }

        .section-title {
            font-size: 1.15rem;
            color: #94a3b8;
            margin-bottom: 1.5rem;
            display: flex;
            align-items: center;
            gap: 12px;
            font-weight: 500;
        }

        /* Light Cards Grid */
        .grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(190px, 1fr));
            gap: 1.5rem;
            margin-bottom: 2.5rem;
        }

        .card {
            background: rgba(255, 255, 255, 0.03);
            border: 1px solid rgba(255, 255, 255, 0.08);
            border-radius: 24px;
            padding: 1.5rem;
            transition: all 0.4s cubic-bezier(0.16, 1, 0.3, 1);
            position: relative;
        }

        .card:hover {
            border-color: rgba(0, 242, 254, 0.3);
            transform: translateY(-4px);
        }

        .card.active {
            background: rgba(0, 242, 254, 0.08);
            border-color: rgba(0, 242, 254, 0.5);
            box-shadow: 0 15px 35px rgba(0, 242, 254, 0.2), inset 0 0 15px rgba(0, 242, 254, 0.1);
        }

        .card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1.5rem;
        }

        .icon-box {
            width: 52px;
            height: 52px;
            border-radius: 16px;
            background: rgba(255, 255, 255, 0.05);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.4rem;
            color: #64748b;
            transition: all 0.4s ease;
        }

        .card.active .icon-box {
            background: #00f2fe;
            color: #07090e;
            box-shadow: 0 0 25px #00f2fe;
        }

        /* 8K Toggle Switch */
        .switch {
            position: relative;
            display: inline-block;
            width: 50px;
            height: 28px;
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
            background-color: rgba(255, 255, 255, 0.12);
            transition: .4s;
            border-radius: 34px;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        .slider:before {
            position: absolute;
            content: "";
            height: 20px;
            width: 20px;
            left: 3px;
            bottom: 3px;
            background-color: #ffffff;
            transition: .4s;
            border-radius: 50%;
            box-shadow: 0 2px 8px rgba(0,0,0,0.5);
        }

        input:checked + .slider {
            background-color: #00f2fe;
            border-color: #00f2fe;
        }

        input:checked + .slider:before {
            transform: translateX(22px);
            background-color: #07090e;
        }

        .card-title {
            font-size: 1.05rem;
            font-weight: 500;
            margin-bottom: 0.3rem;
        }

        .card-status {
            font-size: 0.85rem;
            color: #64748b;
        }

        .card.active .card-status {
            color: #00f2fe;
            font-weight: 500;
        }

        /* 8K Air Conditioner Card */
        .ac-card {
            background: rgba(255, 255, 255, 0.03);
            border: 1px solid rgba(255, 255, 255, 0.08);
            border-radius: 28px;
            padding: 2rem 2.5rem;
            display: flex;
            flex-wrap: wrap;
            gap: 2rem;
            align-items: center;
            justify-content: space-between;
            transition: all 0.4s ease;
        }

        .ac-card.active {
            background: rgba(0, 230, 118, 0.06);
            border-color: rgba(0, 230, 118, 0.4);
            box-shadow: 0 15px 40px rgba(0, 230, 118, 0.15), inset 0 0 20px rgba(0, 230, 118, 0.05);
        }

        .ac-info {
            display: flex;
            align-items: center;
            gap: 1.5rem;
        }

        .ac-icon {
            width: 60px;
            height: 60px;
            border-radius: 18px;
            background: rgba(255, 255, 255, 0.05);
            color: #64748b;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.7rem;
            transition: all 0.4s ease;
        }

        .ac-card.active .ac-icon {
            background: #00e676;
            color: #07090e;
            box-shadow: 0 0 30px #00e676;
        }

        .ac-temp-control {
            display: flex;
            align-items: center;
            gap: 1.2rem;
        }

        .temp-btn {
            width: 44px;
            height: 44px;
            border-radius: 50%;
            border: 1px solid rgba(255, 255, 255, 0.15);
            background: rgba(255, 255, 255, 0.05);
            color: #ffffff;
            font-size: 1.1rem;
            cursor: pointer;
            transition: all 0.2s ease;
        }

        .temp-btn:hover {
            background: rgba(255, 255, 255, 0.2);
            border-color: rgba(255, 255, 255, 0.3);
            transform: scale(1.05);
        }

        .temp-display {
            font-size: 2.5rem;
            font-weight: 600;
            min-width: 90px;
            text-align: center;
            letter-spacing: -1px;
        }
    </style>
</head>
<body>

    <div class="dashboard">
        <!-- Header -->
        <div class="header">
            <h1><i class="fa-solid fa-house-signal"></i> Home Santayanon</h1>
            <div class="status-summary">
                <i class="fa-solid fa-bolt"></i>
                <span id="active-count">เปิดอยู่ 0/5 จุด</span>
            </div>
        </div>

        <!-- 5 Light Switches -->
        <div class="section-title">
            <i class="fa-solid fa-lightbulb" style="color: #00f2fe;"></i> ระบบไฟส่องสว่าง (5 จุด)
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
            <i class="fa-solid fa-snowflake" style="color: #00e676;"></i> ระบบปรับอากาศ
        </div>
        <div class="ac-card" id="ac-card">
            <div class="ac-info">
                <div class="ac-icon"><i class="fa-solid fa-wind"></i></div>
                <div>
                    <div class="card-title" style="font-size: 1.25rem;">เครื่องปรับอากาศ (Inverter)</div>
                    <div class="card-status" id="ac-status">สถานะ: ปิดใช้งาน</div>
                </div>
            </div>

            <div style="display: flex; align-items: center; gap: 1.8rem;">
                <div class="ac-temp-control">
                    <button class="temp-btn" onclick="changeTemp(-1)"><i class="fa-solid fa-minus"></i></button>
                    <div class="temp-display"><span id="ac-temp">25</span>°C</div>
                    <button class="temp-btn" onclick="changeTemp(1)"><i class="fa-solid fa-plus"></i></button>
                </div>

                <label class="switch">
                    <input type="checkbox" onchange="toggleAC(this.checked)">
                    <span class="slider"></span>
                </label>
            </div>
        </div>
    </div>

    <!-- JavaScript Control Logic -->
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
