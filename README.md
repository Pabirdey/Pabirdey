[HttpPost]
public JsonResult Get_Fugitive_Violin_Chart(string pTimestamp, string pOvenNo, string pBatteryNo, string pPlantName)
{
    string sql = string.Empty;
    DataTable dt = new DataTable();
    Dictionary<string, object> param = new Dictionary<string, object>();

    if (pPlantName == "B10")
    {
        if (pBatteryNo == "10")
        {
            sql = "SELECT O.ID_OVEN AS OVEN_NO, TRUNC(O.ST_TIME) AS DATETIME, ROUND(O.DURATION,2) AS PUSH_FORCE " +
                  "FROM imtg.t_cp_fugitive_emission O " +
                  "WHERE TRUNC(O.ST_TIME) > (TO_DATE(:pTimestamp, 'dd/mm/yyyy') - 30) " +
                  "AND TRUNC(O.ST_TIME) <= TO_DATE(:pTimestamp, 'dd/mm/yyyy') " +
                  "AND O.ID_BATTERY = :pBatteryNo AND ID_OVEN = :pOvenNo ORDER BY O.ST_TIME";
        }
        else if (pBatteryNo == "11")
        {
            sql = "SELECT O.ID_OVEN AS OVEN_NO, TRUNC(O.ST_TIME) AS DATETIME, ROUND(O.DURATION,2) AS PUSH_FORCE " +
                  "FROM imtg.t_cp_fugitive_emission O " +
                  "WHERE TRUNC(O.ST_TIME) > (TO_DATE(:pTimestamp, 'dd/mm/yyyy') - 30) " +
                  "AND TRUNC(O.ST_TIME) <= TO_DATE(:pTimestamp, 'dd/mm/yyyy') " +
                  "AND O.ID_BATTERY = :pBatteryNo AND ID_OVEN = :pOvenNo ORDER BY O.ST_TIME";
        }
    }

    param.Add("pTimestamp", pTimestamp);
    param.Add("pOvenNo", pOvenNo);
    param.Add("pBatteryNo", pBatteryNo);

    dt = DAL.GetRecords(sql, param);

    return Json(dt, JsonRequestBehavior.AllowGet);
}



function Get_Fugitive_Violin_Chart(pOvenNo, pDate) {
    debugger;
    var modal = $('#FugitiveModal');
    modal.find('.modal-title').text("Oven No " + pOvenNo);
    Plotly.purge('modalPushCurrentChart1');

    var pBatteryNo = $('#battery_no').val();

    $.post('@Url.Action("Get_Fugitive_Violin_Chart")', {
        'pTimestamp': pDate,
        'pOvenNo': pOvenNo,
        'pBatteryNo': pBatteryNo,
        'pPlantName': Area
    }, function (jData) {
        var values = jData.map(item => item.PUSH_FORCE);
        var labels = jData.map(item => item.DATETIME);

        var dataPlot = [{
            type: 'violin',
            y: values,
            x: labels,
            box: { visible: true },
            line: { color: 'blue' },
            meanline: { visible: true }
        }];

        var layout = {
            title: "Fugitive Violin Chart",
            yaxis: { zeroline: false, title: "Push Force" },
            xaxis: { title: "Date" }
        };

        Plotly.newPlot('modalPushCurrentChart1', dataPlot, layout);
    });
}