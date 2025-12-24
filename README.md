<div class="row mb-2">
    <div class="col-md-3">
        <label>Furnace</label>
        <select id="ddlFurnace" class="form-control">
            <option value="BF1">BF1</option>
            <option value="BF2">BF2</option>
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

        var caldate1 = '@DateTime.Today.AddDays(-1).ToString("dd/MM/yyyy", 
                    new System.Globalization.CultureInfo("en-GB"))';

        $('#currDate-value').html(caldate1);

        $('#date-daily1').datepicker({
            format: "dd/mm/yyyy",
            autoclose: true,
            todayHighlight: true
        }).datepicker("setDate", caldate1);


        $('#date-daily1').on('changeDate', function () {
            caldate1 = $('#date-daily1').datepicker('getFormattedDate');
            $('#currDate-value').html(caldate1);
        });


        $("#btnLoad").click(function () {
            var furnace = $("#ddlFurnace").val();
            var fDate = $("#date-daily1").val();

            Display_Material(furnace, fDate);
        });


        //================ FUNCTION ===================
        function Display_Material(furnaceName, fDate) {
            $.ajax({
                url: '@Url.Action("GetRawMaterialByFurnace","HML")',
                type: 'GET',
                data: { furnace: furnaceName, fdate: fDate },

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

        // Load automatically first time
        Display_Material($("#ddlFurnace").val(), caldate1);
    });
</script>


[HttpGet]
public ActionResult GetRawMaterialByFurnace(string furnace, string fdate)
{
    var list = new List<Dictionary<string, object>>();

    using (OracleConnection conn = new OracleConnection(iMonitorWebUtils.msConRWString))
    {
        conn.Open();

        using (OracleCommand cmd = new OracleCommand("PROC_GET_RAW_MATERIAL", conn))
        {
            cmd.CommandType = CommandType.StoredProcedure;

            cmd.Parameters.Add("p_furnace", OracleDbType.Varchar2).Value = furnace;
            cmd.Parameters.Add("p_date", OracleDbType.Varchar2).Value = fdate;
            cmd.Parameters.Add("p_cursor", OracleDbType.RefCursor).Direction = ParameterDirection.Output;

            using (OracleDataReader dr = cmd.ExecuteReader())
            {
                while (dr.Read())
                {
                    var row = new Dictionary<string, object>();
                    row["MATERIAL"] = dr["MATERIAL_NAME"].ToString();
                    row["VALUE_TON"] = dr["VALUE_TON"].ToString();
                    row["VALUE_KG"] = dr["VALUE_KG"].ToString();
                    list.Add(row);
                }
            }
        }
    }

    return Json(list, JsonRequestBehavior.AllowGet);
}