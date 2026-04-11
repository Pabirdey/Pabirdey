using System;
using System.Collections.Generic;
using System.Configuration;
using System.Web.Mvc;
using Oracle.ManagedDataAccess.Client;

public class HomeController : Controller
{
    public JsonResult GetFurnaceTD(string fDate)
    {
        var result = new List<object>();

        string conStr = ConfigurationManager.ConnectionStrings["OracleDB"].ConnectionString;

        using (OracleConnection con = new OracleConnection(conStr))
        {
            con.Open();

            string query = @"
            SELECT 
                a.FURNACE,
                NVL(a.ACTUAL,0) AS ACT_ONDT,
                NVL(a.REPORTED,0) AS REPORT_ONDT,
                NVL(a.BALANCE,0) AS BALANCE,

                (SELECT NVL(SUM(b.ACTUAL),0)
                 FROM DEMO.T_BF_PRODUCTION_TRACKING b
                 WHERE b.FURNACE = a.FURNACE
                 AND b.TIMESTAMP >= TRUNC(a.TIMESTAMP, 'MON')
                 AND b.TIMESTAMP < a.TIMESTAMP) AS ACT_TODT_PREV,

                (SELECT NVL(SUM(b.REPORTED),0)
                 FROM DEMO.T_BF_PRODUCTION_TRACKING b
                 WHERE b.FURNACE = a.FURNACE
                 AND b.TIMESTAMP >= TRUNC(a.TIMESTAMP, 'MON')
                 AND b.TIMESTAMP < a.TIMESTAMP) AS REPORT_TODT_PREV

            FROM DEMO.T_BF_PRODUCTION_TRACKING a
            WHERE a.TIMESTAMP = TO_DATE(:FDate,'DD/MM/YYYY')
            AND a.FURNACE IN ('C','E','F')
            ORDER BY a.FURNACE";

            using (OracleCommand cmd = new OracleCommand(query, con))
            {
                cmd.Parameters.Add("FDate", OracleDbType.Varchar2).Value = fDate;

                using (OracleDataReader dr = cmd.ExecuteReader())
                {
                    while (dr.Read())
                    {
                        // 🔥 INLINE NULL HANDLING (NO FUNCTION)

                        decimal actOnDt = dr["ACT_ONDT"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["ACT_ONDT"]);
                        decimal repOnDt = dr["REPORT_ONDT"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["REPORT_ONDT"]);
                        decimal balance = dr["BALANCE"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["BALANCE"]);

                        decimal actPrev = dr["ACT_TODT_PREV"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["ACT_TODT_PREV"]);
                        decimal repPrev = dr["REPORT_TODT_PREV"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["REPORT_TODT_PREV"]);

                        // 🔥 PL/SQL LOGIC (SAFE NOW)
                        decimal ACTUAL_TD = actPrev + actOnDt;
                        decimal REPORTED_TD = repPrev + repOnDt;

                        result.Add(new
                        {
                            FURNACE = dr["FURNACE"].ToString(),
                            ACT_ONDT = actOnDt,
                            REPORT_ONDT = repOnDt,
                            ACTUAL_TD = ACTUAL_TD,
                            REPORTED_TD = REPORTED_TD,
                            BALANCE = balance
                        });
                    }
                }
            }
        }

        return Json(result, JsonRequestBehavior.AllowGet);
    }
}
