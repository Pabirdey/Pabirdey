<script>
    function LoadTonnageFromDB() {    
        debugger;
        var shift = $("#ddlshift").val();
        var bunker = $("#bunkerInput").val();       
        $.ajax({
            url: "/Furnace_High_line/GetTonnageData",
            type: "GET",
            data: { date: lsSelectedFDate, shift: shift },
            success: function (data) {
                if (!data.success) {
                    alert(data.message);
                    return;
                }

                var cokeBody = $("#cokeTable tbody");
                var nutBody = $("#nutTable tbody");

                cokeBody.html("");
                nutBody.html("");

              
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
    }

    function bindTonnage(selector, data) {
        var tbody = document.querySelector(selector);
        tbody.innerHTML = ""; 
        if (!data || data.length === 0) {
            tbody.innerHTML = "<tr><td colspan='5'>No Data Found</td></tr>";
            return;
        }
        console.log("Total Records:", data.length);
        for (var i = 0; i < data.length; i++) {
            var item = data[i];
            var c = parseFloat(item.TON_C_SC) || 0;
            var e = parseFloat(item.TON_E_SC) || 0;
            var f = parseFloat(item.TON_F_SC) || 0;
            var TON_C_NC = parseFloat(item.TON_C_NC) || 0;
            var TON_E_NC = parseFloat(item.TON_E_NC) || 0;
            var TON_F_NC = parseFloat(item.TON_F_NC) || 0;

            var total = TON_C_SC + TON_E_SC + TON_F_SC;

            var row = "<tr>" +
                "<td><b>" + item.BUNKER + "</b></td>" +
                "<td><input type='number' class='form-control' value='" + c + "'></td>" +
                "<td><input type='number' class='form-control' value='" + e + "'></td>" +
                "<td><input type='number' class='form-control' value='" + f + "'></td>" +
                "<td><input type='number' class='form-control' value='" + total + "' readonly></td>" +
                "</tr>";

            tbody.innerHTML += row;
        }
        console.log("Rendered Rows:", tbody.rows.length);
    }

</script>
  <script>     
        function updateTonnage() {
            
    let bunkers = [];    
    document.querySelectorAll(".bunker").forEach(el => {
        let val = el.value.trim();
        if (val !== "" && !bunkers.includes(val)) {
            bunkers.push(val);
        }
    });    
    let cokeBody = document.querySelector("#cokeTable tbody");
    let nutBody = document.querySelector("#nutTable tbody");    
    cokeBody.innerHTML = "";
    nutBody.innerHTML = "";    
    bunkers.forEach(bunker => {
        let row = `
            <tr>
                <td><b>${bunker}</b></td>
                <td><input type="number" class="form-control c"></td>
                <td><input type="number" class="form-control e"></td>
                <td><input type="number" class="form-control f"></td>
                <td><input type="number" class="form-control total" readonly></td>
            </tr>
        `;
        cokeBody.innerHTML += row;
        nutBody.innerHTML += row;
    });    
    document.querySelectorAll("#cokeTable input, #nutTable input").forEach(input => {
        input.addEventListener("input", calculateTotal);
    });
}

function calculateTotal() {

    let row = this.closest("tr");

    let c = parseFloat(row.querySelector(".c")?.value) || 0;
    let e = parseFloat(row.querySelector(".e")?.value) || 0;
    let f = parseFloat(row.querySelector(".f")?.value) || 0;

    row.querySelector(".total").value = c + e + f;
}

    </script>
        
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
            <select class ="form-control bunker text-start ps-01" style="height:30px;width:200px;" onchange="updateTonnage()">
                <option value="">---Pls. Select---</option>
                <option value="WESTERN" ${item.BUNKER==='WESTERN'?'selected':''}>WESTERN</option>
                <option value="MIDDLE" ${item.BUNKER==='MIDDLE'?'selected':''}>MIDDLE</option>
                <option value="EASTERN" ${item.BUNKER==='EASTERN'?'selected':''}>EASTERN</option>
                <option value="H/S NC" ${item.BUNKER==='H/S NC'?'selected':''}>H/S NC</option>
                <option value="NC BF KO" ${item.BUNKER==='NC BF KO'?'selected':''}>NC BF KO</option>
                <option value="ST.COKE-HALDIA" ${item.BUNKER==='ST.COKE-HALDIA'?'selected':''}>ST.COKE-HALDIA</option>
                <option value="ST.COKE-IMPORTED" ${item.BUNKER==='ST.COKE-IMPORTED'?'selected':''}>ST.COKE-IMPORTED</option>
                <option value="ST.COKE-OWN" ${item.BUNKER==='ST.COKE-OWN'?'selected':''}>ST.COKE-OWN</option>
                <option value="ST.COKE-TOTAL" ${item.BUNKER==='ST.COKE-TOTAL'?'selected':''}>ST.COKE-TOTAL</option>
                <option value="B/H HIGH ASH" ${item.BUNKER==='B/H HIGH ASH'?'selected':''}>B/H HIGH ASH</option>
                <option value="B/H LOW ASH" ${item.BUNKER==='B/H LOW ASH'?'selected':''}>B/H LOW ASH</option>
                <option value="B/H COKE-TOTAL" ${item.BUNKER==='B/H COKE-TOTAL'?'selected':''}>B/H COKE-TOTAL</option>
                <option value="ROUGH BREEZE" ${item.BUNKER==='ROUGH BREEZE'?'selected':''}>ROUGH BREEZE</option>
                <option value="PLS_25MM_NC" ${item.BUNKER==='PLS_25MM_NC'?'selected':''}>PLS_25MM_NC</option>
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
       updateTonnage();
</script>
