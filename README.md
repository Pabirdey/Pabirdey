 function Display_Mudgun_Details(lsSelectedFDate, IsSelectedFur) {
                $.ajax({
                    url: '@Url.Action("Get_Display_Mudgun_Details", "CastHouse")',
                    type: 'GET',
                    data: { Fdate: lsSelectedFDate, Fur: IsSelectedFur },
                    success: function (result_Mudgun_Details) {
                    var parsedData = JSON.parse(result_Mudgun_Details);
                    var tableBody = "";
                    for (var i = 0; i < parsedData.length; i++) {
                        tableBody += "<tr>";
                        tableBody += `<td><input name="CAST_NO" class='form-control form-control-lg' value='${parsedData[i].CAST_NO}' readonly/></td>`;                       
                tableBody += `<td><input name="CLAY_QUANTITY" class='form-control form-control-lg' value='${parsedData[i].CLAY_QUANTITY}'/></td>`;
                tableBody += `<td>
                    <select name="MG_CLAY_USED" class='form-select form-select-lg'>
                        <option ${!parsedData[i].MG_CLAY_USED ? 'selected' : ''} value=""></option>
                        ${[
                            'ACE','BRL','LRH','UBQ','SARVESH','CALDYRS','HARIMA(S)','HARIMA(D)','CORUS','TRB','VISUVIUS',
                            'HARIMA-TWH4','HARIMA-CPH4','HARIMA(D)-TWH5','HARIMA(D)-TWH5K','HARIMA(D)-TWH-5T','HARIMA RWH-3',
                            'HARIMA RWH-4','HARIMA(S)-RW5F','HARIMA(S)-RG15K','OTHERS'
                        ].map(option => `<option ${parsedData[i].MG_CLAY_USED === option ? 'selected' : ''}>${option}</option>`).join("")}
                    </select>
                </td>`;               
                tableBody += "</tr>";
            }
            $("#Mudgun_Details tbody").html(tableBody);
        }
    });
}
