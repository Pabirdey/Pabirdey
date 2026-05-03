   <script>
        function createRow() {
            return `
    <tr>
        <td><input type="text" class="form-control row-date" style="width:100px;" readonly></td>

        <td>
            <select class="form-control row-shift" style="height:30px;width:50px;">
                <option>A</option>
                <option>B</option>
                <option>C</option>
            </select>
        </td>        
        <td>
            <select class ="form-control bunker text-start ps-01" style="height:30px;width:200px;">
                <option value="">---Pls. Select---</option>
                <option value="WESTERN">WESTERN</option>
                <option value="MIDDLE">MIDDLE</option>
                <option value="EASTERN">EASTERN</option>
                <option value="H/S NC">H/S NC</option>
                <option value="NC BF KO">NC BF KO</option>
                <option value="ST.COKE-HALDIA">ST.COKE-HALDIA</option>
                <option value="ST.COKE-IMPORTED">ST.COKE-IMPORTED</option>
                <option value="ST.COKE-OWN">ST.COKE-OWN</option>
                <option value="ST.COKE-TOTAL">ST.COKE-TOTAL</option>
                <option value="B/H HIGH ASH">B/H HIGH ASH</option>
                <option value="B/H LOW ASH">B/H LOW ASH</option>
                <option value="B/H COKE-TOTAL">B/H COKE-TOTAL</option>
                <option value="ROUGH BREEZE">ROUGH BREEZE</option>
                <option value="PLS_25MM_NC">PLS_25MM_NC</option>
            </select>
        </td>

        <td><input type="text" class="form-control val" data-field="C"></td>
        <td><input type="text" class ="form-control val" data-field="E"></td>
        <td><input type="text" class ="form-control val" data-field="F"></td>
        <td><input type="text" class ="form-control total" readonly></td>
        <td><input type="text" class ="form-control position"></td>
        <td><input type="text" class ="form-control balance"></td>
    </tr>`;
        }

        // generate rows
        for (let i = 0; i < 8; i++) {
            document.getElementById("tblBody").innerHTML += createRow();
        }

    </script>
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
