public JsonResult Get_TAP_Hole_Metal_Details()
        {
            string sql = string.Empty;
            DataTable dt = new DataTable();
            sql ="SELECT CAST_NO,TROUGH_NO,CAST_ST_TIME,CAST_END_TIME,GUTKO,CAST_DURATION,SPEED,NO_TLC,NO_OT,";
            sql+="CH_READY_TIME,SPLACING_WETNESS_TIME,CAST_TYPE,CAST_CLAY_COND,TAPHOLE_BEHAVIOUR,HM_BEFORE_SLAG,";
            sql+="HM_AFTER_SLAG,HM_TEMP,HM_WEIGHT From Demo.T_CAST_DETAILS WHERE DATE_TIME='"+ +"' AND FUR_NAME='"+ +"';            
            dt = DAL.GetRecords(sql);
            sql = string.Empty;
            string result = JsonConvert.SerializeObject(dt, Formatting.None);
            return Json(result, JsonRequestBehavior.AllowGet);
        }
