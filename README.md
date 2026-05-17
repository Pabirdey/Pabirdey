function TotCTOF() {

            // =========================
            // REPORTED ONDATE TOTAL
            // =========================

            let repC = Number($("#REPORTED_C").val()) || 0;
            let repE = Number($("#REPORTED_E").val()) || 0;
            let repF = Number($("#REPORTED_F").val()) || 0;

            let totalReported = repC + repE + repF;

            $("#DisplayReported").val(totalReported);
