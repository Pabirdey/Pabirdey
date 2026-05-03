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
            <select class ="form-control bunker text-start ps-01" style="height:30px;width:200px;">
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
               <script>
        function calculateRow(row) {
            debugger;
            let bunker = row.querySelector(".bunker").value;          
            let C = parseFloat(row.querySelector(".c") ? row.querySelector(".c").value : 0) || 0;            
            let E = parseFloat(row.querySelector(".e") ? row.querySelector(".e").value : 0) || 0;
            let F = parseFloat(row.querySelector(".f") ? row.querySelector(".f").value : 0) || 0;            
            let total = C + E + F;
            row.querySelector(".total").value = total || "";      

            let result = {
                TON_F_SC_S: 0,
                TON_F_NC_H: 0,
                TON_F_NC_BF_KO: 0,
                TON_F_NC_P25: 0
            };           
            if (bunker && bunker.substring(0, 7) === "ST.COKE") {
                result.TON_F_SC_S = F * 40;
            }            
            if (bunker === "H/S NC") {
                result.TON_F_NC_H = F * 21;
            }           
            if (bunker === "NC BF KO") {
                result.TON_F_NC_BF_KO = F * 12;
            }            
            if (bunker === "PLS_25MM_NC") {
                result.TON_F_NC_P25 = F * 40;
            }

            console.log("Calculated:", result);

            return result;
        }

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
                        </div>
                        <!-- 🔹 SIDE BY SIDE TABLES -->
                        <div class="row">
                            <!-- Tonnage of Coke -->
                            <div class="col-md-6 col-12">
                                <div class="section-box">
                                    <div class="section-title">Tonnage of Coke</div>
                                    <table class="table table-bordered text-center">
                                        <thead>
                                            <tr>
                                                <th style="width:100px;">Bunker</th>
                                                <th>C-BF</th>
                                                <th>E-BF</th>
                                                <th>F-BF</th>
                                                <th>Total</th>
                                            </tr>
                                        </thead>
                                        <tbody>
                                            <!-- ROW -->
                                            <tr data-name="ST.COKE">
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
                                            </tr>
                                        </tbody>
                                    </table>
                                </div>
                            </div>
