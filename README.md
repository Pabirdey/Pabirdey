<!DOCTYPE html>
<html>
<head>
    <title>Pile Quality</title>

    <link href="~/css/bootstrap.min.css" rel="stylesheet" />

    <style>
        body { padding:20px; background:white; }

        .card {
            margin:auto;
            width:750px;
            padding:20px;
            box-shadow:0 4px 10px rgba(0,0,0,0.1);
        }

        .chart-cell {
            cursor:pointer;
            color:#0d6efd;
        }

        .chart-cell:hover {
            background:#f2f2f2;
        }
    </style>
</head>

<body>

<div class="card">
    <h3 class="text-center">Pile Mat Wise Quality</h3>

    <table class="table table-bordered text-center" id="finesTable">
        <thead>
            <tr>
                <th>Element</th>
                <th>Return</th>
                <th>Wet</th>
                <th>Dry</th>
                <th>500TPH</th>
            </tr>
        </thead>
        <tbody></tbody>
    </table>
</div>

<!-- MODAL -->
<div class="modal fade" id="trendModal">
    <div class="modal-dialog modal-lg">
        <div class="modal-content">
            <div class="modal-header">
                <h5 class="modal-title">Trend</h5>
                <button class="btn-close" data-bs-dismiss="modal"></button>
            </div>
            <div class="modal-body">
                <div id="chart" style="height:400px;"></div>
            </div>
        </div>
    </div>
</div>

<script src="~/js/Jquey3.6.0.min.js"></script>
<script src="~/js/bootstrap.bundle.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/echarts/dist/echarts.min.js"></script>

<script>

let chart = null;

$(document).ready(function () {
    loadData();
});

// 🔹 LOAD TABLE
function loadData() {
    $.get('/RmbbPile/GetFinesData', function (res) {
        let html = '';

        res.forEach(item => {
            html += `
            <tr>
                <td>${item.ELEMENT}</td>

                <td class="chart-cell" data-type="RETURN_FINES" data-element="${item.ELEMENT}">
                    ${item.RETURN_FINES}
                </td>

                <td class="chart-cell" data-type="WET_FINES" data-element="${item.ELEMENT}">
                    ${item.WET_FINES}
                </td>

                <td class="chart-cell" data-type="DRY_FINES" data-element="${item.ELEMENT}">
                    ${item.DRY_FINES}
                </td>

                <td class="chart-cell" data-type="DRY_FINES_500TPH" data-element="${item.ELEMENT}">
                    ${item.DRY_FINES_500TPH}
                </td>
            </tr>`;
        });

        $("#finesTable tbody").html(html);
    });
}

// 🔹 CLICK EVENT
$(document).on("click", ".chart-cell", function () {

    let type = $(this).data("type");
    let element = $(this).data("element");

    loadTrend(type, element);
});

// 🔹 LOAD TREND
function loadTrend(type, element) {

    $.get('/RmbbPile/GetFinesTrend', { type: type, element: element }, function (res) {

        let modal = new bootstrap.Modal(document.getElementById('trendModal'));
        modal.show();

        $(".modal-title").text(element + " - " + type + " (30 Days)");

        setTimeout(() => drawChart(res), 300);
    });
}

// 🔹 DRAW CHART
function drawChart(data) {

    if (chart) chart.dispose();

    chart = echarts.init(document.getElementById("chart"));

    chart.setOption({
        tooltip: { trigger: 'axis' },

        xAxis: {
            type: 'category',
            data: data.map(x => x.DATE)
        },

        yAxis: { type: 'value' },

        series: [{
            type: 'line',
            smooth: true,
            data: data.map(x => x.VALUE)
        }]
    });
}

</script>

</body>
</html>

public JsonResult GetFinesTrend(string type, string element)
{
    List<object> list = new List<object>();

    using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
    {
        con.Open();

        string column = "";

        switch (type.ToUpper())
        {
            case "RETURN_FINES":
                column = $"RETURN_FINES_{element}";
                break;

            case "WET_FINES":
                column = $"WET_FINES_{element}";
                break;

            case "DRY_FINES":
                column = $"DRY_FINES_{element}";
                break;

            case "DRY_FINES_500TPH":
                column = $"DRY_FINES_500TPH_{element}";
                break;

            default:
                column = $"RETURN_FINES_{element}";
                break;
        }

        string query = $@"
        SELECT TRUNC(TIMESTAMP) AS TREND_DATE, {column} AS VALUE
        FROM imtg.T_NOA_PILE_MAT_ANAL_SHIFT
        WHERE TIMESTAMP >= SYSDATE - 30
        ORDER BY TIMESTAMP";

        using (OracleCommand cmd = new OracleCommand(query, con))
        using (OracleDataReader dr = cmd.ExecuteReader())
        {
            while (dr.Read())
            {
                list.Add(new
                {
                    DATE = Convert.ToDateTime(dr["TREND_DATE"]).ToString("dd-MM-yyyy"),
                    VALUE = dr["VALUE"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["VALUE"])
                });
            }
        }
    }

    return Json(list, JsonRequestBehavior.AllowGet);
}


public JsonResult GetFinesData()
{
    try
    {
        List<object> data = new List<object>();

        using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
        {
            con.Open();

            string query = @"
            SELECT 'AL2O3' ELEMENT, ROUND(RETURN_FINES_AL2O3,2) RETURN_FINES,
                   ROUND(WET_FINES_AL2O3,2) WET_FINES,
                   ROUND(DRY_FINES_AL2O3,2) DRY_FINES,
                   ROUND(DRY_FINES_500TPH_AL2O3,2) DRY_FINES_500TPH
            FROM imtg.T_NOA_PILE_MAT_ANAL_SHIFT
            WHERE ROWNUM = 1

            UNION ALL

            SELECT 'SIO2', ROUND(RETURN_FINES_SIO2,2),
                   ROUND(WET_FINES_SIO2,2),
                   ROUND(DRY_FINES_SIO2,2),
                   ROUND(DRY_FINES_500TPH_SIO2,2)
            FROM imtg.T_NOA_PILE_MAT_ANAL_SHIFT
            WHERE ROWNUM = 1

            UNION ALL

            SELECT 'P', ROUND(RETURN_FINES_P,3),
                   ROUND(WET_FINES_P,3),
                   ROUND(DRY_FINES_P,3),
                   ROUND(DRY_FINES_500TPH_P,3)
            FROM imtg.T_NOA_PILE_MAT_ANAL_SHIFT
            WHERE ROWNUM = 1

            UNION ALL

            SELECT 'K2O', ROUND(RETURN_FINES_K2O,3),
                   ROUND(WET_FINES_K2O,3),
                   ROUND(DRY_FINES_K2O,3),
                   ROUND(DRY_FINES_500TPH_K2O,3)
            FROM imtg.T_NOA_PILE_MAT_ANAL_SHIFT
            WHERE ROWNUM = 1";

            using (OracleCommand cmd = new OracleCommand(query, con))
            using (OracleDataReader dr = cmd.ExecuteReader())
            {
                while (dr.Read())
                {
                    data.Add(new
                    {
                        ELEMENT = dr["ELEMENT"].ToString(),
                        RETURN_FINES = dr["RETURN_FINES"],
                        WET_FINES = dr["WET_FINES"],
                        DRY_FINES = dr["DRY_FINES"],
                        DRY_FINES_500TPH = dr["DRY_FINES_500TPH"]
                    });
                }
            }
        }

        return Json(data, JsonRequestBehavior.AllowGet);
    }
    catch (Exception ex)
    {
        return Json(new { error = ex.Message }, JsonRequestBehavior.AllowGet);
    }
}

