 $.ajax({
            url: '@Url.Action("LoadOtherDetails", "CastHouse")',
            type: 'GET',
            success: function (data) {
                var tableBody = "";
                for (var i = 0; i < data.length; i++) {
                    tableBody += "<tr>";
                    tableBody += "<td>" + data[i].CastNo + "</td>";
                    tableBody += "<td>" + data[i].Date + "</td>";
                    tableBody += "<td>" + data[i].Furnace + "</td>";
                    tableBody += "<td>" + data[i].MainRunnerHMAmt + "</td>";
                    tableBody += "<td>" + data[i].TiltingRunnerHMAmt + "</td>";
                    tableBody += "<td>" + data[i].Remarks + "</td>";
                    tableBody += "</tr>";
                }
                $("#otherDetailsBody").html(tableBody);
            }
        });
