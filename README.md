using System;
using System.Collections.Generic;
using System.Data;
using System.Web.Mvc;
using Oracle.ManagedDataAccess.Client;

public class HomeController : Controller
{
    public JsonResult GetData()
    {
        List<object> list = new List<object>();

        string conStr = "YOUR_ORACLE_CONNECTION_STRING";

        using (OracleConnection con = new OracleConnection(conStr))
        {
            con.Open();

            string query = @"SELECT 
                                TIMESTAMP,
                                SHIFT,
                                BUNKER,
                                C,
                                E,
                                F,
                                TOTAL,
                                BUNKER_P,
                                BALANCE
                             FROM YOUR_TABLE_NAME
                             ORDER BY TIMESTAMP";

            using (OracleCommand cmd = new OracleCommand(query, con))
            {
                using (OracleDataReader dr = cmd.ExecuteReader())
                {
                    while (dr.Read())
                    {
                        list.Add(new
                        {
                            TIMESTAMP = dr["TIMESTAMP"] == DBNull.Value ? null : Convert.ToDateTime(dr["TIMESTAMP"]),
                            SHIFT = dr["SHIFT"]?.ToString(),
                            BUNKER = dr["BUNKER"]?.ToString(),
                            C = dr["C"]?.ToString(),
                            E = dr["E"]?.ToString(),
                            F = dr["F"]?.ToString(),
                            TOTAL = dr["TOTAL"]?.ToString(),
                            BUNKER_P = dr["BUNKER_P"]?.ToString(),
                            BALANCE = dr["BALANCE"]?.ToString()
                        });
                    }
                }
            }
        }

        return Json(list, JsonRequestBehavior.AllowGet);
    }
}
