<!DOCTYPE html>
<html>
<head>
    <title>Save Message Popup</title>
    <style>
        /* Basic Page Styling */
        body {
            font-family: Arial, sans-serif;
            padding: 50px;
        }

        /* Popup Message Style */
        #popupMessage {
            position: fixed;
            top: -100px; /* Start above the screen */
            left: 50%;
            transform: translateX(-50%);
            background-color: #28a745;
            color: white;
            padding: 15px 30px;
            border-radius: 10px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.2);
            transition: top 0.5s ease-in-out;
            z-index: 1000;
        }

        /* Show class moves it down */
        #popupMessage.show {
            top: 30px;
        }

        button {
            padding: 10px 20px;
            font-size: 16px;
            cursor: pointer;
        }
    </style>
</head>
<body>

    <button onclick="saveData()">Save Data</button>

    <div id="popupMessage">Data saved successfully!</div>

    <script>
        function saveData() {
            // Simulate data saving logic here if needed

            var popup = document.getElementById("popupMessage");
            popup.classList.add("show");

            // Hide the popup after 3 seconds
            setTimeout(function () {
                popup.classList.remove("show");
            }, 3000);
        }
    </script>

</body>
</html>