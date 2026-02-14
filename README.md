  function SaveBFRawMaterialCons() {
            debugger;
        var materials = [];
        var rows = document.querySelectorAll("#materialTable tbody tr");
        for (var i = 0; i < rows.length; i++) {
            var tagId = rows[i].getAttribute("data-tagid");
            var ton = rows[i].querySelector(".ton").value;
            var kg = rows[i].querySelector(".kg").value;
            materials.push({
                TAG_ID: tagId,
                VALUE_TON: ton,
                VALUE_KG: kg
            });
        }
        var data = {
            FDate: lsSelectedFDate,
            furnace: document.getElementById("ddlFurnace").value,
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
