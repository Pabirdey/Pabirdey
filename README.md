<script>
    function createRow(item = {}) {  
    debugger;
    return `
    <tr>
        <td><input type="text" class="form-control row-date" style="width:100px;" value="${formatDate(item.TIMESTAMP)}" readonly></td>

        <td>
            <select class="form-control row-shift" style="height:30px;width:50px;">
                <option ${item.SHIFT==='A'?'selected':''}>A</option>
                <option ${item.SHIFT==='B'?'selected':''}>B</option>
                <option ${item.SHIFT==='C'?'selected':''}>C</option>
            </select>
        </td>

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

        <td><input type="text" class="form-control c" value="${item.C || ''}"></td>
        <td><input type="text" class="form-control e" value="${item.E || ''}"></td>
        <td><input type="text" class="form-control f" value="${item.F || ''}"></td>

        <td><input type="text" class="form-control total" value="${item.TOTAL || ''}" readonly></td>

        <td><input type="text" class="form-control position" value="${item.BUNKER_POSITION || ''}"></td>
        <td><input type="text" class="form-control balance" value="${item.BALANCE || ''}"></td>
    </tr>`;
            }

       function copyDateShiftToRows() {         
           var headerDate = document.getElementById("hiddenDate").value;
           var headerShift = document.getElementById("ddlshift").value;          
           document.querySelectorAll("#tblBody tr").forEach(function (row) {
               var dateInput = row.querySelector(".row-date");
               var shiftSelect = row.querySelector(".row-shift");
               if (dateInput) dateInput.value = headerDate;
               if (shiftSelect) shiftSelect.value = headerShift;

           });           
            }
       function formatDate(dt) {
           if (!dt) return "";
           let d = new Date(dt);
           let day = ("0" + d.getDate()).slice(-2);
           let month = ("0" + (d.getMonth() + 1)).slice(-2);
           let year = d.getFullYear();
           return day + "/" + month + "/" + year;
       }       
</script>
<script>
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

                            cokeBody.html("");
                            nutBody.html("");                         
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
                                cokeBody.append(
                                                 "<tr>" +
                                                 "<td>" + bunker + "</td>" +
                                                 "<td><input type='number' class='form-control c' readonly value='" + (cokeRow ? getVal(cokeRow.C) : "") + "'></td>" +
                                                 "<td><input type='number' class='form-control e' readonly value='" + (cokeRow ? getVal(cokeRow.E) : "") + "'></td>" +
                                                 "<td><input type='number' class='form-control f' readonly value='" + (cokeRow ? getVal(cokeRow.F) : "") + "'></td>" +
                                                 "<td><input type='number' class='form-control total' readonly></td>" +
                                                 "</tr>"
                                             );

                                    nutBody.append(
                                            "<tr>" +
                                            "<td>" + bunker + "</td>" +
                                            "<td><input type='number' class='form-control c' readonly value='" + (nutRow ? getVal(nutRow.C) : "") + "'></td>" +
                                            "<td><input type='number' class='form-control e' readonly value='" + (nutRow ? getVal(nutRow.E) : "") + "'></td>" +
                                            "<td><input type='number' class='form-control f' readonly value='" + (nutRow ? getVal(nutRow.F) : "") + "'></td>" +
                                            "<td><input type='number' class='form-control total' readonly></td>" +
                                            "</tr>"
                                );
                            }                          
                            $("#cokeTable input, #nutTable input").on("input", calculateTotal);                            
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
    
                function getVal(val) {
                    return (val === null || val === undefined) ? "" : val;
                }



</script>
