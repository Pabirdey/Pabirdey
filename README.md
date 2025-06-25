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
            }, function (data) {
                var jData = JSON.parse(data);                
                var values = jData.map(item => item.Value);
                var labels = jData.map(item => item.Label);

                var dataPlot = [{
                    type: 'violin',
                    y: values,
                    x: labels,
                    box: {
                        visible: true
                    },
                    line: {
                        color: 'blue'
                    },
                    meanline: {
                        visible: true
                    }
                }];

                var layout = {
                    title: "Fugitive Violin Chart",
                    yaxis: {
                        zeroline: false
                    }
                };

                Plotly.newPlot('modalPushCurrentChart1', dataPlot, layout);
            });
}

[HttpPost]
        public JsonResult Get_Fugitive_Violin_Chart(string pTimestamp, string pOvenNo, string pBatteryNo,string pPlantName)
        {
            string pTable = string.Empty;
            string sql = string.Empty;
            string CF = string.Empty;
            DataTable dt = new DataTable();
            Dictionary<string, object> param;
            
             if (pPlantName == "B10")
            {
                if (pBatteryNo == "10")
                {
                    sql = "SELECT O.ID_OVEN OVEN_NO, TRUNC(O.ST_TIME) DATETIME, ROUND(O.DURATION,2) PUSH_FORCE";
                    sql += " FROM imtg.t_cp_fugitive_emission O WHERE ";
                    sql += " TRUNC(O.ST_TIME) > (TO_DATE(:pTimestamp, 'dd/mm/yyyy') - 30) AND TRUNC(O.ST_TIME) <= TO_DATE(:pTimestamp, 'dd/mm/yyyy') ";
                    sql += "  AND O.ID_BATTERY = :pBatteryNo AND ID_OVEN=:pOvenNo";
                    sql += "  ORDER BY O.ST_TIME ";
                }
                else if (pBatteryNo == "11")
                {
                    sql = "SELECT O.ID_OVEN OVEN_NO, TRUNC(O.ST_TIME) DATETIME, ROUND(O.DURATION,2) PUSH_FORCE";
                    sql += " FROM imtg.t_cp_fugitive_emission O WHERE";
                    sql += " TRUNC(O.ST_TIME) > (TO_DATE(:pTimestamp, 'dd/mm/yyyy') - 30) AND TRUNC(A.ST_TIME) <= TO_DATE(:pTimestamp, 'dd/mm/yyyy') ";
                    sql += "  AND O.ID_BATTERY = :pBatteryNo AND ID_OVEN=:pOvenNo";
                    sql += "  ORDER BY O.ST_TIME ";
                }
            }           
          
            param = new Dictionary<string, object>();
            param.Add("pTimestamp", pTimestamp);
            param.Add("pOvenNo", pOvenNo);
            param.Add("pBatteryNo", pBatteryNo);
            dt.Clear();
            dt = DAL.GetRecords(sql, param);
            CF = JsonConvert.SerializeObject(dt, Formatting.None);

            return Json(CF, JsonRequestBehavior.AllowGet);
        }
