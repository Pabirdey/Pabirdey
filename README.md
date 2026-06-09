public class LadleModel
{
    public string LADLE_FLST_TIME { get; set; }   // "14:30"
    public string LADLE_FLEND_TIME { get; set; }  // "15:45"
    public string TXTDT { get; set; }             // "2026-06-08"
    public string TXTSHIFT { get; set; }

    public string TRP_NO { get; set; }
    public string ARRIVED_FROM { get; set; }

    public decimal GROSS_WT { get; set; }
    public decimal TARE_WT { get; set; }
    public decimal NET_WT { get; set; }
    public decimal HMT { get; set; }

    public decimal TXT_LADLEFILLINGRATE { get; set; }
}


[HttpPost]
public ActionResult CalculateLadle(LadleModel model)
{
    try
    {
        decimal v_Pouring_rate = 0;
        int v_lfe_time;
        DateTime v_timestamp;

        // ✅ Convert DATE
        DateTime baseDate = DateTime.Parse(model.TXTDT);

        // ✅ Convert TIME (SAFE for AM/PM or 24-hour)
        DateTime startTime = DateTime.Parse(model.LADLE_FLST_TIME);
        DateTime endTime = DateTime.Parse(model.LADLE_FLEND_TIME);

        v_lfe_time = endTime.Hour;

        // ==============================
        // SHIFT LOGIC (Oracle Converted)
        // ==============================
        if (v_lfe_time >= 6 && v_lfe_time < 14)
        {
            if (model.TXTSHIFT == "C")
                v_timestamp = baseDate.AddDays(1);
            else
                v_timestamp = baseDate;
        }
        else if (v_lfe_time >= 14 && v_lfe_time < 22)
        {
            v_timestamp = baseDate;
        }
        else if (v_lfe_time >= 22)
        {
            v_timestamp = baseDate;
        }
        else
        {
            v_timestamp = baseDate.AddDays(1);
        }

        // ==============================
        // CALL YOUR DB FUNCTIONS
        // ==============================
        model.GROSS_WT = GetGrossWt(model.TRP_NO, v_timestamp, endTime, model.ARRIVED_FROM);
        model.TARE_WT = GetTareWt(model.TRP_NO, v_timestamp, endTime, model.ARRIVED_FROM);
        model.NET_WT = GetNetWt(model.TRP_NO, v_timestamp, endTime, model.ARRIVED_FROM);
        model.HMT = GetHmt(model.TRP_NO, v_timestamp, endTime, model.ARRIVED_FROM);

        // ==============================
        // FILLING RATE
        // ==============================
        var minutes = (endTime - startTime).TotalMinutes;

        if (minutes > 0)
            model.TXT_LADLEFILLINGRATE = model.NET_WT / (decimal)minutes;
        else
            model.TXT_LADLEFILLINGRATE = 0;

        v_Pouring_rate = model.TXT_LADLEFILLINGRATE;

        return Json(new
        {
            success = true,
            data = model
        });
    }
    catch (Exception ex)
    {
        return Json(new
        {
            success = false,
            message = ex.Message
        });
    }
}

private decimal GetGrossWt(string trpNo, DateTime date, DateTime time, string from)
{
    return 0; // Replace Oracle call
}

private decimal GetTareWt(string trpNo, DateTime date, DateTime time, string from)
{
    return 0;
}

private decimal GetNetWt(string trpNo, DateTime date, DateTime time, string from)
{
    return 0;
}

private decimal GetHmt(string trpNo, DateTime date, DateTime time, string from)
{
    return 0;
}
<td>
                    <select class ="table-input arrivedFrom">
                        <option value=""></option>
                        <option value="C" ${item.ARRIVED_FROM === 'C' ? 'selected': ''}>C</option>
                        <option value="E" ${item.ARRIVED_FROM === 'E' ? 'selected': ''}>E</option>
                        <option value="F" ${item.ARRIVED_FROM === 'F' ? 'selected': ''}>F</option>
                        <option value="C" ${item.ARRIVED_FROM === 'G' ? 'selected': ''}>G</option>
                        <option value="E" ${item.ARRIVED_FROM === 'H' ? 'selected': ''}>H</option>
                        <option value="F" ${item.ARRIVED_FROM === 'I' ? 'selected': ''}>I</option>
                    </select>
               </td>
