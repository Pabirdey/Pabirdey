<div class="container py-4">

    <!-- HEADER -->
    <div class="d-flex justify-content-between align-items-center mb-3">
        <h4 class="fw-bold" style="font-family:Allan,cursive;">Production</h4>

        <div>
            <label>Date:</label>
            <input type="text" id="hiddenDate" />
        </div>
    </div>

    <form method="post">

        <div class="row">

            <!-- ================= LEFT TABLE ================= -->
            <div class="col-md-7">
                <div class="table-responsive">
                    <table class="table table-bordered text-center"
                           style="border:2px solid black;font-family:'Courier New';font-weight:bold;">

                        <thead>
                            <tr>
                                <th>Furnace</th>
                                <th>Actual On Date</th>
                                <th>Actual To Date</th>
                                <th>Reported On Date</th>
                                <th>Reported To Date</th>
                                <th>Balance</th>
                            </tr>
                        </thead>

                        <tbody>

                            <tr>
                                <td>CBF</td>
                                <td><input class="form-control" id="CBF_ActOnDate" /></td>
                                <td><input class="form-control" id="CBF_ActToDate" /></td>
                                <td><input class="form-control" id="CBF_ReportOnDate" /></td>
                                <td><input class="form-control" id="CBF_ReportToDate" /></td>
                                <td><input class="form-control" id="CBF_Balance" /></td>
                            </tr>

                            <tr>
                                <td>EBF</td>
                                <td><input class="form-control" id="EBF_ActOnDate" /></td>
                                <td><input class="form-control" id="EBF_ActToDate" /></td>
                                <td><input class="form-control" id="EBF_ReportOnDate" /></td>
                                <td><input class="form-control" id="EBF_ReportToDate" /></td>
                                <td><input class="form-control" id="EBF_Balance" /></td>
                            </tr>

                            <tr>
                                <td>FBF</td>
                                <td><input class="form-control" id="FBF_ActOnDate" /></td>
                                <td><input class="form-control" id="FBF_ActToDate" /></td>
                                <td><input class="form-control" id="FBF_ReportOnDate" /></td>
                                <td><input class="form-control" id="FBF_ReportToDate" /></td>
                                <td><input class="form-control" id="FBF_Balance" /></td>
                            </tr>

                            <tr>
                                <td>GBF</td>
                                <td><input class="form-control" id="GBF_ActOnDate" /></td>
                                <td><input class="form-control" id="GBF_ActToDate" /></td>
                                <td><input class="form-control" id="GBF_ReportOnDate" /></td>
                                <td><input class="form-control" id="GBF_ReportToDate" /></td>
                                <td><input class="form-control" id="GBF_Balance" /></td>
                            </tr>

                            <tr>
                                <td>HBF</td>
                                <td><input class="form-control" id="HBF_ActOnDate" /></td>
                                <td><input class="form-control" id="HBF_ActToDate" /></td>
                                <td><input class="form-control" id="HBF_ReportOnDate" /></td>
                                <td><input class="form-control" id="HBF_ReportToDate" /></td>
                                <td><input class="form-control" id="HBF_Balance" /></td>
                            </tr>

                            <tr>
                                <td>IBF</td>
                                <td><input class="form-control" id="IBF_ActOnDate" /></td>
                                <td><input class="form-control" id="IBF_ActToDate" /></td>
                                <td><input class="form-control" id="IBF_ReportOnDate" /></td>
                                <td><input class="form-control" id="IBF_ReportToDate" /></td>
                                <td><input class="form-control" id="IBF_Balance" /></td>
                            </tr>

                        </tbody>
                    </table>
                </div>
            </div>

            <!-- ================= RIGHT TABLE ================= -->
            <div class="col-md-5">

                <h5 class="fw-bold mb-2" style="font-family:Allan,cursive;">Actual Breakup</h5>

                <div class="table-responsive">
                    <table class="table table-bordered text-center"
                           style="border:2px solid black;font-family:'Courier New';font-weight:bold;">

                        <thead>
                            <tr>
                                <th></th>
                                <th>LD1</th>
                                <th>LD2</th>
                                <th>LD3</th>
                                <th>MRDTP</th>
                            </tr>
                        </thead>

                        <tbody>

                            <tr>
                                <td>On Date</td>
                                <td><input class="form-control" id="A_F_LD1_TONS" /></td>
                                <td><input class="form-control" id="A_F_LD2_TONS" /></td>
                                <td><input class="form-control" id="A_F_LD3_TONS" /></td>
                                <td><input class="form-control" id="A_F_MRD_TP_TONS" /></td>
                            </tr>

                            <tr>
                                <td>To Date A-F</td>
                                <td><input class="form-control" id="A_F_ACT_LD1_TONS" /></td>
                                <td><input class="form-control" id="A_F_ACT_LD2_TONS" /></td>
                                <td><input class="form-control" id="A_F_ACT_LD3_TONS" /></td>
                                <td><input class="form-control" id="A_F_ACT_MRD_TP_TONS" /></td>
                            </tr>

                            <tr>
                                <td>To Date A-G</td>
                                <td><input class="form-control" id="A_G_ACT_LD1_TONS" /></td>
                                <td><input class="form-control" id="A_G_ACT_LD2_TONS" /></td>
                                <td><input class="form-control" id="A_G_ACT_LD3_TONS" /></td>
                                <td><input class="form-control" id="A_G_ACT_MRD_TP_TONS" /></td>
                            </tr>

                            <tr>
                                <td>To Date A-H</td>
                                <td><input class="form-control" id="A_H_ACT_LD1_TONS" /></td>
                                <td><input class="form-control" id="A_H_ACT_LD2_TONS" /></td>
                                <td><input class="form-control" id="A_H_ACT_LD3_TONS" /></td>
                                <td><input class="form-control" id="A_H_ACT_MRD_TP_TONS" /></td>
                            </tr>

                            <tr>
                                <td>To Date A-I</td>
                                <td><input class="form-control" id="A_I_ACT_LD1_TONS" /></td>
                                <td><input class="form-control" id="A_I_ACT_LD2_TONS" /></td>
                                <td><input class="form-control" id="A_I_ACT_LD3_TONS" /></td>
                                <td><input class="form-control" id="A_I_ACT_MRD_TP_TONS" /></td>
                            </tr>

                        </tbody>
                    </table>
                </div>

            </div>

        </div>

        <!-- BUTTONS -->
        <div class="text-center mt-3">
            <button type="button" onclick="saveAllData()" class="btn btn-success">Save</button>
        </div>

    </form>
</div>
