<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Slide-down Success Message</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            padding: 50px;
        }

        .save-button {
            padding: 10px 20px;
            background-color: #f0f0f0;
            border: 1px solid #999;
            cursor: pointer;
        }

        .popup-message {
            position: fixed;
            top: -100px;
            left: 50%;
            transform: translateX(-50%);
            background-color: #4caf50;
            color: white;
            padding: 15px 25px;
            border-radius: 5px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.2);
            opacity: 0;
            transition: top 0.5s ease, opacity 0.5s ease;
            z-index: 1000;
        }

        .popup-message.show {
            top: 40px;
            opacity: 1;
        }
    </style>
</head>
<body>

    <button class="save-button" onclick="showSuccess()">💾 Save Data</button>

    <div class="popup-message" id="popupMessage">
        ✅ Data saved successfully!
    </div>

    <script>
        function showSuccess() {
            var popup = document.getElementById('popupMessage');
            popup.classList.add('show');

            // Hide after 3 seconds
            setTimeout(function () {
                popup.classList.remove('show');
            }, 3000);
        }
    </script>

</body>
</html>