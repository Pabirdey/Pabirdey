<script>
function loadUsers() {
 $.ajax({
     url: '/Furnace_High_line/GetUsers',
 type: 'GET',
 success: function (data) {
 var dl = document.getElementById("UserList"); 
 dl.innerHTML = ""; 
 for (var i = 0; i < data.length; i++) {
     var option = document.createElement("option");
     option.value = data[i].USER_NAME;
      dl.appendChild(option);
 }
 },
    error: function () {
    alert("Data Load Error");
    }
});
}
</script>

 public JsonResult GetUsers()
        {
            List<object> list = new List<object>();
            using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
            {
                con.Open();
                string query = @"SELECT NAME FROM DEMO.T_BF_SIGNOFF_AUTHORITY  ORDER BY NAME";
                OracleCommand cmd = new OracleCommand(query, con);
                OracleDataReader dr = cmd.ExecuteReader();
                while (dr.Read())
                {
                    list.Add(new
                    {
                        USER_NAME = dr["NAME"].ToString()
                    });
                }
            }

            return Json(list, JsonRequestBehavior.AllowGet);
        }

    <div class="left-section">
                                        <input type="text" class="form-control custom-input" list="UserList" id="UserList" placeholder="Select Users">
                                        <datalist id="UserList">                                           
                                        </datalist>
                                    </div>
