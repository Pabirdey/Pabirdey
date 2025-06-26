  [HttpPost]
        public JsonResult Get_Voilin_Chart(string pTimestamp, string pOvenNo, string pBatteryNo,  string pPlantName)
        {
            string sql = "";
            DataTable dt = new DataTable();
            Dictionary<string, object> param = new Dictionary<string, object>();

            if (pPlantName == "B10")
            {
                if (pBatteryNo == "10" || pBatteryNo == "11")
                {
                    sql = "SELECT O.ID_OVEN AS OVEN_NO, TRUNC(O.ST_TIME) AS DATETIME, ROUND(O.DURATION, 2) AS PUSH_FORCE " +
                          "FROM imtg.t_cp_fugitive_emission O " +
                          "WHERE TRUNC(O.ST_TIME) > (TO_DATE(:pTimestamp, 'dd/mm/yyyy') - 30) " +
                          "AND TRUNC(O.ST_TIME) <= TO_DATE(:pTimestamp, 'dd/mm/yyyy') " +
                          "AND O.ID_BATTERY = :pBatteryNo AND ID_OVEN = :pOvenNo ORDER BY O.ST_TIME";

                    param.Add("pTimestamp", pTimestamp);
                    param.Add("pOvenNo", pOvenNo);
                    param.Add("pBatteryNo", pBatteryNo); // fixed key

                    dt = DAL.GetRecords(sql, param);
                }
            }

            return Json(dt, JsonRequestBehavior.AllowGet); // Directly return DataTable as JSON
        }

         function Get_CP_Fugitivity_Voilin_Chart(pOvenNo, pDate) {
            var modal = $('#FugitiveModal');
            modal.modal('show'); 
            modal.find('.modal-title').text("Oven No " + pOvenNo);
            var pBatteryNo = $('#battery_no').val();            
            var Area = 'B10'; 
            Plotly.purge('modalPushCurrentChart1'); 
            $.post('@Url.Action("Get_Voilin_Chart")', {
                pTimestamp: pDate,
                pOvenNo: pOvenNo,
                pBatteryNo: pBatteryNo,                
                pPlantName: Area
            }, function (data) {
                let parsed = JSON.parse(data);
                let pushForces = parsed.map(row => parseFloat(row.PUSH_FORCE));

                let trace = {
                    type: 'violin',
                    y: pushForces,
                    box: { visible: true },
                    line: { color: 'blue' },
                    meanline: { visible: true },
                    name: 'Push Force',
                };

                let layout = {
                    title: 'Violin Chart - Push Force',
                    yaxis: { title: 'Push Force (kg)' }
                };

                Plotly.newPlot('modalPushCurrentChart1', [trace], layout);
            });
        }

