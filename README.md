tableBody += `<td>
  <div class="input-group">
    <input name="LOT_NO" class='form-control form-control-lg' value='${parsedData[i].LOT_NO}'/>
    <button type="button" class="btn btn-outline-primary openLotModal" data-index="${i}" data-bs-toggle="modal" data-bs-target="#lotModal">
      <i class="fa fa-search"></i>
    </button>
  </div>
</td>`;

<!-- LOT Modal -->
<div class="modal fade" id="lotModal" tabindex="-1" aria-labelledby="lotModalLabel" aria-hidden="true">
  <div class="modal-dialog modal-dialog-centered">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="lotModalLabel">Select LOT NO</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
        <!-- You can add a list of LOTs or a search box here -->
        <input type="text" class="form-control mb-2" placeholder="Search LOT...">
        <ul class="list-group">
          <li class="list-group-item lot-item">LOT1234</li>
          <li class="list-group-item lot-item">LOT5678</li>
          <li class="list-group-item lot-item">LOT9012</li>
        </ul>
      </div>
    </div>
  </div>
</div>

$(document).ready(function () {
    let selectedRowIndex = null;

    // Open modal and store index of clicked row
    $(document).on('click', '.openLotModal', function () {
        selectedRowIndex = $(this).data('index');
    });


     function Display_Mudgun_Details(lsSelectedFDate,IsSelectedFur) {
                $.ajax({
                    url: '@Url.Action("Get_Display_Mudgun_Details", "CastHouse")',
                    type: 'GET',
                    data: { Fdate: lsSelectedFDate, Fur: IsSelectedFur },
                    success: function (result_Mudgun_Details) {
                        var parsedData = JSON.parse(result_Mudgun_Details);
                        var tableBody = "";
                        for (var i = 0; i < parsedData.length; i++) {
                            tableBody += "<tr>";
                            tableBody += `<td><input name="CAST_NO" class='form-control form-control-lg' value='${parsedData[i].CAST_NO}' readonly/></td>`;                            
                            tableBody += `<td>
                                              <select name="CLOSURE_MODE" class ='form-select form-select-lg'>
                                                <option ${!parsedData[i].CLOSURE_MODE ? 'selected': ''} value=""></option>
                                                <option ${parsedData[i].CLOSURE_MODE === 'MUDGUN' ? 'selected': ''} data-content="<i class='fa fa-fire'></i> MUDGUN">MUDGUN</option>
                                                <option ${parsedData[i].CLOSURE_MODE === 'NULL' ? 'selected': ''} data-content="<i class='fa fa-ban'></i> NULL">NULL</option>
                                              </select>
                                            </td>`;
                            tableBody += `<td><input name="CLAY_QUANTITY" class='form-control form-control-lg' value='${parsedData[i].CLAY_QUANTITY}'/></td>`;
                            tableBody += `<td>
                                                <select name="MG_CLAY_USED" class ='form-select form-select-lg'>
                                                <option ${!parsedData[i].MG_CLAY_USED ? 'selected': ''} value=""></option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'LRH' ? 'selected': ''}>LRH</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'UBQ' ? 'selected': ''}>UBQ</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'SARVESH' ? 'selected': ''}>SARVESH</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'CALDYRS' ? 'selected': ''}>CALDYRS</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(S)' ? 'selected': ''}>HARIMA(S) </option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(D)' ? 'selected': ''}>HARIMA(D) </option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'CORUS' ? 'selected': ''}>CORUS</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'TRB' ? 'selected': ''}>TRB</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'VISUVIUS' ? 'selected': ''}>VISUVIUS</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA-TWH4' ? 'selected': ''}>HARIMA-TWH4</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA-CPH4' ? 'selected': ''}>HARIMA-CPH4</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(D)-TWH5' ? 'selected': ''}>HARIMA(D)-TWH5</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(D)-TWH5K' ? 'selected': ''}>HARIMA(D)-TWH5K</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(D)-TWH5-T' ? 'selected': ''}>HARIMA(D)-TWH5-T</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(D)-TWH5-T' ? 'selected': ''}>HARIMA(D)-TWH5-T</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(D)-TWH5-T' ? 'selected': ''}>HARIMA(D)-TWH5-T</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(D)-TWH5-T' ? 'selected': ''}>HARIMA(D)-TWH5-T</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(D)-TWH5-T' ? 'selected': ''}>HARIMA(D)-TWH5-T</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(D)-TWH5-T' ? 'selected': ''}>HARIMA(D)-TWH5-T</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(D)-TWH5-T' ? 'selected': ''}>HARIMA(D)-TWH5-T</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(D)-TWH5-T' ? 'selected': ''}>HARIMA(D)-TWH5-T</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(D)-TWH5-T' ? 'selected': ''}>HARIMA(D)-TWH5-T</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(D)-TWH5-T' ? 'selected': ''}>HARIMA(D)-TWH5-T</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(D)-TWH5-T' ? 'selected': ''}>HARIMA(D)-TWH5-T</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(D)-TWH5-T' ? 'selected': ''}>HARIMA(D)-TWH5-T</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(D)-TWH5-T' ? 'selected': ''}>HARIMA(D)-TWH5-T</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(D)-TWH5-T' ? 'selected': ''}>HARIMA(D)-TWH5-T</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(D)-TWH5-T' ? 'selected': ''}>HARIMA(D)-TWH5-T</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(D)-TWH5-T' ? 'selected': ''}>HARIMA(D)-TWH5-T</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(D)-TWH5-T' ? 'selected': ''}>HARIMA(D)-TWH5-T</option>
                                                <option ${parsedData[i].MG_CLAY_USED === 'HARIMA(D)-TWH5-T' ? 'selected': ''}>HARIMA(D)-TWH5-T</option>
                                                </select>
                                              </td>`;
                            tableBody += `<td><input name="LOT_NO" class='form-control form-control-lg' value='${parsedData[i].LOT_NO}'/></td>`;
                            tableBody += `<button type="button" class="btn btn-outline-primary openLotModal" data-index="${i}" data-bs-toggle="modal" data-bs-target="#lotModal"></button>';'                               
    

                                                tableBody += `<td><input name="NO_OF_BAGS" class='form-control form-control-lg' value='${parsedData[i].NO_OF_BAGS}'/></td>`;
                                                tableBody += `<td><input name="MUDGUN_HOLD_TIME" class='form-control form-control-lg' value='${parsedData[i].MUDGUN_HOLD_TIME}'/></td>`;

                                                tableBody += `<td>
                                                <select name="MUDGUN_NOZZLE" class ='form-select form-select-lg'>
                                                        <option ${!parsedData[i].MUDGUN_NOZZLE ? 'selected': ''} value=""></option>
                                                        <option ${parsedData[i].MUDGUN_NOZZLE === 'REPLACEMENT' ? 'selected': ''}>REPLACEMENT</option>
                                                        <option ${parsedData[i].MUDGUN_NOZZLE === 'WEILD' ? 'selected': ''}>WEILD</option>
                                                </select>
                                              </td>`;                                               
                                                tableBody += `<td><input name="MNOZZLE_BEF_CLOSING" class='form-control form-control-lg' value='${parsedData[i].MNOZZLE_BEF_CLOSING}'/></td>`;
                                                tableBody += `<td><input name="MNOZZLE_AFT_CLOSING" class='form-control form-control-lg' value='${parsedData[i].MNOZZLE_AFT_CLOSING}'/></td>`;
                                                tableBody += `<td><input name="INIT_PLUGIN_PRESSURE" class='form-control form-control-lg' value='${parsedData[i].INIT_PLUGIN_PRESSURE}'/></td>`;
                                                tableBody += `<td><input name="MAX_PLUGIN_PRESSURE" class='form-control form-control-lg' value='${parsedData[i].MAX_PLUGIN_PRESSURE}'/></td>`;
                                                tableBody += `<td><input name="FINAL_PLUGIN_PRESSURE" class='form-control form-control-lg' value='${parsedData[i].FINAL_PLUGIN_PRESSURE}'/></td>`;
                                                tableBody += `<td><input name="PRESS_ON_FORCE" class='form-control form-control-lg' value='${parsedData[i].PRESS_ON_FORCE}'/></td>`;
                                                tableBody += `<td>
                                                <select name="CLAY_LEAKAGE" class ='form-select form-select-lg'>
                                                <option ${!parsedData[i].CLAY_LEAKAGE ? 'selected': ''} value=""></option>
                                                <option ${parsedData[i].CLAY_LEAKAGE === 'YES' ? 'selected': ''}>YES</option>
                                                <option ${parsedData[i].CLAY_LEAKAGE === 'NO' ? 'selected': ''}>NO</option>
                                                </select>
                                              </td>`;
                                                tableBody += `<td>
                                                   <select name="BACK_FIRE" class='form-select form-select-lg'>
                                                    <option ${!parsedData[i].BACK_FIRE ? 'selected' : ''} value=""></option>
                                                    <option ${parsedData[i].BACK_FIRE === 'YES' ? 'selected' : ''}>YES</option>
                                                    <option ${parsedData[i].BACK_FIRE === 'NO' ? 'selected' : ''}>NO</option>
                                                  </select>
                                                </td>`;

                            tableBody += "</tr>";
                        }
                        $("#Mudgun_Details tbody").html(tableBody);
                    },
                });
            }

    // On click of lot item in modal
    $(document).on('click', '.lot-item', function () {
        const selectedLot = $(this).text();
        const row = $("#Mudgun_Details tbody tr").eq(selectedRowIndex);
        row.find('input[name="LOT_NO"]').val(selectedLot);
        $('#lotModal').modal('hide'); // Close modal
    });
});
