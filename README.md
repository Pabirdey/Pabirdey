<script>

    function LoadTonnageFromDB() {

        debugger;

        var shift = $("#ddlshift").val();

        var date = lsSelectedFDate;

        var bunkers = [];

        // =========================================
        // GET ALL BUNKERS
        // =========================================

        $(".bunker").each(function () {

            var val = $(this).val();

            if (val && !bunkers.includes(val)) {

                bunkers.push(val);
            }
        });

        // =========================================
        // VALIDATION
        // =========================================

        if (!date || !shift || bunkers.length === 0) {

            return;
        }

        // =========================================
        // AJAX
        // =========================================

        $.ajax({

            url: "/Furnace_High_line/GetTonnageData",

            type: "GET",

            data: {
                date: date,
                shift: shift
            },

            success: function (data) {

                debugger;

                if (!data.success) {

                    alert(data.message);

                    return;
                }

                // =========================================
                // TABLE BODY
                // =========================================

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
                // LOOP ALL ROWS
                // =========================================

                $("#tblBody tr").each(function () {

                    debugger;

                    var row = $(this);

                    // =========================================
                    // GET VALUES FROM TEXTBOX
                    // =========================================

                    var bunker = row.find(".bunker").val();

                    var c = parseFloat(row.find(".c").val()) || 0;

                    var e = parseFloat(row.find(".e").val()) || 0;

                    var f = parseFloat(row.find(".f").val()) || 0;

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

                            "<td><input type='number' class='form-control' readonly value='" + cVal + "'></td>" +

                            "<td><input type='number' class='form-control' readonly value='" + eVal + "'></td>" +

                            "<td><input type='number' class='form-control' readonly value='" + fVal + "'></td>" +

                            "<td><input type='number' class='form-control' readonly value='" + rowTotal + "'></td>" +

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

                            "<td><input type='number' class='form-control' readonly value='" + cVal + "'></td>" +

                            "<td><input type='number' class='form-control' readonly value='" + eVal + "'></td>" +

                            "<td><input type='number' class='form-control' readonly value='" + fVal + "'></td>" +

                            "<td><input type='number' class='form-control' readonly value='" + rowTotal + "'></td>" +

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

                            "<td><input type='number' class='form-control' readonly value='" + cVal + "'></td>" +

                            "<td><input type='number' class='form-control' readonly value='" + eVal + "'></td>" +

                            "<td><input type='number' class='form-control' readonly value='" + fVal + "'></td>" +

                            "<td><input type='number' class='form-control' readonly value='" + rowTotal + "'></td>" +

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

                            "<td><input type='number' class='form-control' readonly value='" + cVal + "'></td>" +

                            "<td><input type='number' class='form-control' readonly value='" + eVal + "'></td>" +

                            "<td><input type='number' class='form-control' readonly value='" + fVal + "'></td>" +

                            "<td><input type='number' class='form-control' readonly value='" + rowTotal + "'></td>" +

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

                            "<td><input type='number' class='form-control' readonly value='" + c + "'></td>" +

                            "<td><input type='number' class='form-control' readonly value='" + e + "'></td>" +

                            "<td><input type='number' class='form-control' readonly value='" + f + "'></td>" +

                            "<td><input type='number' class='form-control' readonly value='" + total + "'></td>" +

                            "</tr>"
                        );
                    }

                });

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

            },

            error: function () {

                alert("Error loading data");

            }
        });
    }

</script>
