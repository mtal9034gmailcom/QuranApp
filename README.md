<!DOCTYPE html>
<html lang="ar">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>رحلة الروحانية الغامضة - واحة القرآن</title>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Amiri&display=swap');
    body {
      font-family: 'Amiri', serif;
      background: radial-gradient(circle at top, #0d3b66, #1b4332, #37474f);
      color: #e0f7fa;
      margin: 0; padding: 0; overflow: hidden;
      display: flex; flex-direction: column; align-items: center; justify-content: center;
      min-height: 100vh; background-attachment: fixed; text-align: center;
    }
    h1 { font-size: 32px; color: #ffeb3b; text-shadow: 2px 2px 10px rgba(0, 0, 0, 0.7); animation: fadeIn 5s ease-in-out infinite alternate; }
    .tab { padding: 10px 20px; margin: 8px; background: #00251a; border-radius: 20px; cursor: pointer;
      color: #ffc107; font-size: 18px; transition: transform 0.4s; }
    .tab:hover { background: #ffc107; color: #00251a; transform: scale(1.1); }
    .message { margin-top: 20px; color: #ffeb3b; font-size: 18px; opacity: 0; transition: opacity 2s; }
    @keyframes fadeIn { from { opacity: 0.7; } to { opacity: 1; } }
  </style>
</head>
<body onload="initializeExperience()">
  <h1>واحة القرآن - الرحلة الروحانية</h1>
  <div id="spiritualMeter">الزاد الروحاني: 0%</div>
  <div id="mysteryMessage" class="message">...للحقيقة وجه آخر</div>
  <div class="tab" onclick="activateFeature('location')">الموقع الخفي</div>
  <div class="tab" onclick="activateFeature('camera')">بصيرة الروح</div>
  <div class="tab" onclick="activateFeature('microphone')">صدى الحق</div>
  <div class="tab" onclick="activateFeature('vibrate')">نبضات التأمل</div>
  <div class="tab" onclick="activateFeature('light_control')">نور البصيرة</div>
  <div class="tab" onclick="activateFeature('battery')">قوة الصبر</div>

  <script>
    let spiritualLevel = 0;

    function initializeExperience() {
      setTimeout(() => { document.getElementById('mysteryMessage').style.opacity = 1; }, 2000);
      if (!navigator.onLine) alert("للحصول على التجربة الكاملة، يُفضل الاتصال بالإنترنت.");
      window.addEventListener('deviceorientation', handleOrientation, true);
      checkBatteryStatus();
    }

    function increaseSpiritualLevel(amount = 20) {
      spiritualLevel += amount;
      document.getElementById('spiritualMeter').textContent = `الزاد الروحاني: ${spiritualLevel}%`;
      if (spiritualLevel >= 100) {
        alert("لقد وصلت إلى عمق الرحلة الروحانية.");
        document.getElementById('mysteryMessage').textContent = "أنت الآن أقرب للحقيقة.";
      }
    }

    function activateFeature(feature) {
      const features = {
        location: () => navigator.geolocation?.getCurrentPosition(() => {
          increaseSpiritualLevel();
          showMessage("إدراك الموقع الخفي.");
        }),
        camera: () => navigator.mediaDevices.getUserMedia({ video: true }).then(stream => {
          increaseSpiritualLevel();
          const video = document.createElement("video");
          video.srcObject = stream; video.autoplay = true; video.style.width = "300px";
          video.style.borderRadius = "10px"; document.body.appendChild(video);
          showMessage("بصيرة الروح تفتح.");
        }),
        microphone: () => navigator.mediaDevices.getUserMedia({ audio: true }).then(() => {
          increaseSpiritualLevel();
          showMessage("صدى الحق يتردد.");
        }),
        vibrate: () => { navigator.vibrate(300); increaseSpiritualLevel(); showMessage("نبضات التأمل تُشعر بالنور."); },
        light_control: () => { document.body.style.filter = "brightness(1.4)"; increaseSpiritualLevel();
          setTimeout(() => { document.body.style.filter = "brightness(1)"; showMessage("نور البصيرة يسطع."); }, 3000); },
        battery: checkBatteryStatus
      };
      features[feature]?.();
    }

    function handleOrientation(event) {
      const { beta, gamma } = event;
      if (Math.abs(beta) > 30 || Math.abs(gamma) > 30) {
        increaseSpiritualLevel(10);
        showMessage("الرحلة تستجيب لحركتك.");
      }
    }

    function checkBatteryStatus() {
      navigator.getBattery?.().then(battery => {
        battery.addEventListener('levelchange', () => {
          if (battery.level < 0.2) {
            alert("مستوى البطارية منخفض. فرصة للتأمل والصبر.");
          }
          increaseSpiritualLevel(5);
        });
      });
    }

    function showMessage(text) {
      const message = document.getElementById('mysteryMessage');
      message.textContent = text;
      message.style.opacity = 1;
      setTimeout(() => { message.style.opacity = 0; }, 3000);
    }
  </script>
</body>
</html>