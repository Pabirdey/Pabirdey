<script type="text/javascript">
    $(document).ready(function () {

        // Example: Get values from inputs (you can replace with actual values or input field IDs)
        var date = '2025-07-26';         // Replace with actual date
        var fur_name = 'Furnace-A';      // Replace with actual furnace name

        $.ajax({
            url: '@Url.Action("Get_CastDetails", "CastHouse")',
            type: 'GET',
            data: { date: date, fur_name: fur_name }, // 👈 Passing parameters here
            success: function (result) {
                var tableBody = "";
                for (var i = 0; i < result.length; i++) {
                    tableBody += "<tr>";
                    tableBody += `<td><input class='form-control form-control-sm' value='${result[i].CAST_NO}' readonly/></td>`;
                    tableBody += `<td><input class='form-control form-control-sm' value='${result[i].TroughNo}' /></td>`;
                    tableBody += `<td><input class='form-control form-control-sm' value='${result[i].CastStart}' /></td>`;
                    tableBody += `<td><input class='form-control form-control-sm' value='${result[i].Duration}' /></td>`;
                    tableBody += `<td><input class='form-control form-control-sm' value='${result[i].Rate}' /></td>`;
                    tableBody += `<td><input class='form-control form-control-sm' value='${result[i].TLC}' /></td>`;
                    tableBody += `<td><input class='form-control form-control-sm' value='${result[i].OT}' /></td>`;
                    tableBody += `<td><input class='form-control form-control-sm' value='${result[i].Ready}' /></td>`;
                    tableBody += `<td><input class='form-control form-control-sm' value='${result[i].Wetness}' /></td>`;
                    tableBody += `<td><select class='form-select form-select-sm'>
                        <option ${result[i].CastType === 'Normal' ? 'selected' : ''}>Normal</option>
                        <option ${result[i].CastType === 'Emergency' ? 'selected' : ''}>Emergency</option>
                        <option ${result[i].CastType === 'Test' ? 'selected' : ''}>Test</option>
                        </select></td>`;

                    tableBody += `<td><select class='form-select form-select-sm'>
                                    <option ${result[i].Clay === 'Good' ? 'selected' : ''}>Good</option>
                                    <option ${result[i].Clay === 'Soft' ? 'selected' : ''}>Soft</option>
                                    <option ${result[i].Clay === 'Cracked' ? 'selected' : ''}>Cracked</option>
                                  </select></td>`;

                    tableBody += `<td><select class='form-select form-select-sm'>
                                    <option ${result[i].Taphole === 'Normal' ? 'selected' : ''}>Normal</option>
                                    <option ${result[i].Taphole === 'Blocked' ? 'selected' : ''}>Blocked</option>
                                    <option ${result[i].Taphole === 'Leakage' ? 'selected' : ''}>Leakage</option>
                                  </select></td>`;

                    tableBody += "</tr>";
                }

                $("#CastDetailsBody tbody").html(tableBody);
            },
            error: function () {
                alert("Failed to load data.");
            }
        });
    });
</script>
