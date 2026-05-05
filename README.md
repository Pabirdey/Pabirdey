$.ajax({
        url: "/YourController/GetTonnageData",
        type: "GET",
        data: { date: date, shift: shift },

        success: function (data) {

            // ✅ API error handling
            if (!data.success) {
                alert(data.message);
                return;
            }

            var cokeBody = $("#cokeTable tbody");
            var nutBody = $("#nutTable tbody");

            cokeBody.html("");
            nutBody.html("");

            // ✅ Coke row find
            var cokeRow = null;
            for (var i = 0; i < data.coke.length; i++) {
                if (data.coke[i].BUNKER === bunker) {
                    cokeRow = data.coke[i];
                    break;
                }
            }

            if (cokeRow) {
                cokeBody.append(
                    "<tr>" +
                    "<td>" + cokeRow.BUNKER + "</td>" +
                    "<td>" + cokeRow.C + "</td>" +
                    "<td>" + cokeRow.E + "</td>" +
                    "<td>" + cokeRow.F + "</td>" +
                    "</tr>"
                );
            }

            // ✅ Nut row find
            var nutRow = null;
            for (var j = 0; j < data.nut.length; j++) {
                if (data.nut[j].BUNKER === bunker) {
                    nutRow = data.nut[j];
                    break;
                }
            }

            if (nutRow) {
                nutBody.append(
                    "<tr>" +
                    "<td>" + nutRow.BUNKER + "</td>" +
                    "<td>" + nutRow.C + "</td>" +
                    "<td>" + nutRow.E + "</td>" +
                    "<td>" + nutRow.F + "</td>" +
                    "</tr>"
                );
            }
        },

        error: function (xhr) {
            alert("Error: " + xhr.statusText);
        }
    });
