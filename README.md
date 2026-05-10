 [HttpPost]
        public JsonResult SaveFurnaceCokeUnloading(Furnace_High_line model)
        {
            using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
            {
                con.Open();
                OracleTransaction trans = con.BeginTransaction();

                try
                {
                    
                    foreach (var item in model.main)
                    {
                        if (string.IsNullOrWhiteSpace(item.Bunker))
                            continue;

                        string query = @"MERGE INTO imtg.T_BF_CK_CONTROL_UNLOADING t
                                        USING dual
                                        ON (t.TIMESTAMP = TO_DATE(:TDATE,'DD/MM/YYYY') 
                                            AND t.SHIFT = :SHIFT 
                                            AND t.BUNKER = :BUNKER)
                                        WHEN MATCHED THEN
                                        UPDATE SET 
                                                t.C = :C,
                                                t.E = :E,
                                                t.F = :F,
                                                t.TOTAL = :TOTAL,
                                                t.BUNKER_POSITION = :POSITION,
                                                t.BALANCE = :BALANCE
                                        WHEN NOT MATCHED THEN
                                        INSERT (TIMESTAMP, SHIFT, BUNKER, C, E, F, TOTAL, BUNKER_POSITION, BALANCE)
                                        VALUES (TO_DATE(:TDATE,'DD/MM/YYYY'), :SHIFT, :BUNKER, :C, :E, :F, :TOTAL, :POSITION, :BALANCE)";
                        using (OracleCommand cmd = new OracleCommand(query, con))
                        {
                            cmd.Transaction = trans;
                            cmd.Parameters.Add("TIMESTAMP", item.Date);
                            cmd.Parameters.Add("SHIFT", item.Shift);
                            cmd.Parameters.Add("BUNKER", item.Bunker);
                            cmd.Parameters.Add("C", item.C ?? "0");
                            cmd.Parameters.Add("E", item.E ?? "0");
                            cmd.Parameters.Add("F", item.F ?? "0");
                            cmd.Parameters.Add("TOTAL", item.Total ?? "0");
                            cmd.Parameters.Add("BUNKER_POSITION", item.Position ?? "0");
                            cmd.Parameters.Add("BALANCE", item.Balance ?? "0");
                            cmd.ExecuteNonQuery();
                        }
                    }

                   
                    foreach (var item in model.coke)
                    {
                        if (string.IsNullOrWhiteSpace(item.Bunker))
                            continue;

                                    string query = @"MERGE INTO imtg.T_BF_CK_CONTROL_UNLOADING t
                                                            USING dual
                                                     ON (AND t.BUNKER = :BUNKER)
                                                    WHEN MATCHED THEN
                                                        UPDATE SET 
                                                            t.TON_C_SC = :C,
                                                            t.TON_E_SC = :E,
                                                            t.TON_F_SC = :F                       
                                                            WHEN NOT MATCHED THEN
                                                            INSERT (BUNKER, TON_C_SC, TON_E_SC, TON_F_SC)
                                                            VALUES (:BUNKER, :C, :E, :F)";
                        using (OracleCommand cmd = new OracleCommand(query, con))
                        {
                            cmd.Transaction = trans;

                            cmd.Parameters.Add("BUNKER", item.Bunker);
                            cmd.Parameters.Add("TON_C_SC", item.C ?? "0");
                            cmd.Parameters.Add("TON_E_SC", item.E ?? "0");
                            cmd.Parameters.Add("TON_F_SC", item.F ?? "0");                           
                            cmd.ExecuteNonQuery();
                        }
                    }

                   
                    foreach (var item in model.nut)
                    {
                        if (string.IsNullOrWhiteSpace(item.Bunker))
                            continue;

                        string query = @"MERGE INTO imtg.T_BF_CK_CONTROL_UNLOADING t
                                            USING dual
                                                ON (t.BUNKER = :BUNKER)
                                        WHEN MATCHED THEN
                                            UPDATE SET 
                                                t.TON_C_NC = :C,
                                                t.TON_E_NC = :E,
                                                t.TON_F_NC = :F                       
                                            WHEN NOT MATCHED THEN
                                        INSERT (BUNKER, TON_C_NC, TON_E_NC, TON_F_NC)
                                        VALUES (:BUNKER, :C, :E, :F)";
                        using (OracleCommand cmd = new OracleCommand(query, con))
                        {
                            cmd.Transaction = trans;
                            cmd.Parameters.Add("BUNKER", item.Bunker);
                            cmd.Parameters.Add("TON_C_NC", item.C ?? "0");
                            cmd.Parameters.Add("TON_E_NC", item.E ?? "0");
                            cmd.Parameters.Add("TON_F_NC", item.F ?? "0");                           
                            cmd.ExecuteNonQuery();
                        }
                    }

                    trans.Commit();
                    return Json("Success");
                }
                catch (Exception ex)
                {
                    trans.Rollback();
                    return Json("Error: " + ex.Message);
                }
            }
        }

        <script>
    function SaveCokeUnloading() {
        $("#loaderDiv").show();
        var mainList = [];
        var cokeList = [];
        var nutList = [];    
        var mainRows = document.querySelectorAll("#tblBody tr");
        for (var i = 0; i < mainRows.length; i++) {
            var row = mainRows[i];
            var obj = {
                Date: row.querySelector(".row-date").value,
                Shift: row.querySelector(".row-shift").value,
                Bunker: row.querySelector(".bunker").value,

                C: row.querySelector(".c").value,
                E: row.querySelector(".e").value,
                F: row.querySelector(".f").value,

                Total: row.querySelector(".total").value,
                Position: row.querySelector(".position").value,
                Balance: row.querySelector(".balance").value
            };

            mainList.push(obj);
        }    
        var cokeRows = document.querySelectorAll("#cokeTable tbody tr");
        for (var j = 0; j < cokeRows.length; j++) {
            var row = cokeRows[j];
            var obj = {
                Bunker: row.cells[0].innerText,
                C: row.querySelector(".c").value,
                E: row.querySelector(".e").value,
                F: row.querySelector(".f").value,
                Total: row.querySelector(".total").value
            };

            cokeList.push(obj);
        }

        var nutRows = document.querySelectorAll("#nutTable tbody tr");
        for (var k = 0; k < nutRows.length; k++) {
            var row = nutRows[k];
            var obj = {
                Bunker: row.cells[0].innerText,
                C: row.querySelector(".c").value,
                E: row.querySelector(".e").value,
                F: row.querySelector(".f").value,
                Total: row.querySelector(".total").value
            };

            nutList.push(obj);
        }

        console.log("MAIN:", mainList);
        console.log("COKE:", cokeList);
        console.log("NUT:", nutList); 
        $.ajax({
            url: '/Furnace_High_line/SaveFurnaceCokeUnloading',
            type: 'POST',
            data: JSON.stringify({
                main: mainList,
                coke: cokeList,
                nut: nutList
            }),
            contentType: 'application/json',
            success: function () {
             alert(res.message);  
                       $("#loaderDiv").hide();
               // Furnace_Line_Coke_Unloading();
               //SaveFurnaceCokeUnloading_ID();
            },
            error: function () {
                alert("Error Saving Data");
            }
        });
    }
    function Furnace_Line_Coke_Unloading() {          
        var shift=$("#ddlshift").val();
        var furnaces = ["C", "E", "F"];
        $("#msg").text("Processing...");            
        furnaces.forEach(function (furnace) {
            $.ajax({
                url: '/Furnace_High_line/CallProcedure_Coke_Distribution',
                type: 'POST',
                data: {
                    p_date:lsSelectedFDate,
                    p_furnace: furnace,
                    P_shift:shift
                },
                success: function (res) {                   
                },
                error: function () {                    
                }
            });

        });
    }
</script>
