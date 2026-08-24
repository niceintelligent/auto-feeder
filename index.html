<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Automatic Weighing Controller</title>
    <style>
        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
            background-color: #f4f6f9;
            margin: 0;
            padding: 15px;
            color: #333;
        }
        .container {
            max-width: 500px;
            margin: 0 auto;
            background: #fff;
            padding: 20px;
            border-radius: 12px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.08);
        }
        h2 {
            text-align: center;
            color: #111;
            margin-top: 0;
        }
        .btn {
            display: block;
            width: 100%;
            padding: 12px;
            font-size: 16px;
            font-weight: bold;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            text-align: center;
            box-sizing: border-box;
        }
        .btn-blue {
            background-color: #007bff;
            color: white;
            margin-bottom: 15px;
        }
        .btn-red {
            background-color: #e53e3e;
            color: white;
            margin-bottom: 15px;
        }
        .btn-green {
            background-color: #28a745;
            color: white;
            margin-top: 20px;
        }
        .weight-display {
            background: #fff5f5;
            border: 2px solid #feb2b2;
            border-radius: 8px;
            padding: 15px;
            text-align: center;
            font-size: 22px;
            font-weight: bold;
            color: #e53e3e;
            margin: 15px 0;
        }
        .param-group {
            margin-bottom: 15px;
        }
        .param-group label {
            display: block;
            font-size: 14px;
            font-weight: 600;
            margin-bottom: 5px;
            color: #4a5568;
        }
        .param-group label.warning {
            color: #e53e3e; 
        }
        .param-group label.highlight {
            color: #2b6cb0;
        }
        .param-group input, .param-group select {
            width: 100%;
            padding: 10px;
            font-size: 16px;
            border: 1px solid #cbd5e0;
            border-radius: 6px;
            box-sizing: border-box;
        }
        .status-bar {
            text-align: center;
            font-size: 14px;
            color: #718096;
            margin-bottom: 10px;
        }
        .timer-box {
            background: #ebf8ff;
            border: 1px solid #bee3f8;
            padding: 12px;
            border-radius: 8px;
            margin-bottom: 15px;
        }
    </style>
</head>
<body>

<div class="container">
    <h2> Automatic Weighing Controller </h2>
    <div class="status-bar" id="statusText">Status: Disconnected</div>
    <button class="btn btn-blue" id="connectBtn" onclick="onConnectClick()">Search & Connect Device</button> 
    <div class="weight-display" id="weightVal">Current Real-time Weight: 0.0 g</div>
    <hr style="border:0; height:1px; background:#e2e8f0; margin:20px 0;">

    <!-- 新增：定时器功能区块 -->
    <div class="timer-box">
        <div class="param-group">
            <label class="highlight">11. Timer Mode (定时投喂开关):</label>
            <select id="etTimerEnable" onchange="toggleTimerInput()">
                <option value="0">Disabled (Continuous Mode / 连续循环供料)</option>
                <option value="1">Enabled (Scheduled Daily / 每日定时供料)</option>
            </select>
        </div>
        <div class="param-group" id="timerTimeGroup" style="display:none;">
            <label class="highlight">12. Daily Feeding Time (每日定时时间):</label>
            <input type="time" id="etTimerTime" value="08:00">
        </div>
    </div>

    <!-- 基础参数配置 -->
    <div class="param-group">
        <label>1. Target Weight (g):</label>
        <input type="number" id="etWeight" step="0.1" value="100.0">
    </div>
    <div class="param-group">
        <label>2. Target Hold Time (0-10s):</label>
        <input type="number" id="etWeighWait" min="0" max="10" value="2">
    </div>
    <div class="param-group">
        <label>3. Discharge Angle (0-180°):</label>
        <input type="number" id="etServoAngle" min="0" max="180" value="180">
    </div>
    <div class="param-group">
        <label>4. Discharge Hold Time (0-20s):</label>
        <input type="number" id="etServoHold" min="0" max="20" value="3">
    </div>
    <div class="param-group">
        <label>5. Return Time (0-5s):</label>
        <input type="number" id="etCycleInterval" min="0" max="5" value="1">
    </div>
    <div class="param-group">
        <label>6. Weight Error Margin (g):</label>
        <input type="number" id="etWeightErr" step="0.1" value="2.0">
    </div>
    <div class="param-group">
        <label>7. Weight Stability Threshold(ms):</label>
        <input type="number" id="etStableMs" min="100" max="2000" value="300">
    </div>
    <div class="param-group">
        <label>8. Final Dribble Slowdown Value (0-100g):</label>
        <input type="number" id="etSlowDown" min="0" max="100" step="0.1" value="10.0">
    </div>
    <div class="param-group">
        <label>9. Dribble Stabilizing Value (0-5s):</label>
        <input type="number" id="etReduceStable" min="0" max="5" value="2">
    </div>
    <div class="param-group">
        <label class="warning">10. Weighing Calibration Factor (Do Not Alter):</label>
        <input type="number" id="etScaleFactor" step="0.01" value="433.20">
    </div>

    <button class="btn btn-green" onclick="sendParameters()">Apply Settings</button>
</div>

