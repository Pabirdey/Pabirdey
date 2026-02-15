function attachTonEvents() {

    var inputs = document.querySelectorAll(".ton-input");

    for (var i = 0; i < inputs.length; i++) {

        inputs[i].addEventListener("blur", function () {

            var ton = parseFloat(this.value) || 0;
            var kg = ton * 1000;

            var row = this.closest("tr");
            var kgInput = row.querySelector(".kg-input");

            kgInput.value = kg.toFixed(2);
        });
    }
}
function Display_Material(furnace, fDate) {

    fetch('/HML/GetBFRawMaterialByFurnace?furnace=' + furnace + '&fdate=' + fDate)
        .then(response => response.json())
        .then(data => {

            var tbody = document.querySelector("#materialTable tbody");
            tbody.innerHTML = "";

            for (var i = 0; i < data.length; i++) {

                tbody.innerHTML +=
                    "<tr data-tagid='" + data[i].TAG_ID + "'>" +
                    "<td>" + data[i].MATERIAL + "</td>" +
                    "<td><input type='number' class='ton-input' value='" + (data[i].VALUE_TON || "") + "'></td>" +
                    "<td><input type='number' class='kg-input' value='" + (data[i].VALUE_KG || "") + "' readonly></td>" +
                    "</tr>";
            }

            // 🔥 IMPORTANT: Attach event AFTER rows created
            attachTonEvents();

        })
        .catch(error => console.log(error));
}
