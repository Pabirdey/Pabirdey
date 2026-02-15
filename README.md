function Display_Material(furnace, fDate) {
        $.ajax({
            url: '@Url.Action("GetBFRawMaterialByFurnace", "HML")',
            type: 'GET',
            data: { furnace: furnace, fdate: fDate },
            success: function (data) {
                var tbody = $("#materialTable tbody");
                tbody.empty();

                for (var i = 0; i < data.length; i++) {
                    tbody.append(
                        "<tr data-tagid='" + data[i].TAG_ID + "'>" +
                        "<td>" + data[i].MATERIAL + "</td>" +
                        "<td><input class='ton-input form-control medium-textbox' value='" + data[i].VALUE_TON + "'></td>" +
                        "<td><input class='kg-input form-control medium-textbox' value='" + data[i].VALUE_KG + "'></td>" +
                        "</tr>"
                    );
                }
            }
        });
    }

        function SaveBFRawMaterialCons() {            
        var materials = [];
        var rows = document.querySelectorAll("#materialTable tbody tr");
        for (var i = 0; i < rows.length; i++) {
            var tagId = rows[i].getAttribute("data-tagid");
            var ton = rows[i].querySelector(".ton-input").value;
            materials.push({
                TAG_ID: tagId,
                VALUE_TON: ton                
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

        var tonInputs = document.querySelectorAll(".ton-input");
        for (var i = 0; i < tonInputs.length; i++) {
            tonInputs[i].addEventListener("blur", function () {
                var ton = parseFloat(this.value) || 0;
                var kg = ton * 1000;
                var row = this.closest("tr");
                var kgInput = row.querySelector(".kg-input");
                kgInput.value = kg.toFixed(2);
            });

        }
