<!-- Furnace -->
<select id="ddlFurnace">
    <option value="">-- Select Furnace --</option>
    <option value="F">F</option>
    <option value="A">A</option>
</select>

<!-- Supplier -->
<input type="text" id="txtSupplier" placeholder="Supplier" value="BRL" />

<button type="button" id="btnShowLot">Show Lot</button>

<!-- MODAL -->
<div id="lotModal" style="display:none; position:fixed; top:20%; left:35%; 
     background:#fff; border:1px solid #333; padding:15px; width:300px;">

    <h4>Available Lot No</h4>

    <table border="1" width="100%">
        <thead>
            <tr>
                <th>LOT NO</th>
            </tr>
        </thead>
        <tbody id="lotBody"></tbody>
    </table>

    <br />
    <button onclick="closeModal()">Close</button>
</div>
<script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>

<script>
$("#btnShowLot").click(function () {

    var furnace = $("#ddlFurnace").val();
    var supplier = $("#txtSupplier").val();

    if (furnace === "" || supplier === "") {
        alert("Select Furnace & Supplier");
        return;
    }

    $.ajax({
        url: '/HML/GetLotList',
        type: 'GET',
        data: {
            furName: furnace,
            supplier: supplier
        },
        success: function (data) {

            $("#lotBody").empty();

            if (data.length === 0) {
                $("#lotBody").append("<tr><td>No Data</td></tr>");
            } else {
                $.each(data, function (i, lot) {
                    $("#lotBody").append(
                        "<tr><td>" + lot + "</td></tr>"
                    );
                });
            }

            $("#lotModal").show();
        },
        error: function () {
            alert("Error loading lot data");
        }
    });
});

function closeModal() {
    $("#lotModal").hide();
}
</script>

[HttpGet]
public JsonResult GetLotList(string furName, string supplier)
{
    List<string> lotList = new List<string>();

    try
    {
        using (OracleConnection con =
               new OracleConnection(iMonitorWebUtils.msConRWString))
        {
            con.Open();

            string sql = @"
                SELECT DISTINCT lot_no
                FROM t_tap_hole_clay
                WHERE fur_name = :FURNACE
                  AND supplier = :SUPPLIER
                  AND bag_in_stock > 0
                ORDER BY lot_no";

            using (OracleCommand cmd = new OracleCommand(sql, con))
            {
                cmd.BindByName = true;
                cmd.Parameters.Add(":FURNACE", OracleDbType.Varchar2).Value = furName;
                cmd.Parameters.Add(":SUPPLIER", OracleDbType.Varchar2).Value = supplier;

                using (OracleDataReader dr = cmd.ExecuteReader())
                {
                    while (dr.Read())
                    {
                        lotList.Add(dr["LOT_NO"].ToString());
                    }
                }
            }
        }
    }
    catch
    {
        return Json(new List<string>(), JsonRequestBehavior.AllowGet);
    }

    return Json(lotList, JsonRequestBehavior.AllowGet);
}