<script>
    const SERVICE_UUID = "0000ffe0-0000-1000-8000-00805f9b34fb";
    const CHARACTERISTIC_UUID = "0000ffe1-0000-1000-8000-00805f9b34fb";

    let bleDevice = null;
    let bleCharacteristic = null;
    let lastRecData = "";

    function toggleTimerInput() {
        let en = document.getElementById('etTimerEnable').value;
        document.getElementById('timerTimeGroup').style.display = (en === "1") ? "block" : "none";
    }

    function fillDeviceParams(paramStr){
        let arr = paramStr.split(',');
        if(arr.length === 13){
            document.getElementById('etWeight').value = arr[0];
            document.getElementById('etWeighWait').value = arr[1];
            document.getElementById('etServoAngle').value = arr[2];
            document.getElementById('etServoHold').value = arr[3];
            document.getElementById('etCycleInterval').value = arr[4];
            document.getElementById('etWeightErr').value = arr[5];
            document.getElementById('etStableMs').value = arr[6];
            document.getElementById('etSlowDown').value = arr[7];
            document.getElementById('etReduceStable').value = arr[8];
            document.getElementById('etScaleFactor').value = arr[9]; 
            
            // 填充定时器数据
            document.getElementById('etTimerEnable').value = arr[10];
            let hh = arr[11].padStart(2, '0');
            let mm = arr[12].padStart(2, '0');
            document.getElementById('etTimerTime').value = `${hh}:${mm}`;
            
            toggleTimerInput();
            document.getElementById('statusText').innerText = "Status: Parameters Synced";
        }
    }

    async function syncSystemTime() {
        if (!bleCharacteristic) return;
        let now = new Date();
        let h = now.getHours();
        let m = now.getMinutes();
        let s = now.getSeconds();
        let timeCmd = `TIME:${h},${m},${s}`;
        let encoder = new TextEncoder();
        await bleCharacteristic.writeValue(encoder.encode(timeCmd));
    }

    async function onConnectClick() {
        if (!bleDevice) {
            try {
                document.getElementById('statusText').innerText = "Searching for Device...";
                bleDevice = await navigator.bluetooth.requestDevice({
                    acceptAllDevices: true,
                    optionalServices: [SERVICE_UUID]
                });
                document.getElementById('statusText').innerText = "Connecting...";
                let gattServer = await bleDevice.gatt.connect();
                const service = await gattServer.getPrimaryService(SERVICE_UUID);
                bleCharacteristic = await service.getCharacteristic(CHARACTERISTIC_UUID);
                await bleCharacteristic.startNotifications();
                bleCharacteristic.addEventListener('characteristicvaluechanged', handleRecData);
                document.getElementById('statusText').innerText = "Connected, Syncing Time...";
                document.getElementById('connectBtn').innerText = "Disconnect";
                document.getElementById('connectBtn').className = "btn btn-red";
                
                // 1. 自动校准ESP32内部时间为手机当前时间
                await syncSystemTime();

                // 2. 发送读取参数指令
                let encoder = new TextEncoder();
                await bleCharacteristic.writeValue(encoder.encode("READ_PARAMS"));
                
                bleDevice.addEventListener('gattserverdisconnected', onDisconnected);
            } catch (error) {
                document.getElementById('statusText').innerText = "Connection Failed：" + error.message;
                bleDevice = null;
                bleCharacteristic = null;
            }
        } else {
            bleDevice.gatt.disconnect();
        }
    }

    function handleRecData(event){
        let decoder = new TextDecoder('utf-8');
        let str = decoder.decode(event.target.value).trim();
        if(str === lastRecData) return;
        lastRecData = str;

        let commaCnt = (str.match(/,/g) || []).length;
        if(commaCnt === 12){  // 13项数据对应12个逗号
            fillDeviceParams(str);
        }else{
            document.getElementById('weightVal').innerText = "Current Real-time Weight: " + str + " g";
        }
    }

    function onDisconnected() {
        document.getElementById('statusText').innerText = "Status: Disconnected";
        document.getElementById('connectBtn').innerText = "Search & Connect Device";
        document.getElementById('connectBtn').className = "btn btn-blue";
        bleDevice = null;
        bleCharacteristic = null;
    }

    async function sendParameters() {
        if (!bleCharacteristic) {
            alert("Please Connect to Bluetooth First");
            return;
        }
        let w = parseFloat(document.getElementById('etWeight').value).toFixed(1);
        let ww = parseInt(document.getElementById('etWeighWait').value);
        let sa = parseInt(document.getElementById('etServoAngle').value);
        let sh = parseInt(document.getElementById('etServoHold').value);
        let ci = parseInt(document.getElementById('etCycleInterval').value);
        let werr = parseFloat(document.getElementById('etWeightErr').value).toFixed(1);
        let stms = parseInt(document.getElementById('etStableMs').value);
        let slow = parseFloat(document.getElementById('etSlowDown').value).toFixed(1);
        let stableT = parseInt(document.getElementById('etReduceStable').value);
        let scaleFac = parseFloat(document.getElementById('etScaleFactor').value).toFixed(2);

        // 获取定时器参数
        let timerEn = parseInt(document.getElementById('etTimerEnable').value);
        let timerTime = document.getElementById('etTimerTime').value.split(':');
        let timerH = parseInt(timerTime[0]);
        let timerM = parseInt(timerTime[1]);

        // 拼接13项参数
        let dataString = `${w},${ww},${sa},${sh},${ci},${werr},${stms},${slow},${stableT},${scaleFac},${timerEn},${timerH},${timerM}`;
        
        let encoder = new TextEncoder();
        try {
            // 下发参数前先自动校准一次当前系统时间
            await syncSystemTime();
            await bleCharacteristic.writeValue(encoder.encode(dataString));
            alert("Parameters Applied Successfully");
        } catch (error) {
            alert("Sending Failed");
        }
    } 
</script>
</body>
</html>
