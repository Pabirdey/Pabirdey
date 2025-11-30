function loadMaterials(furnaceName) {

    $.ajax({
        url: '/HML/GetMaterialsByFurnace',
        type: 'GET',
        data: { furnace: furnaceName },
        success: function (data) {

            var tbody = $("#materialTable tbody");
            tbody.empty();

            for (var i = 0; i < data.length; i++) {

                var row = "<tr>" +
                    "<td>" + data[i].MATERIAL + "</td>" +
                    "<td><input type='text' class='form-control medium-textbox' value='" + data[i].TONS + "' id='VAL_TONS" + i + "'></td>" +
                    "<td><input type='text' class='form-control medium-textbox' value='" + data[i].KGS + "' id='VAL_KGS" + i + "'></td>" +
                    "</tr>";

                tbody.append(row);
            }
        }
    });
}
public ActionResult GetMaterialsByFurnace(string furnace)
{
    var list = new List<object>();

    using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
    {
        con.Open();

        string sql = @"Select WEB_COLUMN,VAL_TONS,VAL_KGS 
                       From V_RM_MATERIAL_CONSUMPTION 
                       Where Timestamp='29-NOV-2025' 
                       AND FUR_NAME=:FURNACE 
                       AND WEB_SL_NO IS NOT NULL 
                       ORDER BY WEB_SL_NO";

        using (OracleCommand cmd = new OracleCommand(sql, con))
        {
            cmd.Parameters.Add(":FURNACE", furnace);

            using (OracleDataReader dr = cmd.ExecuteReader())
            {
                while (dr.Read())
                {
                    list.Add(new
                    {
                        MATERIAL = dr["WEB_COLUMN"].ToString(),
                        TONS = dr["VAL_TONS"].ToString(),
                        KGS = dr["VAL_KGS"].ToString()
                    });
                }
            }
        }
    }

    return Json(list, JsonRequestBehavior.AllowGet);
}
