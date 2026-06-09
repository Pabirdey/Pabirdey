[10/06, 1:16 am] My Mother: public class GranshotDetail
{
    public int CastNo { get; set; }

    public string StartTime { get; set; }
    public string EndTime { get; set; }

    public int LadleNo { get; set; }

    public string LadleStartTime { get; set; }
    public string LadleEndTime { get; set; }

    public string ArrivedFrom { get; set; }

    public decimal GrossWeight { get; set; }
    public decimal TareWeight { get; set; }
    public decimal NetWeight { get; set; }

    public decimal PouringRate { get; set; }

    public int HMT { get; set; }

    public string ReasonForOutage { get; set; }
}
[10/06, 1:16 am] My Mother: public class GranshotViewModel
{
    public DateTime ProductionDate { get; set; }

    public string Shift { get; set; }

    public List<GranshotDetail> Details { get; set; }
}
[10/06, 1:17 am] My Mother: private DateTime GetActualDateTime(
    DateTime productionDate,
    string shift,
    string timeValue)
{
    TimeSpan time = DateTime.Parse(timeValue).TimeOfDay;

    DateTime actualDate =
        productionDate.Date.Add(time);

    if (shift == "C")
    {
        if (time.Hours >= 0 && time.Hours < 7)
        {
            actualDate = actualDate.AddDays(1);
        }
    }

    return actualDate;
}
[10/06, 1:17 am] My Mother: [HttpPost]
public ActionResult Save(GranshotViewModel model)
{
    string conStr =
        ConfigurationManager.ConnectionStrings["OracleDb"].ConnectionString;

    using (OracleConnection con = new OracleConnection(conStr))
    {
        con.Open();

        foreach (var item in model.Details)
        {
            DateTime castStart =
                GetActualDateTime(
                    model.ProductionDate,
                    model.Shift,
                    item.StartTime);

            DateTime castEnd =
                GetActualDateTime(
                    model.ProductionDate,
                    model.Shift,
                    item.EndTime);

            DateTime ladleStart =
                GetActualDateTime(
                    model.ProductionDate,
                    model.Shift,
                    item.LadleStartTime);

            DateTime ladleEnd =
                GetActualDateTime(
                    model.ProductionDate,
                    model.Shift,
                    item.LadleEndTime);

            string sql = @"
            INSERT INTO GRANSHOT_DETAILS
            (
                PROD_DATE,
                SHIFT_CODE,
                CAST_NO,
                CAST_START_TIME,
                CAST_END_TIME,
                LADLE_NO,
                LADLE_START_TIME,
                LADLE_END_TIME,
                ARRIVED_FROM,
                GROSS_WEIGHT,
                TARE_WEIGHT,
                NET_WEIGHT,
                POURING_RATE,
                HMT,
                OUTAGE_REASON
            )
            VALUES
            (
                :PROD_DATE,
                :SHIFT_CODE,
                :CAST_NO,
                :CAST_START_TIME,
                :CAST_END_TIME,
                :LADLE_NO,
                :LADLE_START_TIME,
                :LADLE_END_TIME,
                :ARRIVED_FROM,
                :GROSS_WEIGHT,
                :TARE_WEIGHT,
                :NET_WEIGHT,
                :POURING_RATE,
                :HMT,
                :OUTAGE_REASON
            )";

            using (OracleCommand cmd =
                new OracleCommand(sql, con))
            {
                cmd.Parameters.Add("PROD_DATE",
                    OracleDbType.Date).Value =
                    model.ProductionDate;

                cmd.Parameters.Add("SHIFT_CODE",
                    OracleDbType.Varchar2).Value =
                    model.Shift;

                cmd.Parameters.Add("CAST_NO",
                    OracleDbType.Int32).Value =
                    item.CastNo;

                cmd.Parameters.Add("CAST_START_TIME",
                    OracleDbType.TimeStamp).Value =
                    castStart;

                cmd.Parameters.Add("CAST_END_TIME",
                    OracleDbType.TimeStamp).Value =
                    castEnd;

                cmd.Parameters.Add("LADLE_NO",
                    OracleDbType.Int32).Value =
                    item.LadleNo;

                cmd.Parameters.Add("LADLE_START_TIME",
                    OracleDbType.TimeStamp).Value =
                    ladleStart;

                cmd.Parameters.Add("LADLE_END_TIME",
                    OracleDbType.TimeStamp).Value =
                    ladleEnd;

                cmd.Parameters.Add("ARRIVED_FROM",
                    OracleDbType.Varchar2).Value =
                    item.ArrivedFrom;

                cmd.Parameters.Add("GROSS_WEIGHT",
                    OracleDbType.Decimal).Value =
                    item.GrossWeight;

                cmd.Parameters.Add("TARE_WEIGHT",
                    OracleDbType.Decimal).Value =
                    item.TareWeight;

                cmd.Parameters.Add("NET_WEIGHT",
                    OracleDbType.Decimal).Value =
                    item.NetWeight;

                cmd.Parameters.Add("POURING_RATE",
                    OracleDbType.Decimal).Value =
                    item.PouringRate;

                cmd.Parameters.Add("HMT",
                    OracleDbType.Int32).Value =
                    item.HMT;

                cmd.Parameters.Add("OUTAGE_REASON",
                    OracleDbType.Varchar2).Value =
                    item.ReasonForOutage;

                cmd.ExecuteNonQuery();
            }
        }
    }

    return Json(new
    {
        success = true,
        message = "Data Saved Successfully"
    });
}
private DateTime GetActualDateTime(DateTime productionDate,
                                   string shift,
                                   string timeValue)
{
    DateTime actualDate = productionDate.Date.Add(
        DateTime.Parse(timeValue).TimeOfDay);

    if (shift == "C" && actualDate.Hour < 7)
    {
        actualDate = actualDate.AddDays(1);
    }

    return actualDate;
}
