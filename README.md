function Display_Material(furnaceName,fDate) {
    $.ajax({
        url: '/HML/GetRawMaterialByFurnace',
        type: 'GET',
        data: { furnace: furnaceName, fdate: fDate },
        success: function (data) {
            var tbody = $("#materialTable tbody");
            tbody.empty();
            for (var i = 0; i < data.length; i++) {
                var row = "<tr>" +
                    "<td class='fw-bold'>" + data[i].MATERIAL + "</td>" +
                    "<td><input type='text' class='form-control medium-textbox shadow-sm' value='" + data[i].VALUE_TON + "'></td>" +
                    "<td><input type='text' class='form-control medium-textbox shadow-sm' value='" + data[i].VALUE_KG + "'></td>" +
                    "</tr>";
                tbody.append(row);
            }
        },
        error: function (xhr) {
            alert("Error: " + xhr.responseText);
        }
    });
}

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
