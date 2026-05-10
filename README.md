If substr(:bunker,1,7)='ST.COKE' THEN
	:global.temp:=nvl(:TON_C_SC_S,0);
	:TON_C_SC_S:=(:global.temp)+:C*40;
END IF;

IF :BUNKER = 'H/S NC' THEN
		:TON_C_NC_H:=:C*21;
END IF;

IF :BUNKER = 'NC BF KO' THEN
	:TON_C_NC_BF_KO:=:C*12;
END IF;
IF :BUNKER = 'PLS_25MM_NC' THEN
	:TON_C_NC_P25:=:C*40;
END IF;

:TOTAL := NVL(:A,0)+NVL(:B,0)+NVL(:C,0)+NVL(:D,0)+NVL(:E,0)+NVL(:F,0);
:TOTAL_TON_SC_S:=NVL(:TON_A_SC_S,0)+NVL(:TON_B_SC_S,0)+NVL(:TON_C_SC_S,0)+NVL(:TON_D_SC_S,0)+NVL(:TON_E_SC_S,0)+NVL(:TON_F_SC_S,0);
:TOTAL_TON_NC_H:=NVL(:TON_A_NC_H,0)+NVL(:TON_B_NC_H,0)+NVL(:TON_C_NC_H,0)+NVL(:TON_D_NC_H,0)+NVL(:TON_E_NC_H,0)+NVL(:TON_F_NC_H,0);
:TOTAL_TON_NC_BF_KO:=NVL(:TON_A_NC_BF_KO,0)+NVL(:TON_B_NC_BF_KO,0)+NVL(:TON_C_NC_BF_KO,0)+NVL(:TON_D_NC_BF_KO,0)+NVL(:TON_E_NC_BF_KO,0)+NVL(:TON_F_NC_BF_KO,0);
:TOTAL_TON_NC_P25:=NVL(:TON_A_NC_P25,0)+NVL(:TON_B_NC_P25,0)+NVL(:TON_C_NC_P25,0)+NVL(:TON_D_NC_P25,0)+NVL(:TON_E_NC_P25,0)+NVL(:TON_F_NC_P25,0);


If :TOTAL_TON_SC_S=0 Then
	:TOTAL_TON_SC_S:= null;
End If;
If :TOTAL_TON_NC_H=0 Then
	:TOTAL_TON_NC_H:= null;
End If;
If :TOTAL_TON_NC_BF_KO=0 Then
	:TOTAL_TON_NC_BF_KO:= null;
End If;
If :TOTAL_TON_NC_P25=0 Then
	:TOTAL_TON_NC_P25:= null;
End If;
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
