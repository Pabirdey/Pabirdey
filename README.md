@{
    ViewBag.Title = "Cast House Details";
}
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet" />
<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>

<div class="container mt-3">
    <h4 class="text-primary">Cast House Details</h4>

    <div class="row mb-2">
        <div class="col-md-3">
            <label class="form-label">Date</label>
            <input type="text" class="form-control" value="@DateTime.Now.ToString("dd-MMM-yyyy")" readonly />
        </div>
        <div class="col-md-2">
            <label class="form-label">Furnace</label>
            <select class="form-select">
                <option>H</option>
                <option>G</option>
            </select>
        </div>
    </div>

    <div style="max-height: 250px; overflow-y: auto; border: 1px solid #ccc;">
        <table id="castTable" class="table table-bordered table-sm text-center align-middle mb-0">
            <thead class="table-light sticky-top">
                <tr>
                    <th>Cast No</th>
                    <th>Trough No</th>
                    <th>Cast Start</th>
                    <th>Duration</th>
                    <th>Rate</th>
                    <th>TLC</th>
                    <th>OT</th>
                    <th>Ready Time</th>
                    <th>Wetness</th>
                    <th>Cast Type</th>
                    <th>Clay</th>
                    <th>Taphole</th>
                </tr>
            </thead>
            <tbody></tbody>
        </table>
    </div>
</div>

<script>
    $(document).ready(function () {
        // Load data via AJAX and populate table using JavaScript
        $.ajax({
            url: '@Url.Action("LoadCastData", "CastHouse")',
            type: 'GET',
            success: function (data) {
                var tableBody = "";

                for (var i = 0; i < data.length; i++) {
                    tableBody += "<tr>";
                    tableBody += `<td><input class='form-control form-control-sm' value='${data[i].CastNo}' /></td>`;
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