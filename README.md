using System;
using System.Collections.Generic;
using System.Data;
using System.Web.Mvc;
using Oracle.ManagedDataAccess.Client;

public class HomeController : Controller
{
    public JsonResult GetFinesData()
    {
        try
        {
            List<object> data = new List<object>();

            using (OracleConnection con = new OracleConnection("YOUR_CONNECTION_STRING"))
            {
                con.Open();

                string query = @"
                    SELECT 
                        ELEMENT,
                        RETURN_FINES,
                        WET_FINES,
                        DRY_FINES,
                        DRY_FINES_500TPH
                    FROM YOUR_TABLE_NAME
                    ORDER BY ELEMENT";

                using (OracleCommand cmd = new OracleCommand(query, con))
                {
                    cmd.CommandType = CommandType.Text;

                    using (OracleDataReader dr = cmd.ExecuteReader())
                    {
                        while (dr.Read())
                        {
                            data.Add(new
                            {
                                ELEMENT = dr["ELEMENT"] == DBNull.Value ? null : dr["ELEMENT"].ToString(),
                                RETURN_FINES = dr["RETURN_FINES"] == DBNull.Value ? null : Convert.ToDecimal(dr["RETURN_FINES"]),
                                WET_FINES = dr["WET_FINES"] == DBNull.Value ? null : Convert.ToDecimal(dr["WET_FINES"]),
                                DRY_FINES = dr["DRY_FINES"] == DBNull.Value ? null : Convert.ToDecimal(dr["DRY_FINES"]),
                                DRY_FINES_500TPH = dr["DRY_FINES_500TPH"] == DBNull.Value ? null : Convert.ToDecimal(dr["DRY_FINES_500TPH"])
                            });
                        }
                    }
                }
            }

            return Json(data, JsonRequestBehavior.AllowGet);
        }
        catch (Exception ex)
        {
            // Return error to UI
            return Json(new { error = ex.Message }, JsonRequestBehavior.AllowGet);
        }
    }
}
