<div class="container py-4 page-wrapper">

    <!-- Header -->
    <div class="d-flex justify-content-between align-items-center mb-4 flex-wrap gap-3">
        <h4 class="fw-bold" style="font-family:Allan,cursive;">Production</h4>
    </div>

    <form method="post">

        <!-- ================= ROW START ================= -->
        <div class="row">

            <!-- ================= LEFT TABLE ================= -->
            <div class="col-md-6">
                <div class="table-responsive">
                    <table class="table table-bordered text-center" style="font-family:'Courier New';font-weight:bold;border:2px solid black;">
                        
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

                            <!-- Furnace Rows -->
                            <tr>
                                <td>CBF</td>
                                <td><input class="form-control" id="CBF_ActOnDate" oninput="calculateAll()" /></td>
                                <td><input class="form-control" id="CBF_ActToDate" readonly /></td>
                                <td><input class="form-control" id="CBF_ReportOnDate" /></td>
                                <td><input class="form-control" id="CBF_ReportToDate" readonly /></td>
                                <td><input class="form-control" id="CBF_Balance" readonly /></td>
                            </tr>

                            <tr>
                                <td>EBF</td>
                                <td><input class="form-control" id="EBF_ActOnDate" oninput="calculateAll()" /></td>
                                <td><input class="form-control" id="EBF_ActToDate" readonly /></td>
                                <td><input class="form-control" id="EBF_ReportOnDate" /></td>
                                <td><input class="form-control" id="EBF_ReportToDate" readonly /></td>
                                <td><input class="form-control" id="EBF_Balance" readonly /></td>
                            </tr>

                            <tr>
                                <td>FBF</td>
                                <td><input class="form-control" id="FBF_ActOnDate" oninput="calculateAll()" /></td>
                                <td><input class="form-control" id="FBF_ActToDate" readonly /></td>
                                <td><input class="form-control" id="FBF_ReportOnDate" /></td>
                                <td><input class="form-control" id="FBF_ReportToDate" readonly /></td>
                                <td><input class="form-control" id="FBF_Balance" readonly /></td>
                            </tr>

                            <tr>
                                <td>GBF</td>
                                <td><input class="form-control" id="GBF_ActOnDate" oninput="calculateAll()" /></td>
                                <td><input class="form-control" id="GBF_ActToDate" readonly /></td>
                                <td><input class="form-control" id="GBF_ReportOnDate" /></td>
                                <td><input class="form-control" id="GBF_ReportToDate" readonly /></td>
                                <td><input class="form-control" id="GBF_Balance" readonly /></td>
                            </tr>

                            <tr>
                                <td>HBF</td>
                                <td><input class="form-control" id="HBF_ActOnDate" oninput="calculateAll()" /></td>
                                <td><input class="form-control" id="HBF_ActToDate" readonly /></td>
                                <td><input class="form-control" id="HBF_ReportOnDate" /></td>
                                <td><input class="form-control" id="HBF_ReportToDate" readonly /></td>
                                <td><input class="form-control" id="HBF_Balance" readonly /></td>
                            </tr>

                            <tr>
                                <td>IBF</td>
                                <td><input class="form-control" id="IBF_ActOnDate" oninput="calculateAll()" /></td>
                                <td><input class="form-control" id="IBF_ActToDate" readonly /></td>
                                <td><input class="form-control" id="IBF_ReportOnDate" /></td>
                                <td><input class="form-control" id="IBF_ReportToDate" readonly /></td>
                                <td><input class="form-control" id="IBF_Balance" readonly /></td>
                            </tr>

                            <!-- Cumulative -->
                            <tr><td>A-F</td><td><input id="CtoFBF_ActOnDate" class="form-control" readonly /></td></tr>
                            <tr><td>A-G</td><td><input id="CtoGBF_ActOnDate" class="form-control" readonly /></td></tr>
                            <tr><td>A-H</td><td><input id="CtoHBF_ActOnDate" class="form-control" readonly /></td></tr>
                            <tr><td>A-I</td><td><input id="CtoIBF_ActOnDate" class="form-control" readonly /></td></tr>

                        </tbody>
                    </table>
                </div>
            </div>

            <!-- ================= RIGHT TABLE ================= -->
            <div class="col-md-6">

                <h5 class="mb-2 fw-bold">Actual Breakup</h5>

                <div class="table-responsive">
                    <table class="table table-bordered text-center" style="font-family:'Courier New';font-weight:bold;border:2px solid black;">
                        
                        <thead>
                            <tr>
                                <th></th>
                                <th>LD1</th>
                                <th>LD2</th>
                                <th>LD3</th>
                            </tr>
                        </thead>

                        <tbody>

                            <tr>
                                <td>A-F</td>
                                <td><input id="A_F_ACT_LD1_TONS" class="form-control" readonly /></td>
                                <td><input id="A_F_ACT_LD2_TONS" class="form-control" readonly /></td>
                                <td><input id="A_F_ACT_LD3_TONS" class="form-control" readonly /></td>
                            </tr>

                            <tr>
                                <td>A-G</td>
                                <td><input id="A_G_ACT_LD1_TONS" class="form-control" readonly /></td>
                                <td><input id="A_G_ACT_LD2_TONS" class="form-control" readonly /></td>
                                <td><input id="A_G_ACT_LD3_TONS" class="form-control" readonly /></td>
                            </tr>

                            <tr>
                                <td>A-H</td>
                                <td><input id="A_H_ACT_LD1_TONS" class="form-control" readonly /></td>
                                <td><input id="A_H_ACT_LD2_TONS" class="form-control" readonly /></td>
                                <td><input id="A_H_ACT_LD3_TONS" class="form-control" readonly /></td>
                            </tr>

                            <tr>
                                <td>A-I</td>
                                <td><input id="A_I_ACT_LD1_TONS" class="form-control" readonly /></td>
                                <td><input id="A_I_ACT_LD2_TONS" class="form-control" readonly /></td>
                                <td><input id="A_I_ACT_LD3_TONS" class="form-control" readonly /></td>
                            </tr>

                        </tbody>
                    </table>
                </div>
            </div>

        </div>
        <!-- ================= ROW END ================= -->

        <div class="text-center mt-3">
            <button type="button" class="btn btn-success" onclick="calculateAll()">Calc Now</button>
        </div>

    </form>
</div>