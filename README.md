function Get_CP_Fugitivity_Voilin_Chart(pOvenNo, pDate) {
            var modal = $('#FugitiveModal');
            modal.find('.modal-title').text("Oven No " + pOvenNo);           
            var pBatteryNo = $('#battery_no').val();
            var pSCP = $('#hf_PC_SCP').val();            
            $.post('@Url.Action("Get_CP_Fugitivity_Voilin_Chart")', { 'pTimestamp': pDate, 'pOvenNo': pOvenNo, 'pBatteryNo': pBatteryNo, 'pPlantName': Area }, function (data) {
                var jData = JSON.parse(data);
                var Pieces = [];
               

            }
            }

              [HttpPost]
        public JsonResult Get_CP_Fugitivity_Voilin_Chart(string pTimestamp, string pOvenNo, string pBatteryNo, string pSCP, string pPlantName)
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


            param = new Dictionary<string, object>();
            param.Add("pTimestamp", pTimestamp);
            param.Add("pOvenNo", pOvenNo);
            param.Add("pBatteryId", pBatteryNo);
            dt.Clear();
            dt = DAL.GetRecords(sql, param);
            CF = JsonConvert.SerializeObject(dt, Formatting.None);

            return Json(CF, JsonRequestBehavior.AllowGet);
        }
