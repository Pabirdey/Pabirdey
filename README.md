HttpGet]
        public JsonResult GetGranShotDetails(string pdate, string pshift)
        {
            List<Granshot> list = new List<Granshot>();
            using (OracleConnection con = new OracleConnection(iMonitorWebUtils.msConRWString))
            {
                con.Open();
                string sql = @"SELECT * FROM IMTG.T_GRANSHOT_DETAILS WHERE TIMESTAMP = TO_DATE(:pdate,'DD/MM/YYYY') AND SHIFT = :pshift AND AREA ='GRANSHOT' ORDER BY CAST_NO";
                OracleCommand cmd = new OracleCommand(sql, con);
                cmd.Parameters.Add(":pdate", pdate);
                cmd.Parameters.Add(":pshift", pshift);              
                OracleDataReader dr = cmd.ExecuteReader();
                while (dr.Read())
                {
                    list.Add(new Granshot
                    {
                        CAST_NO = dr["CAST_NO"].ToString(),
                        CAST_ST_TIME = dr["CAST_ST_TIME"].ToString(),
                        CAST_END_TIME = dr["CAST_END_TIME"].ToString(),
                        TRP_NO = dr["TRP_NO"].ToString(),
                        LADLE_FLST_TIME = dr["LADLE_FLST_TIME"].ToString(),
                        LADLE_FLEND_TIME = dr["LADLE_FLEND_TIME"].ToString(),
                        ARRIVED_FROM = dr["ARRIVED_FROM"].ToString(),
                        GROSS_WT = dr["GROSS_WT"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["GROSS_WT"]),
                        TARE_WT = dr["TARE_WT"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["TARE_WT"]),
                        NET_WT = dr["NET_WT"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["NET_WT"]),
                        POURING_RATE = dr["POURING_RATE"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["POURING_RATE"]),
                        HMT = dr["HMT"].ToString(),
                        REASON_POURING = dr["REASON_POURING"].ToString(),
                        SEQ_NO = dr["SEQ_NO"] == DBNull.Value ? 0 : Convert.ToDecimal(dr["SEQ_NO"])
                    });
                }
            }

            return Json(list, JsonRequestBehavior.AllowGet);
        }

    }
    function Display_Granshot_Details() {
            debugger;
            var shift = $("#ddlshift").val();
            $.ajax({
                url: '/Granshot/Get_Granshot_Details',
                type: 'GET',
                data: {
                    pdate: lsSelectedFDate,
                    pshift: shift
                },
                success: function (result) {
                    debugger;
                    console.log("Success");
                    console.log(result);
                    BindTable(result);
                },
                error: function (xhr, status, error) {
                    debugger;
                    console.log("Error");
                    console.log(xhr.responseText);
                    console.log(error);
                }
            });

        }
        function BindTable(data) {

            $("#tblBody").empty();

            // Data found
            if (data.length > 0) {

                $.each(data, function (i, item) {

                    var row = `<tr>
                <td><input type="text" class="form-control castno" value="${item.CAST_NO || ''}"></td>
                <td><input type="text" class="form-control" value="${item.CAST_ST_TIME || ''}"></td>
                <td><input type="text" class="form-control" value="${item.CAST_END_TIME || ''}"></td>
                <td><input type="text" class="form-control" value="${item.TRP_NO || ''}"></td>
                <td><input type="text" class="form-control" value="${item.LADLE_FLST_TIME || ''}"></td>
                <td><input type="text" class="form-control" value="${item.LADLE_FLEND_TIME || ''}"></td>
                <td><input type="text" class="form-control" value="${item.ARRIVED_FROM || ''}"></td>
                <td><input type="text" class="form-control" value="${item.GROSS_WT || ''}"></td>
                <td><input type="text" class="form-control" value="${item.TARE_WT || ''}"></td>
                <td><input type="text" class="form-control" value="${item.NET_WT || ''}"></td>
                <td><input type="text" class="form-control" value="${item.POURING_RATE || ''}"></td>
                <td><input type="text" class="form-control" value="${item.HMT || ''}"></td>
                <td><input type="text" class="form-control" value="${item.REASON_POURING || ''}"></td>
                <td><input type="text" class="form-control" value="${item.SEQ_NO || ''}"></td>
                <td><button type="button">Delete</button></td>
            </tr>`;

                    $("#tblBody").append(row);
                });
            }
            else {

                // No data found - show 8 blank rows
                for (var i = 1; i <= 8; i++) {

                    var row = `<tr>
                <td><input type="text" class="form-control"></td>
                <td><input type="text" class="form-control"></td>
                <td><input type="text" class="form-control"></td>
                <td><input type="text" class="form-control"></td>
                <td><input type="text" class="form-control"></td>
                <td><input type="text" class="form-control"></td>
                <td><input type="text" class="form-control"></td>
                <td><input type="text" class="form-control"></td>
                <td><input type="text" class="form-control"></td>
                <td><input type="text" class="form-control"></td>
                <td><input type="text" class="form-control"></td>
                <td><input type="text" class="form-control"></td>
                <td><input type="text" class="form-control"></td>
                <td><input type="text" class="form-control"></td>
                <td><button type="button">Delete</button></td>
            </tr>`;

                    $("#tblBody").append(row);
                }
            }
        }
