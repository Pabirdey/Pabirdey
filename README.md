function Display_Tap_Hole_Details() {
                $.ajax({
                    url: '@Url.Action("Get_TAP_Hole_Metal_Details", "CastHouse")',
                    type: 'GET',
                    data: { date: date, Fur_name: Fur_name },
                    success: function (result_Tap_Hole_Metal) {
                        var TAP_Hot_Metal_Details = "";
                        for (var i = 0; i < result_Tap_Hole_Metal.length; i++) {
                            tableBody += "<tr>";
                            tableBody += `<td><input class='form-control form-control-sm' value='${data[i].CAST_NO}' readonly/></td>`;
                            tableBody += `<td><input class='form-control form-control-sm' value='${data[i].TROUGH_NO}'/></td>`;
                            tableBody += `<td><input class='form-control form-control-sm' value='${data[i].CAST_ST_TIME}'/></td>`;
                            tableBody += `<td><input class='form-control form-control-sm' value='${data[i].CAST_END_TIME}'/></td>`;
                            tableBody += "</tr>";
                        }
                        $("#CastDetailsBody tbody").html(tableBody);
                    },
                    error: function () {
                        alert("Failed to load data.");
                    }             
                });
            }
        }
