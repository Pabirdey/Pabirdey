<div class="row mb-2">
    <div class="col-md-3">
        <label>Furnace</label>
        <select id="ddlFurnace" class="form-control">
            <option value="BF1">BF1</option>
            <option value="BF2">BF2</option>
            <option value="BF3">BF3</option>
        </select>
    </div>

    <div class="col-md-3">
        <label>Date</label>
        <input type="text" id="date-daily1" class="form-control" autocomplete="off" />
    </div>

    <div class="col-md-3">
        <label>&nbsp;</label><br />
        <button class="btn btn-primary" id="btnLoad">Load Material</button>
    </div>
</div>

<h4 id="currDate-value" class="text-primary fw-bold"></h4>

<table id="materialTable" class="table table-bordered table-striped">
    <thead>
        <tr>
            <th>MATERIAL</th>
            <th>VALUE TON</th>
            <th>VALUE KG</th>
        </tr>
    </thead>
    <tbody></tbody>
</table>


<script type="text/javascript">
    $(document).ready(function () {

        // Default Yesterday Date
        var caldate1 = '@DateTime.Today.AddDays(-1).ToString("dd/MM/yyyy",
                new System.Globalization.CultureInfo("en-GB"))';

        $('#currDate-value').html(caldate1);

        // Date Picker
        $('#date-daily1').datepicker({
            format: "dd/mm/yyyy",
            autoclose: true,
            todayHighlight: true
        }).datepicker("setDate", caldate1);


        // On Date Change -> Reload Data
        $('#date-daily1').on('changeDate', function () {
            caldate1 = $('#date-daily1').datepicker('getFormattedDate');
            $('#currDate-value').html(caldate1);

            var furnace = $("#ddlFurnace").val();
            Display_Material(furnace, caldate1);
        });


        // Button Click Load
        $("#btnLoad").click(function () {
            var furnace = $("#ddlFurnace").val();
            var fDate = $("#date-daily1").val();
            Display_Material(furnace, fDate);
        });


        // Furnace Change Load
        $("#ddlFurnace").change(function () {
            var furnace = $("#ddlFurnace").val();
            var fDate = $("#date-daily1").val();
            Display_Material(furnace, fDate);
        });


        // ================= FUNCTION ===================
        function Display_Material(furnace, fDate) {

            $.ajax({
                url: '@Url.Action("GetRawMaterialByFurnace","HML")',
                type: 'GET',
                data: { furnace: furnace, fdate: fDate },

                success: function (data) {

                    var tbody = $("#materialTable tbody");
                    tbody.empty();

                    for (var i = 0; i < data.length; i++) {
                        var row = "<tr>" +
                            "<td class='fw-bold'>" + data[i].MATERIAL + "</td>" +
                            "<td><input type='text' class='form-control medium-textbox' value='" + data[i].VALUE_TON + "'></td>" +
                            "<td><input type='text' class='form-control medium-textbox' value='" + data[i].VALUE_KG + "'></td>" +
                            "</tr>";

                        tbody.append(row);
                    }
                },

                error: function (xhr) {
                    alert("Error: " + xhr.responseText);
                }
            });
        }

        // Load first time on page load
        Display_Material($("#ddlFurnace").val(), caldate1);
    });
</script>