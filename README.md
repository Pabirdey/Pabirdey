function LoadTonnageFromDB() {

    var shift = $("#ddlshift").val();
    var date = lsSelectedFDate;

    // ✅ collect all selected bunkers
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

            cokeBody.html("");
            nutBody.html("");

            // ✅ loop all bunkers
            for (var b = 0; b < bunkers.length; b++) {

                var bunker = bunkers[b];

                // 🔹 find coke
                var cokeRow = null;
                for (var i = 0; i < data.coke.length; i++) {
                    if (data.coke[i].BUNKER === bunker) {
                        cokeRow = data.coke[i];
                        break;
                    }
                }

                // 🔹 find nut
                var nutRow = null;
                for (var j = 0; j < data.nut.length; j++) {
                    if (data.nut[j].BUNKER === bunker) {
                        nutRow = data.nut[j];
                        break;
                    }
                }

                // ✅ append Coke row
                cokeBody.append(
                    "<tr>" +
                    "<td><b>" + bunker + "</b></td>" +
                    "<td><input type='number' class='form-control c' value='" + (cokeRow ? cokeRow.C : 0) + "'></td>" +
                    "<td><input type='number' class='form-control e' value='" + (cokeRow ? cokeRow.E : 0) + "'></td>" +
                    "<td><input type='number' class='form-control f' value='" + (cokeRow ? cokeRow.F : 0) + "'></td>" +
                    "<td><input type='number' class='form-control total' readonly></td>" +
                    "</tr>"
                );

                // ✅ append Nut row
                nutBody.append(
                    "<tr>" +
                    "<td><b>" + bunker + "</b></td>" +
                    "<td><input type='number' class='form-control c' value='" + (nutRow ? nutRow.C : 0) + "'></td>" +
                    "<td><input type='number' class='form-control e' value='" + (nutRow ? nutRow.E : 0) + "'></td>" +
                    "<td><input type='number' class='form-control f' value='" + (nutRow ? nutRow.F : 0) + "'></td>" +
                    "<td><input type='number' class='form-control total' readonly></td>" +
                    "</tr>"
                );
            }

            // ✅ attach calculation
            $("#cokeTable input, #nutTable input").on("input", calculateTotal);

            // ✅ calculate initial totals
            calculateAllTotals();
        }
    });
}
function calculateTotal() {
    var row = this.closest("tr");

    var c = parseFloat(row.querySelector(".c").value) || 0;
    var e = parseFloat(row.querySelector(".e").value) || 0;
    var f = parseFloat(row.querySelector(".f").value) || 0;

    row.querySelector(".total").value = c + e + f;
}

function calculateAllTotals() {
    document.querySelectorAll("#cokeTable tr, #nutTable tr").forEach(function (row) {

        var c = parseFloat(row.querySelector(".c")?.value) || 0;
        var e = parseFloat(row.querySelector(".e")?.value) || 0;
        var f = parseFloat(row.querySelector(".f")?.value) || 0;

        var totalInput = row.querySelector(".total");
        if (totalInput) {
            totalInput.value = c + e + f;
        }
    });
}
