 function Display_BinDetails(furnace) {
            $.ajax({
                url: "/HML/GetATOFBinDetails",
                type: "Get",
                data: { furnace: furnace },
                success: function (data) {
                    var tbody = $("#tblBinDetails tbody");
                    tbody.empty();
                    for (var i = 0; i < data.length; i++) {                        
                        var selectedY = data[i].REQUIRED === "Y" ? "selected" : "";
                        var selectedN = data[i].REQUIRED === "N" ? "selected" : "";
                        var row = "<tr>" +
                            "<td>" + data[i].iMonitor_TAG_ID + "</td>" +
                            "<td>" + data[i].HISTORIAN_TAG_NAME + "</td>" +
                            "<td>" + data[i].WEB_COLUMN + "</td>" +
                            "<td>" + data[i].TAG_TYPE + "</td>" +
                            "<td>" +
                                "<select>" +
                                    "<option value='Y' " + selectedY + ">Y</option>" +
                                    "<option value='N' " + selectedN + ">N</option>" +
                                "</select>" +
                            "</td>" +
                            "</tr>";
                        tbody.append(row);
                    }
                },
                error: function () {
                    alert("Error loading data");
                }
            });       
        }

        function goToBinDetails() {
            var myModal = new bootstrap.Modal(document.getElementById('BinDetailsmodal'));
            myModal.show();
            Display_BinDetails($(this).val());
        }
        <div class="modal fade" id="BinDetailsmodal" tabindex="-1">
        <div class="modal-dialog modal-xl custom-modal">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title w-100 text-center" style="font-family:Allan,cursive;">Bin Details Master</h5>
                    <button type="button" class="btn-close btn-close-white" data-bs-dismiss="modal"></button>
                </div>
                <div class="modal-body">
                    <table id="tblBinDetails" class="table table-bordered" style="font-family:Courier New; font-weight:bold;">
                        <thead>
                            <tr>
                                <th style="width:40px;">iMONITOR TAG ID</th>
                                <th style="width:70px;">iHISTORIAN TAG NAME</th>
                                <th style="width:40px;">WEB COLUMN</th>
                                <th style="width:40px;">TAG TYPE</th>
                                <th style="width:40px;">REQUIRED</th>
                            </tr>
                        </thead>
                        <tbody></tbody>
                    </table>
                </div>
                <div class="modal-footer justify-content-center">
                    <button class="btn-Modalsave" onclick="btnSaveBinRequired()">Save</button>
                    <button class="btn-Modalexit" data-bs-dismiss="modal">Exit</button>
                </div>

            </div>
        </div>
    </div>
