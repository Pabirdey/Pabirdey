[HttpGet]
public JsonResult GetNextExceptionCastId()
{
    string nextId = "";

    using (OracleConnection con = new OracleConnection(connectionString))
    {
        con.Open();
        string sql = "SELECT SEQ_EXCEPTION_CAST_ID.NEXTVAL FROM DUAL";
        using (OracleCommand cmd = new OracleCommand(sql, con))
        {
            nextId = cmd.ExecuteScalar().ToString();
        }
    }
    return Json(nextId, JsonRequestBehavior.AllowGet);
}