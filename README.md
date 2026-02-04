<script>
document.addEventListener("click", function (e) {

    if (e.target.classList.contains("btnCheck")) {

        /* =========================
           1️⃣ CURRENT ROW
        ========================= */
        var row = e.target.closest("tr");

        /* =========================
           2️⃣ SUPPLIER VALUE FROM CELL
        ========================= */
        var supplier = row.querySelector(".supplier").innerText.trim();

        /* =========================
           3️⃣ FURNACE FROM DROPDOWN
        ========================= */
        var furName = document.getElementById("ddlFurnace").value;

        if (!furName) {
            alert("Please select Furnace");
            return;
        }

        /* =========================
           4️⃣ AJAX CALL
        ========================= */
        $.ajax({
            url: '/CastHouse/CheckLotCount',
            type: 'GET',
            data: {
                furName: furName,
                supplier: supplier
            },
            success: function (cnt) {

                if (cnt > 0) {

                    if (furName === 'A' || furName === 'B' || furName === 'C') {
                        openLovABC();
                    } else {
                        openLov();
                    }

                } else {
                    alert("No Lot No. Exists Against The Selected Supplier !!");
                }
            },
            error: function () {
                alert("Error while checking Lot Count");
            }
        });
    }
});
</script>

using System;
using System.Data;
using System.Web.Mvc;
using Oracle.ManagedDataAccess.Client;

public class CastHouseController : Controller
{
    [HttpGet]
    public JsonResult CheckLotCount(string furName, string supplier)
    {
        int count = 0;

        try
        {
            using (OracleConnection con =
                   new OracleConnection(iMonitorWebUtils.msConRWString))
            {
                con.Open();

                string sql = @"
                    SELECT COUNT(1)
                    FROM T_LOT_MASTER
                    WHERE FURNACE = :FURNACE
                      AND SUPPLIER = :SUPPLIER";

                using (OracleCommand cmd = new OracleCommand(sql, con))
                {
                    cmd.BindByName = true;

                    cmd.Parameters.Add(":FURNACE", OracleDbType.Varchar2).Value = furName;
                    cmd.Parameters.Add(":SUPPLIER", OracleDbType.Varchar2).Value = supplier;

                    count = Convert.ToInt32(cmd.ExecuteScalar());
                }
            }
        }
        catch (Exception ex)
        {
            // Optional: log error
            return Json(-1, JsonRequestBehavior.AllowGet);
        }

        return Json(count, JsonRequestBehavior.AllowGet);
    }
}