<script>

function LoadTonnageFromDB() {

    var shift = $("#ddlshift").val();

    var date = lsSelectedFDate;

    if (!date || !shift) {
        return;
    }

    var cokeBody = $("#cokeTable tbody");

    var nutBody = $("#nutTable tbody");

    cokeBody.empty();

    nutBody.empty();

    var TOTAL_TON_SC_S = 0;
    var TOTAL_TON_NC_H = 0;
    var TOTAL_TON_NC_BF_KO = 0;
    var TOTAL_TON_NC_P25 = 0;

    $("#tblBody tr").each(function () {

        var row = $(this);

        var bunker = row.find(".bunker").val();

        if (!bunker)
            return;

        // ======================================
        // GET VALUES FROM MAIN TABLE
        // ======================================

        var c = parseFloat(row.find(".c").val()) || 0;

        var e = parseFloat(row.find(".e").val()) || 0;

        var f = parseFloat(row.find(".f").val()) || 0;

        var total = c + e + f;

        row.find(".total").val(total);

        // ======================================
        // ST.COKE
        // ======================================

        if (bunker.substring(0, 7) === "ST.COKE") {

            var cVal = c * 40;
            var eVal = e * 40;
            var fVal = f * 40;

            var rowTotal = cVal + eVal + fVal;

            TOTAL_TON_SC_S += rowTotal;

            cokeBody.append(
                "<tr>" +
                "<td>" + bunker + "</td>" +

                "<td><input type='number' class='form-control c' readonly value='" + cVal + "'></td>" +

                "<td><input type='number' class='form-control e' readonly value='" + eVal + "'></td>" +

                "<td><input type='number' class='form-control f' readonly value='" + fVal + "'></td>" +

                "<td><input type='number' class='form-control total' readonly value='" + rowTotal + "'></td>" +

                "</tr>"
            );
        }

        // ======================================
        // H/S NC
        // ======================================

        else if (bunker === "H/S NC") {

            var cVal = c * 21;
            var eVal = e * 21;
            var fVal = f * 21;

            var rowTotal = cVal + eVal + fVal;

            TOTAL_TON_NC_H += rowTotal;

            nutBody.append(
                "<tr>" +
                "<td>" + bunker + "</td>" +

                "<td><input type='number' class='form-control c' readonly value='" + cVal + "'></td>" +

                "<td><input type='number' class='form-control e' readonly value='" + eVal + "'></td>" +

                "<td><input type='number' class='form-control f' readonly value='" + fVal + "'></td>" +

                "<td><input type='number' class='form-control total' readonly value='" + rowTotal + "'></td>" +

                "</tr>"
            );
        }

        // ======================================
        // NC BF KO
        // ======================================

        else if (bunker === "NC BF KO") {

            var cVal = c * 12;
            var eVal = e * 12;
            var fVal = f * 12;

            var rowTotal = cVal + eVal + fVal;

            TOTAL_TON_NC_BF_KO += rowTotal;

            nutBody.append(
                "<tr>" +
                "<td>" + bunker + "</td>" +

                "<td><input type='number' class='form-control c' readonly value='" + cVal + "'></td>" +

                "<td><input type='number' class='form-control e' readonly value='" + eVal + "'></td>" +

                "<td><input type='number' class='form-control f' readonly value='" + fVal + "'></td>" +

                "<td><input type='number' class='form-control total' readonly value='" + rowTotal + "'></td>" +

                "</tr>"
            );
        }

        // ======================================
        // PLS_25MM_NC
        // ======================================

        else if (bunker === "PLS_25MM_NC") {

            var cVal = c * 40;
            var eVal = e * 40;
            var fVal = f * 40;

            var rowTotal = cVal + eVal + fVal;

            TOTAL_TON_NC_P25 += rowTotal;

            nutBody.append(
                "<tr>" +
                "<td>" + bunker + "</td>" +

                "<td><input type='number' class='form-control c' readonly value='" + cVal + "'></td>" +

                "<td><input type='number' class='form-control e' readonly value='" + eVal + "'></td>" +

                "<td><input type='number' class='form-control f' readonly value='" + fVal + "'></td>" +

                "<td><input type='number' class='form-control total' readonly value='" + rowTotal + "'></td>" +

                "</tr>"
            );
        }

        // ======================================
        // OTHER
        // ======================================

        else {

            cokeBody.append(
                "<tr>" +
                "<td>" + bunker + "</td>" +

                "<td><input type='number' class='form-control c' readonly value='" + c + "'></td>" +

                "<td><input type='number' class='form-control e' readonly value='" + e + "'></td>" +

                "<td><input type='number' class='form-control f' readonly value='" + f + "'></td>" +

                "<td><input type='number' class='form-control total' readonly value='" + total + "'></td>" +

                "</tr>"
            );
        }

    });

    // ======================================
    // DISPLAY TOTALS
    // ======================================

    $("#TOTAL_TON_SC_S").val(TOTAL_TON_SC_S || "");

    $("#TOTAL_TON_NC_H").val(TOTAL_TON_NC_H || "");

    $("#TOTAL_TON_NC_BF_KO").val(TOTAL_TON_NC_BF_KO || "");

    $("#TOTAL_TON_NC_P25").val(TOTAL_TON_NC_P25 || "");
}

</script>
