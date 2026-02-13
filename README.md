unction Display_Material(furnace, fDate) {
    $.ajax({
        url: '@Url.Action("GetRawMaterialByFurnace","HML")',
        type: 'GET',
        data: { furnace: furnace, fdate: fDate },
        success: function (data) {
            var tbody = $("#materialTable tbody");
            tbody.empty();
            for (var i = 0; i < data.length; i++) {
                tbody.append("<tr>" +
                    "<tr data-tagid='" + data[i].TAG_ID + "'>" +
                    "<td class='material'>" + data[i].MATERIAL + "</td>" +
                    "<td><input class='ton form-control medium-textbox' value='" + data[i].VALUE_TON + "'></td>" +
                    "<td><input class='kg form-control medium-textbox' value='" + data[i].VALUE_KG + "'></td>" +
                    "</tr>"
                );
            }
            
        }
    });
}    
