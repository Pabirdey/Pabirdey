function SaveBFRawMaterialCons() {            

    var materials = [];
    var furnace = document.getElementById("ddlFurnace").value;
    var rows = document.querySelectorAll("#materialTable tbody tr");

    for (var i = 0; i < rows.length; i++) {

        var tagId = rows[i].getAttribute("data-tagid");
        var ton = parseFloat(rows[i].querySelector(".ton-input").value) || 0;
        var materialName = rows[i].querySelector("td").innerText.trim(); // WEB_COLUMN

        var finalValue;

        // ✅ Condition: Furnace F AND Pellet → DO NOT multiply
        if (furnace === "F" && materialName === "Pellet") {
            finalValue = ton;
        } 
        else {
            finalValue = ton * 1000;
        }

        materials.push({
            TAG_ID: tagId,
            VALUE_TON: finalValue
        });
    }

    var data = {
        FDate: lsSelectedFDate,
        furnace: furnace,
        materials: materials
    };

    $.ajax({
        url: '/HML/SaveBFRawMaterialData',
        type: 'POST',
        contentType: 'application/json',
        data: JSON.stringify(data),
        success: function (res) {
            alert(res.message);
        },
        error: function () {
            alert("Error saving data");
        }
    });
}
