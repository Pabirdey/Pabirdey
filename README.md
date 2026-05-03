[03/05, 11:00 am] ♥️Wife😡🥰🤩: <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">

<div class="table-responsive">

    <table class="table table-bordered text-center" id="tblData">

        <thead class="table-primary">

            <tr>
                <th>Date</th>
                <th>Shift</th>
                <th>Bunker</th>
                <th>A</th>
                <th>B</th>
                <th>C</th>
                <th>D</th>
                <th>E</th>
                <th>F</th>
                <th>Total</th>
                <th>Bunker Position</th>
                <th>Balance</th>
            </tr>

        </thead>

        <tbody>
        </tbody>

    </table>

</div>

<script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>

<script>

    $(document).ready(function () {

        $.ajax({
            url: '/Home/GetData',
            type: 'GET',
            success: function (data) {

                var html = '';

                $.each(data, function (i, item) {

                    html += '<tr>';

                    html += '<td>' + item.TIMESTAMP + '</td>';
                    html += '<td>' + item.SHIFT + '</td>';

                    html += '<td>' +
                            '<select class="form-select">' +
                            '<option>' + item.BUNKER + '</option>' +
                            '</select>' +
                            '</td>';

                    html += '<td><input type="text" class="form-control" value="' + item.A + '"></td>';

                    html += '<td><input type="text" class="form-control" value="' + item.B + '"></td>';

                    html += '<td><input type="text" class="form-control" value="' + item.C + '"></td>';

                    html += '<td><input type="text" class="form-control" value="' + item.D + '"></td>';

                    html += '<td><input type="text" class="form-control" value="' + item.E + '"></td>';

                    html += '<td><input type="text" class="form-control" value="' + item.F + '"></td>';

                    html += '<td>' + item.TOTAL + '</td>';

                    html += '<td>' + item.BUNKER_P + '</td>';

                    html += '<td>' + item.BALANCE + '</td>';

                    html += '</tr>';

                });

                $('#tblData tbody').html(html);
            }
        });

    });

</script>
[03/05, 11:01 am] ♥️Wife😡🥰🤩: public JsonResult GetData()
{
    List<object> list = new List<object>();

    using (OracleConnection con = new OracleConnection(conString))
    {
        con.Open();

        OracleCommand cmd = new OracleCommand("SELECT * FROM COKE_UNLOADING", con);

        OracleDataReader dr = cmd.ExecuteReader();

        while (dr.Read())
        {
            list.Add(new
            {
                TIMESTAMP = dr["TIMESTAMP"].ToString(),
                SHIFT = dr["SHIFT"].ToString(),
                BUNKER = dr["BUNKER"].ToString(),
                A = dr["A"].ToString(),
                B = dr["B"].ToString(),
                C = dr["C"].ToString(),
                D = dr["D"].ToString(),
                E = dr["E"].ToString(),
                F = dr["F"].ToString(),
                TOTAL = dr["TOTAL"].ToString(),
                BUNKER_P = dr["BUNKER_P"].ToString(),
                BALANCE = dr["BALANCE"].ToString()
            });
        }
    }

    return Json(list, JsonRequestBehavior.AllowGet);
}