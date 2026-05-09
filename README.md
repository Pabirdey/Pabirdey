function LoadTonnageFromDB() {

    var shift = $("#ddlshift").val();

    var date = lsSelectedFDate;

    var bunkers = [];

    $(".bunker").each(function () {

        var val = $(this).val();

        if (val && !bunkers.includes(val)) {

            bunkers.push(val);
        }
    });

    if (!date || !shift || bunkers.length === 0) {

        return;
    }

    $.ajax({

        url: "/Furnace_High_line/GetTonnageData",

        type: "GET",

        data: { date: date, shift: shift },

        success: function (data) {

            if (!data.success) {

                alert(data.message);

                return;
            }

            var cokeBody = $("#cokeTable tbody");

            var nutBody = $("#nutTable tbody");

            cokeBody.empty();

            nutBody.empty();

            // =========================================
            // TOTAL VARIABLES
            // =========================================

            var TOTAL_TON_SC_S = 0;

            var TOTAL_TON_NC_H = 0;

            var TOTAL_TON_NC_BF_KO = 0;

            var TOTAL_TON_NC_P25 = 0;

            // =========================================
            // LOOP BUNKERS
            // =========================================

            for (var b = 0; b < bunkers.length; b++) {

                var bunker = bunkers[b];

                var cokeRow = null;

                for (var i = 0; i < data.coke.length; i++) {

                    if (data.coke[i].BUNKER === bunker) {

                        cokeRow = data.coke[i];

                        break;
                    }
                }

                var nutRow = null;

                for (var j = 0; j < data.nut.length; j++) {

                    if (data.nut[j].BUNKER === bunker) {

                        nutRow = data.nut[j];

                        break;
                    }
                }

                // =========================================
                // VALUES
                // =========================================

                var c = parseFloat(cokeRow?.C || nutRow?.C || 0);

                var e = parseFloat(cokeRow?.E || nutRow?.E || 0);

                var f = parseFloat(cokeRow?.F || nutRow?.F || 0);

                var total = c + e + f;

                // =========================================
                // ST.COKE
                // =========================================

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

                // =========================================
                // H/S NC
                // =========================================

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

                // =========================================
                // NC BF KO
                // =========================================

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

                // =========================================
                // PLS_25MM_NC
                // =========================================

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

                // =========================================
                // OTHER BUNKERS
                // =========================================

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
            }

            // =========================================
            // NULL LOGIC
            // =========================================

            if (TOTAL_TON_SC_S === 0)
                TOTAL_TON_SC_S = "";

            if (TOTAL_TON_NC_H === 0)
                TOTAL_TON_NC_H = "";

            if (TOTAL_TON_NC_BF_KO === 0)
                TOTAL_TON_NC_BF_KO = "";

            if (TOTAL_TON_NC_P25 === 0)
                TOTAL_TON_NC_P25 = "";

            // =========================================
            // DISPLAY TOTALS
            // =========================================

            $("#TOTAL_TON_SC_S").val(TOTAL_TON_SC_S);

            $("#TOTAL_TON_NC_H").val(TOTAL_TON_NC_H);

            $("#TOTAL_TON_NC_BF_KO").val(TOTAL_TON_NC_BF_KO);

            $("#TOTAL_TON_NC_P25").val(TOTAL_TON_NC_P25);
        }
    });
}
