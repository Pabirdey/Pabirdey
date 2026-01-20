 <script>
        function saveCarbonPaste() {
            debugger;
            var dataList = [];
            var rows =document.querySelectorAll("#carbon_paste_inj tbody tr");
            for (var i = 0; i < rows.length; i++) {
                var dt = rows[i].querySelector("[name='DATE_TIME']").value;
                var shift = rows[i].querySelector("[name='SHIFT']").value;
                var tuyere = rows[i].querySelector("[name='BELOW_TUYERE']").value;
                var drum = rows[i].querySelector("[name='NO_OF_DRUM']").value;
                var obj = {
                    DATE_TIME: dt,
                    SHIFT: shift,
                    BELOW_TUYERE: tuyere,
                    NO_OF_DRUM: drum
                };
                dataList.push(obj);
            }            
            localStorage.setItem("Save_Carbon_Paste", JSON.stringify(dataList));
            console.log(obj);
            alert("Saved Successfully!");
            loadCarbonPaste_JS();
        }
    </script>
    [HttpPost]
        public string Save_Carbon_Paste(string DATE_TIME,string SHIFT,string BELOW_TUYERE,string NO_OF_DRUM)
        {
            OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString);
            try
            {
                con.Open();
                string sql = @"MERGE INTO Test.T_FUR_CARBON_PASTE_INJECTION t
                    USING dual
                    ON (t.DATE_TIME =TO_DATE(:DATE_TIME,'YYYY-MM-DD HH24:MI:SS')AND t.SHIFT = :SHIFT)
                    WHEN MATCHED THEN  UPDATE SET  BELOW_TUYERE = :BELOW_TUYERE, NO_OF_DRUM   = :NO_OF_DRUM
                    WHEN NOT MATCHED THEN
                    INSERT(DATE_TIME, SHIFT, BELOW_TUYERE, NO_OF_DRUM) VALUES(TO_DATE(:DATE_TIME,'YYYY-MM-DD HH24:MI:SS'),:SHIFT, :BELOW_TUYERE, :NO_OF_DRUM)";
                    OracleCommand cmd =new OracleCommand(sql, con);
                    cmd.Parameters.Add(":DATE_TIME", DATE_TIME);
                    cmd.Parameters.Add(":SHIFT", SHIFT);
                    cmd.Parameters.Add(":BELOW_TUYERE", BELOW_TUYERE);
                    cmd.Parameters.Add(":NO_OF_DRUM", NO_OF_DRUM);
                cmd.ExecuteNonQuery();
                return "OO";
            }
            catch (Exception ex)
            {
                return ex.Message;
            }
            finally
            {
                con.Close();
            }
        }
