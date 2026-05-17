 <script>
       function Dis_GBF_TO_IBF_ReportData(lsSelectedFDate) {
           $.ajax({
               url:'@Url.Action("GET_GBF_IBF_ACTUAL_REPORT", "HML")',
               type: 'GET',
               data: { prodDate: lsSelectedFDate },
               success: function (res) {
                   if (!res.success) {
                       alert(res.message);
                       return;
                   }
                   res.data.Furnaces.forEach(function (item){                       
                       if (item.FURNACE === "G") {
                           $("#TXT_FURNACE_G").val(item.FURNACE);
                           $("#TXT_ACTUAL_G").val(item.ACTUAL);
                           $("#TXT_ACTUAL_G_TD").val(item.ACTUAL_TD);
                           $("#TXT_RPT_G").val(item.REPORTED);
                           $("#TXT_RPT_G_TD").val(item.REPORTED_TD);
                           $("#TXT_BAL_G").val(item.BALANCE);
                       }
                       if (item.FURNACE === "H") {
                           $("#TXT_FURNACE_H").val(item.FURNACE);
                           $("#TXT_ACTUAL_H").val(item.ACTUAL);
                           $("#TXT_ACTUAL_H_TD").val(item.ACTUAL_TD);
                           $("#TXT_RPT_H").val(item.REPORTED);
                           $("#TXT_RPT_H_TD").val(item.REPORTED_TD);
                           $("#TXT_BAL_H").val(item.BALANCE);
                       }
                       if (item.FURNACE === "I") {
                           $("#TXT_FURNACE_I").val(item.FURNACE);
                           $("#TXT_ACTUAL_I").val(item.ACTUAL);
                           $("#TXT_ACTUAL_I_TD").val(item.ACTUAL_TD);
                           $("#TXT_RPT_I").val(item.REPORTED);
                           $("#TXT_RPT_I_TD").val(item.REPORTED_TD);
                           $("#TXT_BAL_I").val(item.BALANCE);
                       }

                   });

               },

               error: function () {
                   alert("Error Loading Data");
               }

           });
       }
   </script>

    <script>  
        function Dis_CBF_TO_FBF_ReportData(lsSelectedFDate) {           
            $.ajax({
                url: '/HML/GET_CBF_TO_FBF_ReportData',
                type: 'GET',
                data: { prodDate: lsSelectedFDate },
                success: function (response) {
                    if (response.success) {
                        var data = response.data;
                        $("#ACTUAL_C").val(data.ActualC);
                        $("#ACTUAL_C_TD").val(data.ACTUAL_C_TD);
                        $("#REPORTED_C").val(data.ReportedC);
                        $("#REPORTED_C_TD").val(data.REPORTED_C_TD);
                        $("#BALANCE_C").val(data.BalanceC);
                        $("#ACTUAL_E").val(data.ActualE);
                        $("#ACTUAL_E_TD").val(data.ACTUAL_E_TD);
                        $("#REPORTED_E").val(data.ReportedE);
                        $("#REPORTED_E_TD").val(data.REPORTED_E_TD);
                        $("#BALANCE_E").val(data.BalanceE);
                        $("#ACTUAL_F").val(data.ActualF);
                        $("#ACTUAL_F_TD").val(data.ACTUAL_F_TD);
                        $("#REPORTED_F").val(data.ReportedF);
                        $("#REPORTED_F_TD").val(data.REPORTED_F_TD);
                        $("#BALANCE_F").val(data.BalanceF);

                    }
                    else {

                        alert(response.message + "\n" + response.error);
                    }
                },
                error: function (xhr) {

                    alert("Error occurred while loading data.");
                }
            });
        }
    </script>
