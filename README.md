<script>
        $(document).ready(function () {
            $.ajax({
                url: '@Url.Action("LoadCastData", "CastHouse")',
                type: 'GET',
                success: function (data) {
                    var tableBody = "";
                    for (var i = 0; i < data.length; i++) {
                        tableBody += "<tr>";
                        tableBody += `<td><input class='form-control form-control-sm' value='${data[i].CastNo}' readonly/></td>`;
                        tableBody += `<td><input class='form-control form-control-sm' value='${data[i].TroughNo}' /></td>`;
                        tableBody += `<td><input class='form-control form-control-sm' value='${data[i].CastStart}' /></td>`;
                        tableBody += `<td><input class='form-control form-control-sm' value='${data[i].Duration}' /></td>`;
                        tableBody += `<td><input class='form-control form-control-sm' value='${data[i].Rate}' /></td>`;
                        tableBody += `<td><input class='form-control form-control-sm' value='${data[i].TLC}' /></td>`;
                        tableBody += `<td><input class='form-control form-control-sm' value='${data[i].OT}' /></td>`;
                        tableBody += `<td><input class='form-control form-control-sm' value='${data[i].Ready}' /></td>`;
                        tableBody += `<td><input class='form-control form-control-sm' value='${data[i].Wetness}' /></td>`;
                        tableBody += `<td><select class='form-select form-select-sm'>
                        <option ${data[i].CastType === 'Normal' ? 'selected' : ''}>Normal</option>
                        <option ${data[i].CastType === 'Emergency' ? 'selected' : ''}>Emergency</option>
                        <option ${data[i].CastType === 'Test' ? 'selected' : ''}>Test</option>
                        </select></td>`;

                        tableBody += `<td><select class='form-select form-select-sm'>
                                    <option ${data[i].Clay === 'Good' ? 'selected' : ''}>Good</option>
                                    <option ${data[i].Clay === 'Soft' ? 'selected' : ''}>Soft</option>
                                    <option ${data[i].Clay === 'Cracked' ? 'selected' : ''}>Cracked</option>
                                  </select></td>`;

                        tableBody += `<td><select class='form-select form-select-sm'>
                                    <option ${data[i].Taphole === 'Normal' ? 'selected' : ''}>Normal</option>
                                    <option ${data[i].Taphole === 'Blocked' ? 'selected' : ''}>Blocked</option>
                                    <option ${data[i].Taphole === 'Leakage' ? 'selected' : ''}>Leakage</option>
                                  </select></td>`;

                        tableBody += "</tr>";
                    }

                    $("#castTable tbody").html(tableBody);
                },
                error: function () {
                    alert("Failed to load data.");
                }
            });
        });
</script>
