[HttpPost]
        public string SaveCarbonPaste(string DATE_TIME,string SHIFT,string BELOW_TUYERE,string NO_OF_DRUM)
        {
            OracleConnection con =new OracleConnection(iMonitorWebUtils.msConRWString);
            con.Open();
            string updateSql = @"UPDATE TEST.T_FUR_CARBON_PASTE_INJECTION SET  BELOW_TUYERE = :BELOW_TUYERE,NO_OF_DRUM = :NO_OF_DRUM  WHERE DATE_TIME = :DATE_TIME AND SHIFT = :SHIFT";
            OracleCommand upCmd = new OracleCommand(updateSql, con);            
            upCmd.Parameters.Add(":BELOW_TUYERE", OracleDbType.Varchar2).Value =string.IsNullOrEmpty(BELOW_TUYERE) ? (object)DBNull.Value : BELOW_TUYERE;
            upCmd.Parameters.Add(":NO_OF_DRUM", OracleDbType.Varchar2).Value =string.IsNullOrEmpty(NO_OF_DRUM) ? (object)DBNull.Value : NO_OF_DRUM;
            upCmd.Parameters.Add(":DATE_TIME", OracleDbType.Varchar2).Value = DATE_TIME;
            upCmd.Parameters.Add(":SHIFT", OracleDbType.Varchar2).Value = SHIFT;
            int rows = upCmd.ExecuteNonQuery();
            if (rows == 0)
            {
                string insertSql = @"INSERT INTO TEST.T_FUR_CARBON_PASTE_INJECTION(DATE_TIME, SHIFT, BELOW_TUYERE, NO_OF_DRUM) VALUES(:DATE_TIME, :SHIFT, :BELOW_TUYERE, :NO_OF_DRUM)";
                OracleCommand inCmd = new OracleCommand(insertSql, con);
                inCmd.Parameters.Add(":DATE_TIME", OracleDbType.Varchar2).Value = DATE_TIME;
                inCmd.Parameters.Add(":SHIFT", OracleDbType.Varchar2).Value = SHIFT;
                inCmd.Parameters.Add(":BELOW_TUYERE", OracleDbType.Varchar2).Value =string.IsNullOrEmpty(BELOW_TUYERE) ? (object)DBNull.Value : BELOW_TUYERE;
                inCmd.Parameters.Add(":NO_OF_DRUM", OracleDbType.Varchar2).Value =string.IsNullOrEmpty(NO_OF_DRUM) ? (object)DBNull.Value : NO_OF_DRUM;
                inCmd.ExecuteNonQuery();
            }

            con.Close();

            return "Saved Successfully";
        }
         <script>
        function saveCarbonPaste() {
            debugger;
            var rows =document.querySelectorAll("#carbon_paste_inj tbody tr");
            for (var i = 0; i < rows.length; i++) {
                var dt =rows[i].querySelector("[name='DATE_TIME']").value;
                var shift =rows[i].querySelector("[name='SHIFT']").value;
                var tuyere =rows[i].querySelector("[name='BELOW_TUYERE']").value;
                var drum =rows[i].querySelector("[name='NO_OF_DRUM']").value;
                $.ajax({url: '@Url.Action("SaveCarbonPaste", "CastHouse")',
                    type: 'POST',
                    data: {
                        DATE_TIME: dt,
                        SHIFT: shift,
                        BELOW_TUYERE: tuyere,
                        NO_OF_DRUM: drum
                    },
                    success: function (res) {
                        console.log(res);
                    },
                    error: function (err) {
                        alert("Controller not hit");
                    }
                });
            }

            alert("Saved Successfully!");
        }
    </script>
