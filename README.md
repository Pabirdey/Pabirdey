using Oracle.ManagedDataAccess.Client;
using System.Configuration;
using System.Data;
using System.Collections.Generic;
using System.Web.Mvc;

public JsonResult GetFinesTrend(string type, string value)
{
    List<object> list = new List<object>();

    string connStr = ConfigurationManager.ConnectionStrings["OracleConn"].ConnectionString;

    using (OracleConnection con = new OracleConnection(connStr))
    {
        con.Open();

        string query = @"
            SELECT TREND_DATE, VALUE
            FROM T_FINES_TREND
            WHERE ELEMENT_TYPE = :p_type
              AND VALUE_NAME = :p_value
              AND TREND_DATE >= SYSDATE - 30
            ORDER BY TREND_DATE";

        using (OracleCommand cmd = new OracleCommand(query, con))
        {
            cmd.Parameters.Add(":p_type", type);
            cmd.Parameters.Add(":p_value", value);

            using (OracleDataReader dr = cmd.ExecuteReader())
            {
                while (dr.Read())
                {
                    list.Add(new
                    {
                        DATE = Convert.ToDateTime(dr["TREND_DATE"]).ToString("yyyy-MM-dd"),
                        VALUE = Convert.ToDecimal(dr["VALUE"])
                    });
                }
            }
        }
    }

    return Json(list, JsonRequestBehavior.AllowGet);
}
