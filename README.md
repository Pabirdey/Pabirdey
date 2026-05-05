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
 <div class="section-title">Coke Unloading</div>
                            <table class="table table-bordered text-center">
                                <thead>
                                    <tr>
                                        <th>Date</th>
                                        <th>Shift</th>
                                        <th>Bunker</th>
                                        <th>C-BF</th>
                                        <th>E-BF</th>
                                        <th>F-BF</th>
                                        <th>Total</th>
                                        <th>Position</th>
                                        <th>Balance</th>
                                    </tr>
                                </thead>
                                <tbody id="tblBody"></tbody>
                            </table>
                             <div class="section-title">Tonnage of Coke</div>
                                    <table class="table table-bordered text-center" id="cokeTable">
                                        <thead>
                                            <tr>
                                                <th>Bunker</th>
                                                <th>C-BF</th>
                                                <th>E-BF</th>
                                                <th>F-BF</th>
                                                <th>Total</th>
                                            </tr>
                                        </thead>
                                        <tbody>                                            
                                            <!-- ROW -->
                                       
                                            @*<tr data-name="ST.COKE">
                                                <td>ST.COKE</td>
                                                <td><input type="text" class="form-control TON_C_SC_S"></td>
                                                <td><input type="text" class="form-control TON_E_SC_S"></td>
                                                <td><input type="text" class="form-control TON_F_SC_S"></td>
                                                <td><input type="text" class="form-control TOTAL_TON_SC_S"></td>
                                            </tr>
                                            <tr data-name="H/S NC">
                                                <td>H/S NC</td>
                                                <td><input type="text" class="form-control TON_C_SC_H" ></td>
                                                <td><input type="text" class="form-control TON_E_SC_H" ></td>
                                                <td><input type="text" class="form-control TON_F_SC_H" ></td>
                                                <td><input type="text" class="form-control TOTAL_TON_SC_H"></td>
                                            </tr>
                                            <tr data-name="WESTERN">
                                                <td>WESTERN</td>
                                                <td><input type="text" class="form-control TON_C_SC_W"></td>
                                                <td><input type="text" class="form-control TON_E_SC_W"></td>
                                                <td><input type="text" class="form-control TON_F_SC_W"></td>>
                                                <td><input type="text" class="form-control TOTAL_TON_SC_W"></td>
                                            </tr>
                                            <tr data-name="MIDDLE">
                                                <td>MIDDLE</td>
                                                <td><input type="text" class="form-control TON_C_SC_M"></td>
                                                <td><input type="text" class="form-control TON_E_SC_M"></td>
                                                <td><input type="text" class="form-control TON_F_SC_M"></td>
                                                <td><input type="text" class="form-control TOTAL_TON_SC_M"></td>
                                            </tr>
                                            <tr data-name="EASTERN">
                                                <td>EASTERN</td>
                                                <td><input type="text" class="form-control TON_C_SC_E"></td>
                                                <td><input type="text" class="form-control TON_E_SC_E"></td>
                                                <td><input type="text" class="form-control TON_F_SC_E"></td>
                                                <td><input type="text" class="form-control TOTAL_TON_SC_E"></td>
                                            </tr>
                                            <tr data-name="NC_BF_KO">
                                                <td>NC_BF_KO</td>
                                                <td><input type="text" class="form-control TON_C_SC_N"></td>
                                                <td><input type="text" class="form-control TON_E_SC_N"></td>
                                                <td><input type="text" class="form-control TON_F_SC_N"></td>
                                                <td><input type="text" class="form-control TOTAL_TON_SC_N"></td>
                                            </tr>
                                            <tr data-name="B/H">
                                                <td>B/H</td>
                                                <td><input type="text" class="form-control TON_C_SC_B"></td>
                                                <td><input type="text" class="form-control TON_E_SC_B"></td>
                                                <td><input type="text" class="form-control TON_F_SC_B"></td>
                                                <td><input type="text" class="form-control TOTAL_TON_SC_B" id=""></td>
                                            </tr>
                                            <tr data-name="PLS_25MM_NC">
                                                <td>PLS_25MM_NC</td>
                                                <td><input type="text" class="form-control TON_C_SC_P25"></td>
                                                <td><input type="text" class="form-control TON_E_SC_P25"></td>
                                                <td><input type="text" class="form-control TON_F_SC_P25"></td>
                                                <td><input type="text" class="form-control TOTAL_TON_SC_P25"></td>
                                            </tr>*@
                                        </tbody>
                                    </table>
                                     <div class="section-title">Tonnage of Nut Coke</div>
                                    <table class="table table-bordered text-center" id="nutTable">
                                        <thead>
                                            <tr>
                                                <th>Bunker</th>
                                                <th>C-BF</th>
                                                <th>E-BF</th>
                                                <th>F-BF</th>
                                                <th>Total</th>
                                            </tr>
                                        </thead>
                                        <tbody>
                                            <!-- ROW -->
                                            @*<tr data-name="ST.COKE">
                                                <td>ST.COKE</td>
                                                <td><input type="text" class="form-control"></td>
                                                <td><input type="text" class="form-control"></td>
                                                <td><input type="text" class="form-control"></td>
                                                <td><input type="text" class="form-control"></td>
                                            </tr>
                                            <tr data-name="H/S NC">
                                                <td>H/S NC</td>
                                                <td><input type="text" class="form-control"></td>
                                                <td><input type="text" class="form-control"></td>
                                                <td><input type="text" class="form-control"></td>
                                                <td><input type="text" class="form-control"></td>
                                            </tr>
                                            <tr data-name="WESTERN">
                                                <td>WESTERN</td>
                                                <td><input type="text" class="form-control"></td>
                                                <td><input type="text" class="form-control"></td>
                                                <td><input type="text" class="form-control"></td>
                                                <td><input type="text" class="form-control"></td>
                                            </tr>
                                            <tr data-name="MIDDLE">
                                                <td>MIDDLE</td>
                                                <td><input type="text" class="form-control"></td>
                                                <td><input type="text" class="form-control"></td>
                                                <td><input type="text" class="form-control"></td>
                                                <td><input type="text" class="form-control"></td>
                                            </tr>
                                            <tr data-name="EASTERN">
                                                <td>EASTERN</td>
                                                <td><input type="text" class="form-control"></td>
                                                <td><input type="text" class="form-control"></td>
                                                <td><input type="text" class="form-control"></td>
                                                <td><input type="text" class="form-control"></td>
                                            </tr>
                                            <tr data-name="NC_BF_KO">
                                                <td>NC_BF_KO</td>
                                                <td><input type="text" class="form-control"></td>
                                                <td><input type="text" class="form-control"></td>
                                                <td><input type="text" class="form-control"></td>
                                                <td><input type="text" class="form-control"></td>
                                            </tr>
                                            <tr data-name="B/H">
                                                <td>B/H</td>
                                                <td><input type="text" class="form-control"></td>
                                                <td><input type="text" class="form-control"></td>
                                                <td><input type="text" class="form-control"></td>
                                                <td><input type="text" class="form-control"></td>
                                            </tr>
                                            <tr data-name="PLS_25MM_NC">
                                                <td>PLS_25MM_NC</td>
                                                <td><input type="text" class="form-control"></td>
                                                <td><input type="text" class="form-control"></td>
                                                <td><input type="text" class="form-control"></td>
                                                <td><input type="text" class="form-control"></td>
                                            </tr>*@
                                        </tbody>
                                    </table>
                                    <script>
        let lsSelectedFDate;        
        $(document).ready(function () {
            lsSelectedFDate = '@DateTime.Today.AddDays(0).ToString("dd/MM/yyyy", new System.Globalization.CultureInfo("en-GB"))';
            $('#currDate-value').text(lsSelectedFDate);
            $('#hiddenDate').datepicker({
                format: "dd/mm/yyyy",
                autoclose: true,
                todayHighlight: true
            }).datepicker('setDate', lsSelectedFDate);
            $('#tbFDatePick').on('click', function (e) {
                e.preventDefault();
                $('#hiddenDate').datepicker('show');
            });
            $('#hiddenDate').on('changeDate', function (e) {
                lsSelectedFDate = e.format('dd/mm/yyyy');
                $('#currDate-value').text(lsSelectedFDate);
                Display_Bin_Position();
                copyDateShiftToRows();
                Display_Coke_unloading();
                updateTonnage();
            });
            $('#ddlshift').on('change', function () {
                Display_Bin_Position();
                copyDateShiftToRows();
                Display_Coke_unloading();
                updateTonnage();
            });
            Display_Bin_Position();
            copyDateShiftToRows();  
            Display_Coke_unloading(); 
            debugger;
            //updateTonnage();
            TotUL();         
        });
        document.addEventListener("DOMContentLoaded", function () {
            updateTonnage();
        });
    </script>
