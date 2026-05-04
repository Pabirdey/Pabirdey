  public JsonResult GetFinesData()
        {
            try
            {
                List<object> data = new List<object>();
                using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
                {
                    con.Open();

                    string query = @"
                   SELECT 'AL2O3' AS ELEMENT,ROUND(RETURN_FINES_AL2O3,2) AS RETURN_FINES,Round(WET_FINES_AL2O3,2) AS WET_FINES,ROUND(DRY_FINES_AL2O3,2) AS DRY_FINES,
                   Round(DRY_FINES_500TPH_AL2O3,2) AS DRY_FINES_500TPH
                    FROM (SELECT * FROM imtg.T_NOA_PILE_MAT_ANAL_SHIFT WHERE SHIFT = (SELECT MAX(SHIFT) FROM imtg.T_NOA_PILE_MAT_ANAL_SHIFT) ORDER BY TIMESTAMP DESC)
                   WHERE ROWNUM = 1
                    UNION ALL
                    SELECT 'SIO2',ROUND(RETURN_FINES_SIO2,2) AS RETURN_FINES,Round(WET_FINES_SIO2,2)AS WET_FINES,ROUND(DRY_FINES_SIO2,2) AS DRY_FINES ,ROUND(DRY_FINES_500TPH_SIO2,2) AS DRY_FINES_500TPH
                    FROM (SELECT *  FROM imtg.T_NOA_PILE_MAT_ANAL_SHIFT  WHERE SHIFT = (SELECT MAX(SHIFT) FROM imtg.T_NOA_PILE_MAT_ANAL_SHIFT) ORDER BY TIMESTAMP DESC)
                    WHERE ROWNUM = 1
                    UNION ALL
                    SELECT 'P',ROUND(RETURN_FINES_P,3) AS RETURN_FINES,ROUND(WET_FINES_P,3) AS WET_FINES,ROUND(DRY_FINES_P,3) AS DRY_FINES,ROUND(DRY_FINES_500TPH_P,3) AS DRY_FINES_500TPH
                    FROM (
                        SELECT *
                        FROM imtg.T_NOA_PILE_MAT_ANAL_SHIFT
                        WHERE SHIFT = (SELECT MAX(SHIFT) FROM imtg.T_NOA_PILE_MAT_ANAL_SHIFT)
                        ORDER BY TIMESTAMP DESC
                        )
                    WHERE ROWNUM = 1
                UNION ALL
            SELECT 'K2O',ROUND(RETURN_FINES_K2O,3) AS RETURN_FINES,ROUND(WET_FINES_K2O,3) AS WET_FINES,ROUND(DRY_FINES_K2O,3) AS DRY_FINES,ROUND(DRY_FINES_500TPH_K20,3) AS DRY_FINES_500TPH
        FROM (
            SELECT *
            FROM imtg.T_NOA_PILE_MAT_ANAL_SHIFT
            WHERE SHIFT = (SELECT MAX(SHIFT) FROM imtg.T_NOA_PILE_MAT_ANAL_SHIFT)
            ORDER BY TIMESTAMP DESC
            )
WHERE ROWNUM = 1";
                    using (OracleCommand cmd = new OracleCommand(query, con))
                    {
                      

                        using (OracleDataReader dr = cmd.ExecuteReader())
                        {
                            while (dr.Read())
                            {
                                data.Add(new
                                {
                                    ELEMENT = dr["ELEMENT"] == DBNull.Value ? null : dr["ELEMENT"].ToString(),
                                    RETURN_FINES = dr["RETURN_FINES"] == DBNull.Value ? null : (decimal?)Convert.ToDecimal(dr["RETURN_FINES"]),
                                    WET_FINES = dr["WET_FINES"] == DBNull.Value ? null : (decimal?)Convert.ToDecimal(dr["WET_FINES"]),
                                    DRY_FINES = dr["DRY_FINES"] == DBNull.Value ? null : (decimal?)Convert.ToDecimal(dr["DRY_FINES"]),
                                    DRY_FINES_500TPH = dr["DRY_FINES_500TPH"] == DBNull.Value ? null : (decimal?)Convert.ToDecimal(dr["DRY_FINES_500TPH"])

                                });
                            }
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
        public JsonResult GetFinesTrend(string type)
        {
            List<object> list = new List<object>();

            using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
            {
                con.Open();

                string column = "";

                switch (type.ToUpper())
                {
                    case "RETURN_FINES":
                        column = "RETURN_FINES_AL2O3";
                        break;

                    case "WET_FINES":
                        column = "WET_FINES_AL2O3";
                        break;

                    case "DRY_FINES":
                        column = "DRY_FINES_AL2O3";
                        break;

                    case "DRY_FINES_500TPH":
                        column = "DRY_FINES_500TPH_AL2O3";
                        break;                  

                    default:
                        column = "RETURN_FINES_AL2O3";
                        break;
                }

                string query = $@"SELECT  TRUNC(TIMESTAMP) AS TREND_DATE, {column} AS VALUE FROM imtg.T_NOA_PILE_MAT_ANAL_SHIFT
                    WHERE TIMESTAMP >= SYSDATE - 30  ORDER BY TIMESTAMP";

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


@{
    Layout = null;
}

<!DOCTYPE html>

<html>
<head>
    <meta name="viewport" content="width=device-width" />
    <title>PileQuality</title>
    <link href="~/css/bootstrap.min.css" rel="stylesheet" />
    <link href="~/css/bootstrap-datepicker.min.css" rel="stylesheet" />
    <style>
        body {
            background: white;
            padding: 20px;
        }

        .card {
            margin-top: 20px;
            margin-left: 300px;
            width: 750px;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
        }

        #loader {
            display: none;
            text-align: center;
            font-weight: bold;
            color: #0d6efd;
            margin-bottom: 10px;
        }

        .chart-cell {
            cursor: pointer;
            color: #0d6efd;
        }

            .chart-cell:hover {
                background: #f2f2f2;
            }
    </style>
</head>
<body>
    <div class="main-content">
        <div class="container">
            <div class="card">
                <h3 class="text-center">Pile Mat Wise Quality Data</h3>
                <div id="loader">Loading...</div>
                <table class="table table-bordered text-center" id="finesTable">
                    <thead>
                        <tr>
                            <th>Element</th>
                            <th>Return Fines</th>
                            <th>Wet Fines</th>
                            <th>Dry Fines</th>
                            <th>Dry Fines 500TPH</th>
                        </tr>
                    </thead>
                    <tbody></tbody>
                </table>
            </div>
        </div>
    </div>
    
    <!-- MODAL -->
    <div class="modal fade" id="trendModal" tabindex="-1">
        <div class="modal-dialog modal-lg modal-dialog-centered">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title">30 Days Trend</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
                </div>
                <div class="modal-body">
                    <div id="trendChart" style="height:400px;"></div>
                </div>
            </div>
        </div>
        </div>
    <script src="~/js/Jquey3.6.0.min.js"></script>
    <script src="~/js/bootstrap.bundle.min.js"></script>
    <script src="~/js/bootstrap-datepicker.min.js"></script>    
    <script src="https://cdn.jsdelivr.net/npm/echarts@5.5.0/dist/echarts.min.js"></script>
    <script>

let chartInstance = null;

$(document).ready(function () {
    loadFinesData();
});


$(document).on("click", ".chart-cell", function () {
    let type = $(this).data("type");
    loadTrend(type);
});

function loadFinesData() {

    $('#loader').show();

    $.ajax({
        url: '/RmbbPile/GetFinesData',
        type: 'GET',
        success: function (res) {

            $('#loader').hide();

            renderTable(res.data || res);
        },
        error: function () {
            $('#loader').hide();
            alert("Error loading data");
        }
    });
}
function renderTable(data) {

    let html = '';

    if (!data || data.length === 0) {
        html = "<tr><td colspan='5'>No Data Found</td></tr>";
    }
    else {
        data.forEach(item => {

            html += `
            <tr>
                <td>${item.ELEMENT}</td>

                <td class="chart-cell" data-type="RETURN_FINES">${item.RETURN_FINES}</td>

                <td class="chart-cell" data-type="WET_FINES">${item.WET_FINES}</td>

                <td class="chart-cell" data-type="DRY_FINES">${item.DRY_FINES}</td>

                <td class="chart-cell" data-type="DRY_FINES_500TPH">${item.DRY_FINES_500TPH}</td>
            </tr>`;
        });
    }

    $("#finesTable tbody").html(html);
}
function loadTrend(type) {

    $.ajax({
        url: '/RmbbPile/GetFinesTrend',
        type: 'GET',
        data: { type: type },
        success: function (res) {

            const modalEl = document.getElementById('trendModal');

            const modal = new bootstrap.Modal(modalEl);

            modal.show();            
            setTimeout(function () {
                drawChart(res);
            }, 300);
        },
        error: function () {
            alert("Chart load failed");
        }
    });
}

function drawChart(data) {

    if (chartInstance != null) {
        chartInstance.dispose();
    }

    chartInstance = echarts.init(document.getElementById("trendChart"));

    chartInstance.setOption({
        tooltip: { trigger: 'axis' },

        xAxis: {
            type: 'category',
            data: data.map(x => x.DATE)
        },

        yAxis: {
            type: 'value'
        },

        series: [{
            type: 'line',
            smooth: true,
            data: data.map(x => x.VALUE),
            lineStyle: { width: 3 }
        }]
    });
}

    </script>
    }


</body>
</html>
