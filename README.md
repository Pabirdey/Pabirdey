function bindTonnage(selector, data) {

    var tbody = document.querySelector(selector);
    tbody.innerHTML = "";

    // ✅ Check data length
    if (!data || data.length === 0) {
        tbody.innerHTML = "<tr><td colspan='5'>No Data Found</td></tr>";
        return;
    }

    console.log("Total Records:", data.length);

    for (var i = 0; i < data.length; i++) {

        var item = data[i];

        var c = parseFloat(item.C) || 0;
        var e = parseFloat(item.E) || 0;
        var f = parseFloat(item.F) || 0;

        var total = c + e + f;

        var row = "<tr>" +
            "<td><b>" + item.BUNKER + "</b></td>" +
            "<td><input type='number' class='form-control' value='" + c + "'></td>" +
            "<td><input type='number' class='form-control' value='" + e + "'></td>" +
            "<td><input type='number' class='form-control' value='" + f + "'></td>" +
            "<td><input type='number' class='form-control' value='" + total + "' readonly></td>" +
            "</tr>";

        tbody.innerHTML += row;
    }

    // ✅ Row count after binding
    console.log("Rendered Rows:", tbody.rows.length);
}
function LoadTonnageFromDB() {

    let date = $("#hiddenDate").val();
    let shift = $("#ddlshift").val();

    $.ajax({
        url: '/YourController/GetTonnageData',
        type: 'GET',
        data: { date: date, shift: shift },
        success: function (res) {

            bindTonnage("#cokeTable tbody", res.coke);
            bindTonnage("#nutTable tbody", res.nut);
        }
    });
}
public JsonResult GetTonnageData(string date, string shift)
{
    List<object> cokeList = new List<object>();
    List<object> nutList = new List<object>();

    using (OracleConnection con = new OracleConnection("YOUR_CONNECTION"))
    {
        con.Open();

        string query = @"SELECT BUNKER, TYPE, C_BF, E_BF, F_BF 
                         FROM T_COKE_TONNAGE
                         WHERE TRUNC(TDATE)=TO_DATE(:date,'DD/MM/YYYY')
                         AND SHIFT=:shift";

        using (OracleCommand cmd = new OracleCommand(query, con))
        {
            cmd.Parameters.Add("date", date);
            cmd.Parameters.Add("shift", shift);

            OracleDataReader dr = cmd.ExecuteReader();

            while (dr.Read())
            {
                var obj = new
                {
                    BUNKER = dr["BUNKER"].ToString(),
                    C = dr["C_BF"].ToString(),
                    E = dr["E_BF"].ToString(),
                    F = dr["F_BF"].ToString()
                };

                if (dr["TYPE"].ToString() == "COKE")
                    cokeList.Add(obj);
                else
                    nutList.Add(obj);
            }
        }
    }

    return Json(new { coke = cokeList, nut = nutList }, JsonRequestBehavior.AllowGet);
}