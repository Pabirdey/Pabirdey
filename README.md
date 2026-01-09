<!DOCTYPE html>
<html>
<head>
    <title>Input with Separate Arrow List</title>

    <style>
        body {
            font-family: Arial;
            padding: 40px;
        }

        .input-wrapper {
            display: flex;
            width: 300px;
            border: 1px solid #999;
        }

        .input-wrapper input {
            flex: 1;
            border: none;
            padding: 6px;
            outline: none;
        }

        .arrow-btn {
            width: 30px;
            border-left: 1px solid #999;
            cursor: pointer;
            text-align: center;
            background: #f0f0f0;
            user-select: none;
        }

        .arrow-btn:hover {
            background: #ddd;
        }

        .list-box {
            width: 300px;
            border: 1px solid #999;
            border-top: none;
            display: none;
            background: #fff;
        }

        .list-box div {
            padding: 6px;
            cursor: pointer;
        }

        .list-box div:hover {
            background: #e6e6e6;
        }
    </style>
</head>

<body>

<h3>Textbox with Arrow Dropdown</h3>

<div class="input-wrapper">
    <input type="text" id="txtInput" placeholder="Type or select">
    <div class="arrow-btn" onclick="toggleList()">▼</div>
</div>

<div id="list" class="list-box">
    <div onclick="selectItem(this)">VISUVUS</div>
    <div onclick="selectItem(this)">ETNA</div>
    <div onclick="selectItem(this)">FUJI</div>
    <div onclick="selectItem(this)">OTHERS</div>
</div>

<script>
function toggleList() {
    var list = document.getElementById("list");
    list.style.display = list.style.display === "block" ? "none" : "block";
}

function selectItem(el) {
    document.getElementById("txtInput").value = el.innerText;
    document.getElementById("list").style.display = "none";
}

// close list when clicking outside
document.addEventListener("click", function (e) {
    if (!e.target.closest(".input-wrapper") &&
        !e.target.closest("#list")) {
        document.getElementById("list").style.display = "none";
    }
});
</script>

</body>
</html>