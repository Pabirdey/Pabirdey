<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Save Data Popup</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            padding: 40px;
        }

        .save-button {
            padding: 10px 20px;
            border: 1px solid #999;
            background-color: #f0f0f0;
            cursor: pointer;
            margin-bottom: 30px;
        }

        .progress-bar {
            width: 300px;
            height: 20px;
            background-color: #eee;
            border-radius: 10px;
            overflow: hidden;
            margin: 20px 0;
            display: none;
        }

        .progress-fill {
            height: 100%;
            width: 0%;
            background-color: #4caf50;
            transition: width 0.1s linear;
        }

        .popup {
            position: relative;
            display: inline-block;
            background-color: #4caf50;
            color: white;
            padding: 12px 20px;
            border-radius: 6px;
            box-shadow: 0 0 10px rgba(0,0,0,0.2);
            animation: slideDown 0.5s ease;
            margin-top: 20px;
            display: none;
        }

        .popup .close-btn {
            position: absolute;
            top: 4px;
            right: 10px;
            cursor: pointer;
            font-size: 16px;
        }

        @keyframes slideDown {
            from {
                transform: translateY(-20px);
                opacity: 0;
            }
            to {
                transform: translateY(0);
                opacity: 1;
            }
        }
    </style>
</head>
<body>

    <button class="save-button" onclick="saveData()">💾 Save Data</button>

    <div class="progress-bar" id="progressBar">
        <div class="progress-fill" id="progressFill"></div>
    </div>

    <div class="popup" id="popup">
        <span class="close-btn" onclick="closePopup()">❌</span>
        Data saved successfully!
    </div>

    <script>
        function saveData() {
            document.getElementById('progressBar').style.display = 'block';
            let progressFill = document.getElementById('progressFill');
            let popup = document.getElementById('popup');
            let width = 0;
            progressFill.style.width = '0%';
            popup.style.display = 'none';

            let interval = setInterval(function () {
                if (width >= 100) {
                    clearInterval(interval);
                    document.getElementById('popup').style.display = 'inline-block';
                    document.getElementById('progressBar').style.display = 'none';
                } else {
                    width++;
                    progressFill.style.width = width + '%';
                }
            }, 30); // Adjust speed here
        }

        function closePopup() {
            document.getElementById('popup').style.display = 'none';
        }
    </script>

</body>
</html>