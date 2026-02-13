function saveData() {

    var materials = [];
    var rows = document.querySelectorAll("#myTable tbody tr");

    for (var i = 0; i < rows.length; i++) {

        var tagId = rows[i].querySelector(".tagid").value;
        var ton = rows[i].querySelector(".ton").value;
        var kg = rows[i].querySelector(".kg").value;

        materials.push({
            TAG_ID: tagId,
            VALUE_TON: ton,
            VALUE_KG: kg
        });
    }

    var data = {
        reportDate: document.getElementById("reportDate").value,
        furnace: document.getElementById("furnace").value,
        materials: materials
    };

    $.ajax({
        url: '/YourController/SaveRawMaterialData',
        type: 'POST',
        contentType: 'application/json; charset=utf-8',
        dataType: 'json',
        data: JSON.stringify(data),
        success: function (res) {
            alert(res.message);
        },
        error: function () {
            alert("Error saving data");
        }
    });
}
