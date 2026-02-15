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
                Display_ValueKg();
            }
        });
    }
