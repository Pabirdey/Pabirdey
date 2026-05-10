<script>
    function createRow(item = {}) {      
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

      <td>
    <input type="text" class="form-control c" value="${item.C || ''}" onkeyup="calculateTotal(this)">
</td>

<td>
    <input type="text" class="form-control e" value="${item.E || ''}" onkeyup="calculateTotal(this)">
</td>

<td>
    <input type="text" class="form-control f" value="${item.F || ''}" onkeyup="calculateTotal(this)">
</td>

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
       function calculateTotal(ele) {
           var row = ele.closest("tr");
           var c =parseFloat(row.querySelector(".c").value) || 0;
           var e =parseFloat(row.querySelector(".e").value) || 0;
           var f =parseFloat(row.querySelector(".f").value) || 0;
           var total = c + e + f;
           row.querySelector(".total").value =total.toFixed(2);
       }
</script>
<script>
    function SaveCokeUnloading() {
        $("#loaderDiv").show();
        var mainList = [];
        var cokeList = [];
        var nutList = [];    
        var mainRows = document.querySelectorAll("#tblBody tr");
        for (var i = 0; i < mainRows.length; i++) {
            var row = mainRows[i];
            var obj = {
                Date: row.querySelector(".row-date").value,
                Shift: row.querySelector(".row-shift").value,
                Bunker: row.querySelector(".bunker").value,

                C: row.querySelector(".c").value,
                E: row.querySelector(".e").value,
                F: row.querySelector(".f").value,

                Total: row.querySelector(".total").value,
                Position: row.querySelector(".position").value,
                Balance: row.querySelector(".balance").value
            };

            mainList.push(obj);
        }    
        var cokeRows = document.querySelectorAll("#cokeTable tbody tr");
        for (var j = 0; j < cokeRows.length; j++) {
            var row = cokeRows[j];
            var obj = {
                Bunker: row.cells[0].innerText,
                C: row.querySelector(".c").value,
                E: row.querySelector(".e").value,
                F: row.querySelector(".f").value,
                Total: row.querySelector(".total").value
            };

            cokeList.push(obj);
        }

        var nutRows = document.querySelectorAll("#nutTable tbody tr");
        for (var k = 0; k < nutRows.length; k++) {
            var row = nutRows[k];
            var obj = {
                Bunker: row.cells[0].innerText,
                C: row.querySelector(".c").value,
                E: row.querySelector(".e").value,
                F: row.querySelector(".f").value,
                Total: row.querySelector(".total").value
            };

            nutList.push(obj);
        }

        console.log("MAIN:", mainList);
        console.log("COKE:", cokeList);
        console.log("NUT:", nutList); 
        $.ajax({
            url: '/Furnace_High_line/SaveFurnaceCokeUnloading',
            type: 'POST',
            data: JSON.stringify({
                main: mainList,
                coke: cokeList,
                nut: nutList
            }),
            contentType: 'application/json',
            success: function () {
               // Furnace_Line_Coke_Unloading();
                SaveFurnaceCokeUnloading_ID();
            },
            error: function () {
                alert("Error Saving Data");
            }
        });
    }
    function Furnace_Line_Coke_Unloading() {          
        var shift=$("#ddlshift").val();
        var furnaces = ["C", "E", "F"];
        $("#msg").text("Processing...");            
        furnaces.forEach(function (furnace) {
            $.ajax({
                url: '/Furnace_High_line/CallProcedure_Coke_Distribution',
                type: 'POST',
                data: {
                    p_date:lsSelectedFDate,
                    p_furnace: furnace,
                    P_shift:shift
                },
                success: function (res) {                   
                },
                error: function () {                    
                }
            });

        });
    }
</script>
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
