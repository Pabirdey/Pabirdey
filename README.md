<!DOCTYPE html>
<html>
<head>
    <title>Custom Input List Without Datalist</title>

    <style>
        body {
            font-family: Arial;
            padding: 40px;
        }

        .container {
            position: relative;
            width: 250px;
        }

        .form-control {
            width: 100%;
            padding: 6px;
            font-size: 14px;
        }

        .list-box {
            position: absolute;
            top: 34px;
            left: 0;
            width: 100%;
            border: 1px solid #999;
            background: #fff;
            max-height: 150px;
            overflow-y: auto;
            display: none;
            z-index: 999;
        }

        .list-box div {
            padding: 6px;
            cursor: pointer;
        }

        .list-box div:hover {
            background: #e6e6e6;
        }

        .mt-10 {
            margin-top: 10px;
        }
    </style>
</head>

<body>

    <h3>Input with List (Without Datalist)</h3>

    <div class="container">
        <input type="text" id="clayInput"
               class="form-control"
               placeholder="Select or type"
               autocomplete="off"
               onclick="showList()"
               onkeyup="filterList()" />

        <div id="clayList" class="list-box">
            <div onclick="selectItem(this)">LRH</div>
            <div onclick="selectItem(this)">UBQ</div>
            <div onclick="selectItem(this)">SARVESH</div>
            <div onclick="selectItem(this)">CALDYRS</div>
            <div onclick="selectItem(this)">HARIMA</div>
            <div onclick="selectItem(this)">OTHERS</div>
        </div>
    </div>

    <!-- Other Clay Input -->
    <input type="text" id="otherClay"
           class="form-control mt-10"
           placeholder="Enter Other Clay"
           style="display:none; width:250px;" />

    <script>
        function showList() {
            document.getElementById("clayList").style.display = "block";
        }

        function filterList() {
            var input = document.getElementById("clayInput").value.toUpperCase();
            var items = document.getElementById("clayList").getElementsByTagName("div");

            document.getElementById("clayList").style.display = "block";

            for (var i = 0; i < items.length; i++) {
                var txt = items[i].innerText.toUpperCase();
                items[i].style.display = (txt.indexOf(input) > -1) ? "" : "none";
            }
        }

        function selectItem(el) {
            var value = el.innerText;
            document.getElementById("clayInput").value = value;
            document.getElementById("clayList").style.display = "none";

            if (value === "OTHERS") {
                document.getElementById("otherClay").style.display = "block";
            } else {
                document.getElementById("otherClay").style.display = "none";
            }
        }

        // Close list when clicking outside
        document.addEventListener("click", function (e) {
            if (!e.target.closest(".container")) {
                document.getElementById("clayList").style.display = "none";
            }
        });
    </script>

</body>
</html>