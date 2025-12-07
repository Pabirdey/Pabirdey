function Display_Drilling_Details(lsSelectedFDate, IsSelectedFur) {
    $.ajax({
        url: '/CastHouse/Get_Drilling_Slag_Details',
        type: 'GET',
        data: { Fdate: lsSelectedFDate, Fur: IsSelectedFur },
        success: function (resultData) {

            var parsedData = JSON.parse(resultData);
            var tableBody = "";

            for (var i = 0; i < parsedData.length; i++) {

                tableBody += `<tr data-castno='${parsedData[i].CAST_NO}'>`;

                tableBody += `<td><input class="form-control form-control-lg" name="CAST_NO" value="${parsedData[i].CAST_NO}" readonly/></td>`;
                tableBody += `<td><input class="form-control form-control-lg" name="DRILL_DIA" value="${parsedData[i].DRILL_DIA}"/></td>`;
                tableBody += `<td><input class="form-control form-control-lg" name="DRILL_TYPE" value="${parsedData[i].DRILL_TYPE}"/></td>`;
                tableBody += `<td><input class="form-control form-control-lg" name="TOTAL_DRILLING_TIME" value="${parsedData[i].TOTAL_DRILLING_TIME}"/></td>`;
                // Add remaining fields...

                tableBody += "</tr>";
            }

            $("#Driling_Slag_Details tbody").html(tableBody);
        }
    });
}