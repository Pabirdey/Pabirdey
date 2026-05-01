function SaveBinPosition() {
           var list = [];
           var shift = $("#ddlshift").val();
           $(".cell").each(function () {
               //var value = $(this).val();
               //var cellId=$(this).data("id");
               //if(value!==null && value.trim()!==""){
               list.push({
                   CellId: $(this).data("id"),
                   Value: $(this).val(),
                   Date: lsSelectedFDate,
                   Shift: shift
               });
            //}
           });

           console.log(list);
           $.ajax({
               url: '/Furnace_High_line/Save_Furnace_High_Line',
               type: 'POST',
               data: JSON.stringify({ list: list }),  
               contentType: 'application/json',
               success: function (res) {
                   if (res.success) {
                       alert(res.message);   
                   }
                   else {
                       alert(res.message);
                   }
               },

               error: function () {
                   alert("Save failed!");
               }
           });
       }

          [HttpPost]
        public JsonResult Save_Furnace_High_Line(List<Furnace_High_line> list)
        {
            try
            {
                using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
                {
                    con.Open();

                    using (OracleTransaction trans = con.BeginTransaction())
                    {
                        foreach (var item in list)
                        {                           
                            object dbValue;
                            if (string.IsNullOrWhiteSpace(item.Value))
                            {
                                dbValue = DBNull.Value;
                            }
                            else
                            {
                                dbValue = item.Value.Trim();   
                            }

                            
                            string updateSql = @"UPDATE DEMO.T_HIGHLINE_REPORT_DATA
                                                    SET TAG_VAL = :val
                                                    WHERE TAG_ID = :TAG_ID
                                                    AND TRUNC(TIMESTAMP) = :dt
                                                    AND SHIFT = :shift";

                            using (OracleCommand updateCmd = new OracleCommand(updateSql, con))
                            {
                                updateCmd.Transaction = trans;
                                updateCmd.Parameters.Add(":val", OracleDbType.Varchar2).Value = dbValue;
                                updateCmd.Parameters.Add(":TAG_ID", OracleDbType.Varchar2).Value = item.CellId ?? "";
                                updateCmd.Parameters.Add(":dt", OracleDbType.Date).Value = Convert.ToDateTime(item.Date);
                                updateCmd.Parameters.Add(":shift", OracleDbType.Varchar2).Value = item.Shift ?? "";
                                int rowsAffected = updateCmd.ExecuteNonQuery();                                
                                if (rowsAffected == 0)
                                {
                                    string insertSql = @"INSERT INTO DEMO.T_HIGHLINE_REPORT_DATA
                                                        (TIMESTAMP, SHIFT, TAG_ID, TAG_VAL)
                                                        VALUES (:dt, :shift, :TAG_ID, :val)";

                                    using (OracleCommand insertCmd = new OracleCommand(insertSql, con))
                                    {
                                        insertCmd.Transaction = trans;
                                        insertCmd.Parameters.Add(":dt", OracleDbType.Date).Value = Convert.ToDateTime(item.Date);
                                        insertCmd.Parameters.Add(":shift", OracleDbType.Varchar2).Value = item.Shift ?? "";
                                        insertCmd.Parameters.Add(":TAG_ID", OracleDbType.Varchar2).Value = item.CellId ?? "";
                                        insertCmd.Parameters.Add(":val", OracleDbType.Varchar2).Value = dbValue;
                                        insertCmd.ExecuteNonQuery();
                                    }
                                }
                            }
                        }

                        trans.Commit();
                    }
                }

                return Json(new { success = true, message = " Raw Material Position Data Saved Successfully" });
            }
            catch (Exception ex)
            {
                return Json(new { success = false, message = ex.Message });
            }
        }
