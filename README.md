[HttpGet]
public JsonResult CheckLotCount(string furName, string supplier)
{
    int cnt = 0;

    try
    {
        using (OracleConnection con =
               new OracleConnection(iMonitorWebUtils.msConRWString))
        {
            con.Open();

            string sql;

            // ✅ Correct C# condition
            if (furName == "A" || furName == "B" || furName == "C")
            {
                sql = @"
                    SELECT COUNT(lot_no)
                    FROM imtg.T_TAP_HOLE_CLAY
                    WHERE supplier = :SUPPLIER
                      AND fur_name = :FURNACE
                      AND bag_in_stock > 0";
            }
            else
            {
                sql = @"
                    SELECT COUNT(lot_no)
                    FROM imtg.T_TAP_HOLE_CLAY
                    WHERE supplier = :SUPPLIER
                      AND fur_name = :FURNACE
                      AND bag_in_stock > 0";
            }

            using (OracleCommand cmd = new OracleCommand(sql, con))
            {
                cmd.BindByName = true;

                cmd.Parameters.Add(":SUPPLIER", OracleDbType.Varchar2).Value = supplier;
                cmd.Parameters.Add(":FURNACE", OracleDbType.Varchar2).Value = furName;

                cnt = Convert.ToInt32(cmd.ExecuteScalar());
            }
        }
    }
    catch (Exception ex)
    {
        // optional: log ex
        return Json(-1, JsonRequestBehavior.AllowGet);
    }

    return Json(cnt, JsonRequestBehavior.AllowGet);
}