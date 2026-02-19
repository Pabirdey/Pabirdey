<div class="modal fade" id="mgClayOtherModal" tabindex="-1">
        <div class="modal-dialog modal-md modal-dialog-centered">
            <div class="modal-content">
                <!-- HEADER -->
                <div class="modal-header">
                    <h5 class="modal-title w-100 text-center">Bin Details Master</h5>
                    <button type="button" class="btn-close btn-close-white" data-bs-dismiss="modal"></button>
                </div>
                <!-- BODY -->
                <div class="modal-body">
                    <div class="title-box">Weightage of Clay</div>
                    <div class="clay-box">
                        <!-- Clay 1 (DROPDOWN) -->
                        <div class="row align-items-center mb-3">
                            <div class="col-2 clay-label">Clay1</div>
                            <div class="col-7">
                                <select class="form-select clay-input" id="MG_CLAY1">
                                    <option value="">-- Select Clay1 --</option>
                                    <option>ACE</option>                                   
                                </select>
                            </div>
                            <div class="col-3">
                                <select class="form-select clay-input" id="P1">
                                    <option value="">%</option>
                                    <option>5</option>                                   
                                </select>
                            </div>
                        </div>
                        <!-- Clay 2 -->
                        <div class="row align-items-center mb-3">
                            <div class="col-2 clay-label">Clay2</div>
                            <div class="col-7">
                                <select class="form-select clay-input" id="MG_CLAY2">
                                    <option value="">-- Select Clay2 --</option>
                                    <option>ACE</option>                                   
                                </select>
                            </div>
                            <div class="col-3">
                                <select class="form-select clay-input" id="P2">
                                    <option value="">%</option>
                                    <option>5</option>                                   
                                </select>
                            </div>
                        </div>
                        <!-- Clay 3 -->
                        <div class="row align-items-center">
                            <div class="col-2 clay-label">Clay3</div>
                            <div class="col-7">
                                <select class="form-select clay-input" id="MG_CLAY3">
                                    <option value="">-- Select Clay3 --</option>
                                    <option>ACE</option>                                   
                                </select>
                            </div>
                            <div class="col-3">
                                <select class="form-select clay-input" id="P3">
                                    <option value="">%</option>
                                    <option>5</option>                                   
                                </select>
                            </div>
                        </div>
                    </div>
                </div>
                <!-- FOOTER -->
                <div class="modal-footer justify-content-center">
                    <button class="btn btn-save" onclick="checkClay()">Save</button>
                    <button class="btn btn-exit" data-bs-dismiss="modal">Exit</button>
                </div>
            </div>
        </div>
    </div>

     function goToBinDetails() {
            var Bin_Required = [];
            var furnace = document.getElementById("ddlFurnace").value;
            var rows = document.querySelectorAll("#tblBinDetails tbody tr");
            for (var i = 0; i < rows.length; i++) {
                var Web_Id = rows[i].getAttribute("data-tagid");
                var Required = rows[i].querySelector("td").innerText.trim();
                Bin_Required.push({
                    Web_Id: Web_Id,
                    Required: Required
                });
            }
            var data = {
                furnace: furnace,
                SL_NO: Web_Id,
                Bin_Required: Bin_Required
            };

            $.ajax({
                url: '/HML/SaveATOFBinRequired',
                type: 'POST',
                contentType: 'application/json',
                data: JSON.stringify(data),
                success: function (res) {
                    alert(res.message);
                },
                error: function () {
                    alert("Error saving data");
                }
            });
        }
