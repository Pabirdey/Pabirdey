   <div class="col-md-5">
                        <!-- Exception Cast Heading + Save Button -->
                        <div class="d-flex justify-content-between align-items-center mb-2">
                            <div class="section_Exception-title">Exception Cast</div>
                            <button type="button" class="btn btn-success btn-sm" onclick="saveExceptionCast()">Save</button>
                        </div>
                        <!-- Exception Cast Table -->
                        <div class="table-responsive scrollable-table" style="max-height:255px;">
                            <table class="table table-bordered table-sm text-center align-middle">
                                <thead>
                                    <tr>
                                        <th class="Heading_Tiny">ID No</th>
                                        <th class="Heading_Tiny">Taphole No</th>
                                        <th>Date Time</th>
                                        <th>HH24</th>
                                        <th>MM</th>
                                        <th>Taphole Length</th>
                                        <th>Clay Paused</th>
                                        <th>Type</th>
                                    </tr>
                                </thead>
                                <tbody id="exception_cast"></tbody>
                            </table>
                        </div>
                        <!-- Carbon Paste Inj Heading + Save Button -->
                        <div class="d-flex justify-content-between align-items-center mb-2 mt-4">
                            <div class="section_Exception-title">Carbon Paste Inj</div>
                            <button type="button" class="btn btn-success btn-sm" onclick="saveCarbonPaste()">Save</button>
                        </div>
                        <!-- Carbon Paste Inj Table -->
                        <div class="table-responsive scrollable-table" style="max-height:255px;">
                            <table class="table table-bordered table-sm text-center align-middle">
                                <thead>
                                    <tr>
                                        <th class="Heading_Small">Date Time</th>
                                        <th class="Heading_Small">Shift</th>
                                        <th class="Heading_Small">Below Tuyere</th>
                                        <th class="Heading_Small">No of Drum</th>
                                    </tr>
                                </thead>
                                <tbody id="carbon_paste_inj"></tbody>
                            </table>
                        </div>

                             
                    </div>
