  function SaveCastHouseData() {
            debugger;

            // Collect table rows data
             var rows = document.querySelectorAll("#TAP_Hot_Metal_Details tbody tr,#Driling_Slag_Details tbody tr");
            //var rows = document.querySelectorAll("#Driling_Slag_Details tbody tr");
            var CastHouse = [];
            rows.forEach(function (row) {
                var rowData = {};
                var inputs = row.querySelectorAll("input, select");
                inputs.forEach(function (input) {
                    // Trim spaces from each value
                    rowData[input.name] = input.value.trim();
                });
                CastHouse.push(rowData);
            });

            // Trim date and furnace values too
            var selectedDate = document.getElementById("tbFDatePick").value.trim();
            var selectedFurnace = document.getElementById("lstFur").value.trim();

            // Debug check
            console.log(CastHouse);
            console.log(selectedDate);
            console.log(selectedFurnace);

            // Send AJAX request

            $.ajax({
                url: '/CastHouse/SaveCastHouseData',
                type: 'POST',
                contentType: 'application/json',
                data: JSON.stringify({
                    data: CastHouse,
                    Fdate: selectedDate,
                    Fur: selectedFurnace
                }),
                success: function (response) {
                    if (response.success) {
                        Swal.fire({
                            icon: 'success',
                            text: 'Data Saved successfully!',
                            showConfirmButton: true,
                            customClass: {
                                popup: 'my-swal-popup',   // Popup box
                                title: 'my-swal-title',   // Title text
                                htmlContainer: 'my-swal-text' // Text body
                            }
                        });
                    } else {
                        Swal.fire({
                            icon: 'error',
                            title: '❌ Failed!',
                            text: 'Data could not be saved. Please try again.'
                        });
                    }
                },
                error: function () {
                    Swal.fire({
                        icon: 'error',
                        title: '🚫 Error!',
                        text: 'Something went wrong while saving.'
                    });
                }
            });
        }
 [HttpPost]
        public JsonResult SaveCastHouseData(List<Dictionary<string, string>> data, string Fdate, string Fur)
        {
            try
            {
                using (OracleConnection conn = new OracleConnection(iMonitorWebUtils.msConRWString))
                {
                    conn.Open();

                    string updateSql = @"UPDATE TEST.T_CAST_DETAILS SET  
                    CH_READY_TIME=:CH_READY_TIME,SPLACING_WETNESS_TIME=:SPLACING_WETNESS_TIME,CAST_TYPE=:CAST_TYPE,
                    CAST_CLAY_COND = :CAST_CLAY_COND,TAPHOLE_BEHAVIOUR=:TAPHOLE_BEHAVIOUR,HM_BEFORE_SLAG=:HM_BEFORE_SLAG,
                    HM_AFTER_SLAG=:HM_AFTER_SLAG,HM_TEMP=:HM_TEMP,      
                    DRILL_DIA=:DRILL_DIA,DRILL_TYPE=:DRILL_TYPE,
                    DRILL_TIME=:DRILL_TIME,NO_DRILL_BAR=:NO_DRILL_BAR,NO_DRILL_BIT=:NO_DRILL_BIT,NO_LANCING_PIPE=:NO_LANCING_PIPE,
                    NO_SHAFT_USED=:NO_SHAFT_USED,DRILL_MC_AIR_PRESSURE=:DRILL_MC_AIR_PRESSURE,TAPHOLE_LENGTH=:TAPHOLE_LENGTH,
                    LEN_DRILL_HAMMER=:LEN_DRILL_HAMMER,COLOR_FUME_DRILLING=:COLOR_FUME_DRILLING,SLAG_RETENTION=:SLAG_RETENTION,
                    SLAG_LADLE=:SLAG_LADLE,NO_CINDER_GRANULATION=:NO_CINDER_GRANULATION,GRANULATION_PERC=:GRANULATION_PERC,
                    CINDER_THEORETICAL_WT=:CINDER_THEORETICAL_WT,SLAG_RATE=:SLAG_RATE,TOTAL_SLAG=:TOTAL_SLAG
                    WHERE CAST_NO = :CAST_NO AND DATE_TIME = TO_DATE(:Fdate, 'DD-MM-YYYY') AND FUR_NAME = :Fur";

                    
                    foreach (var row in data)
                    {
                        using (OracleCommand updateCmd = new OracleCommand(updateSql, conn))
                        {
                            updateCmd.Parameters.Add(":CH_READY_TIME", row["CH_READY_TIME"]);
                            updateCmd.Parameters.Add(":SPLACING_WETNESS_TIME", row["SPLACING_WETNESS_TIME"]);
                            updateCmd.Parameters.Add(":CAST_TYPE", row["CAST_TYPE"]);
                            updateCmd.Parameters.Add(":CAST_CLAY_COND", row["CAST_CLAY_COND"]);
                            updateCmd.Parameters.Add(":TAPHOLE_BEHAVIOUR", row["TAPHOLE_BEHAVIOUR"]);
                            updateCmd.Parameters.Add(":HM_BEFORE_SLAG", row["HM_BEFORE_SLAG"]);
                            updateCmd.Parameters.Add(":HM_AFTER_SLAG", row["HM_AFTER_SLAG"]);
                            updateCmd.Parameters.Add(":HM_TEMP", row["HM_TEMP"]);
                            updateCmd.Parameters.Add(":DRILL_DIA", row["DRILL_DIA"]);
                            updateCmd.Parameters.Add(":DRILL_TYPE", row["DRILL_TYPE"]);
                            updateCmd.Parameters.Add(":DRILL_TIME", row["DRILL_TIME"]);
                            updateCmd.Parameters.Add(":NO_DRILL_BAR", row["NO_DRILL_BAR"]);
                            updateCmd.Parameters.Add(":NO_DRILL_BIT", row["NO_DRILL_BIT"]);
                            updateCmd.Parameters.Add(":NO_LANCING_PIPE", row["NO_LANCING_PIPE"]);
                            updateCmd.Parameters.Add(":NO_SHAFT_USED", row["NO_SHAFT_USED"]);
                            updateCmd.Parameters.Add(":DRILL_MC_AIR_PRESSURE", row["DRILL_MC_AIR_PRESSURE"]);
                            updateCmd.Parameters.Add(":TAPHOLE_LENGTH", row["TAPHOLE_LENGTH"]);
                            updateCmd.Parameters.Add(":LEN_DRILL_HAMMER", row["LEN_DRILL_HAMMER"]);
                            updateCmd.Parameters.Add(":COLOR_FUME_DRILLING", row["COLOR_FUME_DRILLING"]);                           
                            updateCmd.Parameters.Add(":SLAG_RETENTION", row["SLAG_RETENTION"]);
                            updateCmd.Parameters.Add(":SLAG_LADLE", row["SLAG_LADLE"]);
                            updateCmd.Parameters.Add(":NO_CINDER_GRANULATION", row["NO_CINDER_GRANULATION"]);
                            updateCmd.Parameters.Add(":GRANULATION_PERC", row["GRANULATION_PERC"]);
                            updateCmd.Parameters.Add(":CINDER_THEORETICAL_WT", row["CINDER_THEORETICAL_WT"]);
                            updateCmd.Parameters.Add(":SLAG_RATE", row["SLAG_RATE"]);
                            updateCmd.Parameters.Add(":TOTAL_SLAG", row["TOTAL_SLAG"]);                            
                            updateCmd.Parameters.Add(":CAST_NO", row["CAST_NO"]);
                            updateCmd.Parameters.Add(":Fdate", Fdate);
                            updateCmd.Parameters.Add(":Fur", Fur);
                            updateCmd.ExecuteNonQuery();
                        }
                    }
                }

                return Json(new { success = true });
            }
            catch (Exception ex)
            {
                return Json(new { success = false, message = ex.Message });
            }
        }
