  $("#REPORTED_C").keydown(function (e) {

            if (e.keyCode == 9) {

                let rpt =
                    parseFloat($("#REPORTED_C").val()) || 0;

                let rptTd =
                    parseFloat($("#REPORTED_C_TD").val()) || 0;

                let bal =
                    parseFloat($("#BALANCE_C").val()) || 0;

                $("#REPORTED_C_TD").val(
                    Math.round(rptTd + rpt)
                );

                $("#BALANCE_C").val(
                    Math.round(bal - rpt)
                );
            }
        });
