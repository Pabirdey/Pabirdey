public ActionResult GetMaterials()
{
    List<string> materials = new List<string>();

    using (OracleConnection con = new OracleConnection("YOUR_CONN"))
    {
        con.Open();
        string query = "SELECT MATERIAL_NAME FROM T_MATERIAL_MASTER ORDER BY MATERIAL_NAME";

        using (OracleCommand cmd = new OracleCommand(query, con))
        using (OracleDataReader dr = cmd.ExecuteReader())
        {
            while (dr.Read())
            {
                materials.Add(dr["MATERIAL_NAME"].ToString());
            }
        }
    }
    return Json(materials, JsonRequestBehavior.AllowGet);
}
<table id="materialTable" class="table table-bordered" style="width:60%;">
    <thead>
        <tr>
            <th>Material</th>
            <th>Value (Tons)</th>
            <th>Value (Kgs)</th>
        </tr>
    </thead>
    <tbody></tbody>
</table>

<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>

<script>
$(document).ready(function () {

    $.ajax({
        url: '/Home/GetMaterials',
        type: 'GET',
        success: function (data) {
            var tbody = $("#materialTable tbody");

            for (var i = 0; i < data.length; i++) {

                var row = "<tr>" +
                    "<td>" + data[i] + "</td>" +
                    "<td><input type='text' class='form-control' id='ton_" + i + "'></td>" +
                    "<td><input type='text' class='form-control' id='kg_" + i + "'></td>" +
                    "</tr>";

                tbody.append(row);
            }
        }
    });

});
</script>
