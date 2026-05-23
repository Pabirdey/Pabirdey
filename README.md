<td>
            <select class ="form-control bunker text-start ps-01" style="height:30px;width:200px;" onchange="LoadTonnageFromDB()">
                <option value="">---Pls. Select---</option>
                <option value="WESTERN" ${item.BUNKER==='WESTERN'?'selected':''}>WESTERN</option>
                <option value="H/S NC" ${item.BUNKER==='H/S NC'?'selected':''}>H/S NC</option>
                <option value="ST.COKE - TOTAL" ${item.BUNKER==='ST.COKE - TOTAL'?'selected':''}>ST.COKE - TOTAL</option>
                <option value="EASTERN" ${item.BUNKER==='EASTERN'?'selected':''}>EASTERN</option>
                <option value="ST.COKE - HALDIA" ${item.BUNKER==='ST.COKE - HALDIA'?'selected':''}>ST.COKE - HALDIA</option>
                <option value="MIDDLE" ${item.BUNKER==='MIDDLE'?'selected':''}>MIDDLE</option>
                <option value="B/H COKE - TOTAL" ${item.BUNKER==='B/H COKE - TOTAL'?'selected':''}>B/H COKE - TOTAL</option>
                <option value="ST.COKE" ${item.BUNKER==='ST.COKE'?'selected':''}>ST.COKE</option>
                <option value="B/H LOW ASH" ${item.BUNKER==='B/H LOW ASH'?'selected':''}>B/H LOW ASH</option>
                <option value="NC BF KO" ${item.BUNKER==='NC BF KO'?'selected':''}>NC BF KO</option>
                <option value="ROUGH BREEZE" ${item.BUNKER==='ROUGH BREEZE'?'selected':''}>ROUGH BREEZE</option>
                <option value="PLS_25MM_NC" ${item.BUNKER==='PLS_25MM_NC'?'selected':''}>PLS_25MM_NC</option>
                <option value="ST.COKE - IMPORTED" ${item.BUNKER==='ST.COKE - IMPORTED'?'selected':''}>ST.COKE - IMPORTED</option>
                <option value="B/H HIGH ASH" ${item.BUNKER==='B/H HIGH ASH'?'selected':''}>B/H HIGH ASH</option>
                <option value="ST.COKE - OWN" ${item.BUNKER==='ST.COKE - OWN'?'selected':''}>ST.COKE - OWN</option>
            </select>
        </td>
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
        var c = parseFloat(row.find(".c").val()) || 0;
        var e = parseFloat(row.find(".e").val()) || 0;
        var f = parseFloat(row.find(".f").val()) || 0;
        var total = c + e + f;
        row.find(".total").val(total);
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
    });

    $("#TOTAL_TON_SC_S").val(TOTAL_TON_SC_S || "");
    $("#TOTAL_TON_NC_H").val(TOTAL_TON_NC_H || "");
    $("#TOTAL_TON_NC_BF_KO").val(TOTAL_TON_NC_BF_KO || "");
    $("#TOTAL_TON_NC_P25").val(TOTAL_TON_NC_P25 || "");
}
    </script>
