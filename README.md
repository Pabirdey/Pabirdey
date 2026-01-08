<!DOCTYPE html>
<html>
<head>
    <title>Editable List Without Datalist</title>

    <style>
        body {
            font-family: Arial;
            padding: 20px;
        }
        .form-control {
            width: 250px;
            padding: 6px;
            margin-top: 5px;
        }
    </style>
</head>
<body>

    <h3>Editable List (No Datalist)</h3>

    <!-- Dropdown -->
    <select id="claySelect" class="form-control" onchange="onSelectChange()">
        <option value="">-- Select Clay --</option>
        <option value="LRH">LRH</option>
        <option value="UBQ">UBQ</option>
        <option value="SARVESH">SARVESH</option>
        <option value="CALDYRS">CALDYRS</option>
        <option value="OTHERS">OTHERS</option>
    </select>

    <!-- Textbox for new item -->
    <input type="text" id="editBox" class="form-control"
           placeholder="Enter new item"
           style="display:none"
           onkeydown="addOnEnter(event)"
           onblur="addNewItem()">

    <p id="msg" style="color:green;margin-top:10px;"></p>

    <script>
        function onSelectChange() {
            var sel = document.getElementById("claySelect");
            var txt = document.getElementById("editBox");
            document.getElementById("msg").innerText = "";

            if (sel.value === "OTHERS") {
                txt.value = "";
                txt.style.display = "block";
                txt.focus();
            } else {
                txt.style.display = "none";
            }
        }

        function addOnEnter(e) {
            if (e.key === "Enter") {
                addNewItem();
            }
        }

        function addNewItem() {
            var sel = document.getElementById("claySelect");
            var txt = document.getElementById("editBox");
            var val = txt.value.trim();

            if (val === "") return;

            // Check duplicate
            for (var i = 0; i < sel.options.length; i++) {
                if (sel.options[i].value.toLowerCase() === val.toLowerCase()) {
                    sel.value = sel.options[i].value;
                    txt.style.display = "none";
                    document.getElementById("msg").innerText = "Item already exists.";
                    return;
                }
            }

            // Create new option
            var opt = document.createElement("option");
            opt.value = val;
            opt.text = val;

            sel.add(opt);
            sel.value = val;

            txt.style.display = "none";
            document.getElementById("msg").innerText = "New item added successfully.";
        }
    </script>

</body>
</html>