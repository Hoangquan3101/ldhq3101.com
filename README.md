<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Đếm Ngược Tết Nguyên Đán</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/flipclock/0.7.8/flipclock.css">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/flipclock/0.7.8/flipclock.min.js"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=AllRoundGothic&display=swap');
        
        body {
            font-family: 'AllRoundGothic', sans-serif;
            text-align: center;
            background-color: #282c34;
            color: white;
            transition: background-color 0.5s ease-in-out, color 0.5s ease-in-out;
        }
        .light-mode {
            background-color: white;
            color: black;
        }
        .toggle-theme {
            position: absolute;
            top: 20px;
            right: 20px;
            font-size: 2em;
            cursor: pointer;
        }
        .flip-clock-wrapper {
            margin: 50px auto;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        #current-time {
            margin-top: 20px;
            font-size: 1.5em;
        }
        .timezone-selector {
            margin-top: 20px;
            transition: opacity 0.5s ease-in-out, transform 0.5s ease-in-out;
            opacity: 0;
            transform: translateY(10px);
        }
        select {
            font-size: 1em;
            padding: 5px;
            border-radius: 5px;
        }
        .timezone-selector.show {
            opacity: 1;
            transform: translateY(0);
        }
        .section {
            padding: 50px;
            text-align: left;
            max-width: 800px;
            margin: auto;
        }
    </style>
</head>
<body>
    <div class="toggle-theme" onclick="toggleTheme()">🌙</div>
    <h1>✨TẾT NGUYÊN ĐÁN 2026 BÍNH NGỌ SẮP ĐẾN✨</h1>
    <div class="flip-clock-wrapper" id="countdown"></div>
    <div id="current-time"></div>
    <div class="timezone-selector" id="timezone-container">
        <select id="timezone"></select>
    </div>
    
    <div class="section" id="introduction">
        <h2>Giới thiệu về Tết Nguyên Đán</h2>
        <p>Tết Nguyên Đán, hay còn gọi là Tết Ta, là lễ hội lớn nhất trong năm của người Việt Nam, đánh dấu ngày đầu tiên của năm mới theo lịch âm.</p>
        <p>Hàng năm, Tết được tổ chức vào ngày mồng 1 tháng Giêng âm lịch trên toàn nước Việt Nam và ở một vài nước khác có cộng đồng người Việt sinh sống.</p>
        <p>Sắm cây đào và cây quất ở Bắc Bộ, Bắc Trung Bộ, hay cây mai và dưa hấu ở Nam Trung Bộ và Nam Bộ được coi là sự chuẩn bị không thể thiếu trong những ngày giáp Tết.</p>
        <p>Sau đó, trong những ngày Tết, các gia đình sum họp bên nhau, cùng thăm hỏi người thân, dành những lời chúc mừng, mừng tuổi và thờ cúng tổ tiên.</p>
    </div>
    
    <div class="footer">
        <p>Tác giả: ldhq.3101</p>
    </div>
    
    <script>
        function toggleTheme() {
            document.body.classList.toggle("light-mode");
        }
        function updateCurrentTime() {
            const now = new Date();
            const timezoneOffset = parseFloat(document.getElementById("timezone").value) * 60;
            const localTime = new Date(now.getTime() + timezoneOffset * 60000);
            const days = ["SUN", "MON", "TUE", "WED", "THU", "FRI", "SAT"];
            const day = days[localTime.getUTCDay()];
            const formattedTime = `${day} - ${localTime.getUTCDate().toString().padStart(2, '0')}/${(localTime.getUTCMonth() + 1).toString().padStart(2, '0')}/${localTime.getUTCFullYear()} ${localTime.getUTCHours().toString().padStart(2, '0')}:${localTime.getUTCMinutes().toString().padStart(2, '0')}:${localTime.getUTCSeconds().toString().padStart(2, '0')}`;
            document.getElementById("current-time").textContent = formattedTime;
        }
        setInterval(updateCurrentTime, 1000);
        updateCurrentTime();
        
        function populateTimezones() {
            const timezoneSelect = document.getElementById("timezone");
            const timezones = ["-12", "-11", "-10", "-9.5", "-9", "-8", "-7", "-6", "-5", "-4", "-3.5", "-3", "-2", "-1", "±0", "+1", "+2", "+3", "+3.5", "+4", "+4.5", "+5", "+5.5", "+5.75", "+6", "+7", "+8", "+8.75", "+9", "+9.5", "+10", "+10.5", "+11", "+12", "+12.75", "+13", "+14"];
            timezones.forEach(tz => {
                let option = document.createElement("option");
                option.value = tz.replace("±0", "0");
                option.textContent = `UTC${tz}`;
                timezoneSelect.appendChild(option);
            });
            timezoneSelect.value = "0";
            document.getElementById("timezone-container").classList.add("show");
        }
        populateTimezones();

        $(document).ready(function() {
            var clock = $('#countdown').FlipClock((new Date(2026, 1, 17, 0, 0, 0) - new Date()) / 1000, {
                clockFace: 'DailyCounter',
                countdown: true
            });
        });
    </script>
</body>
</html>
