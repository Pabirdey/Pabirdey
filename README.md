[HttpGet]
public JsonResult GetNextCastNo()
{
    string castNo = "";

    using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
    {
        con.Open();

        string sql = @"SELECT NVL(MAX(CAST_NO),0) + 1 AS NEXT_CAST_NO
                       FROM T_GRANSHOT_DETAILS";

        OracleCommand cmd = new OracleCommand(sql, con);

        castNo = cmd.ExecuteScalar().ToString();
    }

    return Json(castNo, JsonRequestBehavior.AllowGet);
}

function GenerateRow() {

    $.ajax({
        url: '/Granshot/GetNextCastNo',
        type: 'GET',
        success: function (castNo) {

            var row = `
            <tr>
                <td class="castno">${castNo}</td>
                <td><input type="time" class="form-control" /></td>
                <td><input type="time" class="form-control" /></td>
                <td><input type="text" class="form-control" /></td>
                <td><button type="button" class="btn btn-danger">Delete</button></td>
            </tr>`;

            $("#tblBody").append(row);
        }
    });
}