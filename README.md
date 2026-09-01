using System;
using System.Collections.Generic;
using System.Web.Mvc;
using Oracle.ManagedDataAccess.Client;

public class TLCController : Controller
{
    [HttpGet]
    public ActionResult Index()
    {
        return View();
    }


    [HttpGet]
    public JsonResult GetTLCMaster()
    {
        List<TlcMasterModel> list = new List<TlcMasterModel>();

        try
        {
            using (OracleConnection con =
                new OracleConnection(iMonitorWebUtils.msConRWString))
            {
                con.Open();

                string query = @"
                    SELECT TLC_NO,
                           MATURITY_LIFE,
                           TLC_SIZE
                    FROM T_TLC_MASTER
                    ORDER BY TLC_NO";

                using (OracleCommand cmd =
                    new OracleCommand(query, con))
                {
                    using (OracleDataReader dr =
                        cmd.ExecuteReader())
                    {
                        while (dr.Read())
                        {
                            TlcMasterModel model =
                                new TlcMasterModel();

                            model.TLC_NO =
                                dr["TLC_NO"] == DBNull.Value
                                ? 0
                                : Convert.ToInt32(dr["TLC_NO"]);

                            model.MATURITY_LIFE =
                                dr["MATURITY_LIFE"] == DBNull.Value
                                ? 0
                                : Convert.ToInt32(dr["MATURITY_LIFE"]);

                            model.TLC_SIZE =
                                dr["TLC_SIZE"] == DBNull.Value
                                ? ""
                                : dr["TLC_SIZE"].ToString();

                            list.Add(model);
                        }
                    }
                }
            }

            return Json(new
            {
                success = true,
                data = list
            }, JsonRequestBehavior.AllowGet);
        }
        catch (Exception ex)
        {
            return Json(new
            {
                success = false,
                message = ex.Message
            }, JsonRequestBehavior.AllowGet);
        }
    }
}