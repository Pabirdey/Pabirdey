$("#ddlFurnace").change(function () {

    var furnace = $(this).val();

    $.ajax({
        url: "/HML/GetATOFBinDetails",
        type: "POST",
        data: { furnace: furnace },
        success: function (data) {

            var tbody = $("#tblBinDetails tbody");
            tbody.empty();

            for (var i = 0; i < data.length; i++) {

                var selectedY = data[i].REQUIRED === "Y" ? "selected" : "";
                var selectedN = data[i].REQUIRED === "N" ? "selected" : "";

                var row = "<tr>" +
                    "<td>" + data[i].WEB_SL_NO + "</td>" +
                    "<td>" + data[i].FUR_NAME + "</td>" +
                    "<td>" + data[i].TAG_NAME + "</td>" +
                    "<td>" + data[i].WEB_COLUMN + "</td>" +
                    "<td>" + data[i].TAG_TYPE + "</td>" +
                    "<td>" +
                        "<select>" +
                            "<option value='Y' " + selectedY + ">Y</option>" +
                            "<option value='N' " + selectedN + ">N</option>" +
                        "</select>" +
                    "</td>" +
                    "</tr>";

                tbody.append(row);
            }
        },
        error: function () {
            alert("Error loading data");
        }
    });

});