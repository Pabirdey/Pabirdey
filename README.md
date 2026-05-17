 $("#REPORTED_C").keydown(function (e) {

        if (e.keyCode == 9) {

            let rpt =
                parseFloat($("#REPORTED_C").val()) || 0;

            let oldRpt =
                parseFloat($("#REPORTED_C").attr("data-old-input")) || 0;

            let diff = rpt - oldRpt;

            let rptTd =
                parseFloat($("#REPORTED_C_TD").val()) || 0;

            let bal =
                parseFloat($("#BALANCE_C").val()) || 0;

            $("#REPORTED_C_TD").val(
                Math.round(rptTd + diff)
            );

            $("#BALANCE_C").val(
                Math.round(bal - diff)
            );

            $("#REPORTED_C")
                .attr("data-old-input", rpt);
        }
    });
