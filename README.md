<script src="~/Scripts/jquery-3.7.1.min.js"></script>

<script>

    $("#btnLoad").click(function () {

        var prodDate = $("#txtProdDate").val();

        $.ajax({
            url: '/Production/GET_CBF_TO_FBF_ReportData',
            type: 'GET',
            data: { prodDate: prodDate },
            success: function (response) {

                if (response.success) {

                    var data = response.data;

                    // =====================
                    // C Furnace
                    // =====================

                    $("#ACTUAL_C").val(data.ActualC);
                    $("#ACTUAL_C_TD").val(data.ActualCTD);
                    $("#REPORTED_C").val(data.ReportedC);
                    $("#REPORTED_C_TD").val(data.ReportedCTD);
                    $("#BALANCE_C").val(data.BalanceC);

                    // =====================
                    // E Furnace
                    // =====================

                    $("#ACTUAL_E").val(data.ActualE);
                    $("#ACTUAL_E_TD").val(data.ActualETD);
                    $("#REPORTED_E").val(data.ReportedE);
                    $("#REPORTED_E_TD").val(data.ReportedETD);
                    $("#BALANCE_E").val(data.BalanceE);

                    // =====================
                    // F Furnace
                    // =====================

                    $("#ACTUAL_F").val(data.ActualF);
                    $("#ACTUAL_F_TD").val(data.ActualFTD);
                    $("#REPORTED_F").val(data.ReportedF);
                    $("#REPORTED_F_TD").val(data.ReportedFTD);
                    $("#BALANCE_F").val(data.BalanceF);

                    // =====================
                    // Display Totals
                    // =====================

                    $("#DISPLAY_ACTUAL").val(data.DisplayActual);
                    $("#DISPLAY_REPORTED").val(data.DisplayReported);
                    $("#DISPLAY_BALANCE").val(data.DisplayBalance);
                }
                else {

                    alert(response.message + "\n" + response.error);
                }
            },
            error: function (xhr) {

                alert("Error occurred while loading data.");
            }
        });

    });

</script>
