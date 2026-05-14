@{
    ViewBag.Title = "BF Production";
}

<!DOCTYPE html>

<html>

<head>

    <meta name="viewport"
          content="width=device-width" />

    <title>
        BF Production
    </title>

    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css"
          rel="stylesheet" />

</head>

<body>

    <div class="container mt-4">

        <div class="card shadow">

            <div class="card-header bg-primary text-white">

                <h4>
                    G H I Furnace Production
                </h4>

            </div>

            <div class="card-body">

                <!-- DATE -->

                <div class="row mb-3">

                    <div class="col-md-3">

                        <label>
                            Production Date
                        </label>

                        <input type="date"
                               id="txtDate"
                               class="form-control" />

                    </div>

                    <div class="col-md-2 mt-4">

                        <button class="btn btn-success w-100"
                                onclick="LoadData()">

                            Load Data

                        </button>

                    </div>

                </div>

                <!-- TABLE -->

                <div class="table-responsive">

                    <table class="table table-bordered text-center align-middle">

                        <thead class="table-dark">

                            <tr>

                                <th>Furnace</th>

                                <th>Actual</th>

                                <th>Reported</th>

                                <th>Balance</th>

                                <th>Actual TD</th>

                                <th>Reported TD</th>

                                <th>LD1</th>

                                <th>LD2</th>

                                <th>LD3</th>

                                <th>MRD</th>

                                <th>TP</th>

                            </tr>

                        </thead>

                        <tbody>

                            <!-- G -->

                            <tr>

                                <td>
                                    G
                                </td>

                                <td id="tdActualG"></td>

                                <td id="tdReportedG"></td>

                                <td id="tdBalanceG"></td>

                                <td id="tdActualTDG"></td>

                                <td id="tdReportedTDG"></td>

                                <td id="tdLD1G"></td>

                                <td id="tdLD2G"></td>

                                <td id="tdLD3G"></td>

                                <td id="tdMRDG"></td>

                                <td id="tdTPG"></td>

                            </tr>

                            <!-- H -->

                            <tr>

                                <td>
                                    H
                                </td>

                                <td id="tdActualH"></td>

                                <td id="tdReportedH"></td>

                                <td id="tdBalanceH"></td>

                                <td id="tdActualTDH"></td>

                                <td id="tdReportedTDH"></td>

                                <td id="tdLD1H"></td>

                                <td id="tdLD2H"></td>

                                <td id="tdLD3H"></td>

                                <td id="tdMRDH"></td>

                                <td id="tdTPH"></td>

                            </tr>

                            <!-- I -->

                            <tr>

                                <td>
                                    I
                                </td>

                                <td id="tdActualI"></td>

                                <td id="tdReportedI"></td>

                                <td id="tdBalanceI"></td>

                                <td id="tdActualTDI"></td>

                                <td id="tdReportedTDI"></td>

                                <td id="tdLD1I"></td>

                                <td id="tdLD2I"></td>

                                <td id="tdLD3I"></td>

                                <td id="tdMRDI"></td>

                                <td id="tdTPI"></td>

                            </tr>

                            <!-- TOTAL -->

                            <tr class="table-warning fw-bold">

                                <td>
                                    TOTAL
                                </td>

                                <td id="tdDisplayActual"></td>

                                <td id="tdDisplayReported"></td>

                                <td id="tdDisplayBalance"></td>

                                <td id="tdDisplayActualTD"></td>

                                <td id="tdDisplayReportedTD"></td>

                                <td colspan="5"></td>

                            </tr>

                        </tbody>

                    </table>

                </div>

            </div>

        </div>

    </div>

    <!-- JQUERY -->

    <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>

    <script>

        //------------------------------------------------
        // LOAD DATA
        //------------------------------------------------

        function LoadData() {

            var prodDate =
                $("#txtDate").val();

            if (prodDate == "") {

                alert("Select Date");

                return;
            }

            $.ajax({

                url: '/BF/LoadData',

                type: 'GET',

                data: {
                    prodDate: prodDate
                },

                success: function (res) {

                    console.log(res);

                    //-------------------------------------
                    // G H I
                    //-------------------------------------

                    $.each(res.Furnaces,
                    function (i, row) {

                        //---------------------------------
                        // G
                        //---------------------------------

                        if (row.FURNACE == "G") {

                            $("#tdActualG")
                                .html(row.ACTUAL);

                            $("#tdReportedG")
                                .html(row.REPORTED);

                            $("#tdBalanceG")
                                .html(row.BALANCE);

                            $("#tdActualTDG")
                                .html(row.ACTUAL_TD);

                            $("#tdReportedTDG")
                                .html(row.REPORTED_TD);

                            $("#tdLD1G")
                                .html(row.LD1_TONS);

                            $("#tdLD2G")
                                .html(row.LD2_TONS);

                            $("#tdLD3G")
                                .html(row.LD3_TONS);

                            $("#tdMRDG")
                                .html(row.MRDTP_TONS);

                            $("#tdTPG")
                                .html(row.NOOFTP);
                        }

                        //---------------------------------
                        // H
                        //---------------------------------

                        if (row.FURNACE == "H") {

                            $("#tdActualH")
                                .html(row.ACTUAL);

                            $("#tdReportedH")
                                .html(row.REPORTED);

                            $("#tdBalanceH")
                                .html(row.BALANCE);

                            $("#tdActualTDH")
                                .html(row.ACTUAL_TD);

                            $("#tdReportedTDH")
                                .html(row.REPORTED_TD);

                            $("#tdLD1H")
                                .html(row.LD1_TONS);

                            $("#tdLD2H")
                                .html(row.LD2_TONS);

                            $("#tdLD3H")
                                .html(row.LD3_TONS);

                            $("#tdMRDH")
                                .html(row.MRDTP_TONS);

                            $("#tdTPH")
                                .html(row.NOOFTP);
                        }

                        //---------------------------------
                        // I
                        //---------------------------------

                        if (row.FURNACE == "I") {

                            $("#tdActualI")
                                .html(row.ACTUAL);

                            $("#tdReportedI")
                                .html(row.REPORTED);

                            $("#tdBalanceI")
                                .html(row.BALANCE);

                            $("#tdActualTDI")
                                .html(row.ACTUAL_TD);

                            $("#tdReportedTDI")
                                .html(row.REPORTED_TD);

                            $("#tdLD1I")
                                .html(row.LD1_TONS);

                            $("#tdLD2I")
                                .html(row.LD2_TONS);

                            $("#tdLD3I")
                                .html(row.LD3_TONS);

                            $("#tdMRDI")
                                .html(row.MRDTP_TONS);

                            $("#tdTPI")
                                .html(row.NOOFTP);
                        }

                    });

                    //-------------------------------------
                    // TOTAL
                    //-------------------------------------

                    $("#tdDisplayActual")
                        .html(res.DISPLAY_ACTUAL);

                    $("#tdDisplayReported")
                        .html(res.DISPLAY_REPORTED);

                    $("#tdDisplayBalance")
                        .html(res.DISPLAY_BALANCE);

                    $("#tdDisplayActualTD")
                        .html(res.DISPLAY_ACTUAL_TD);

                    $("#tdDisplayReportedTD")
                        .html(res.DISPLAY_REPORTED_TD);
                },

                error: function (err) {

                    console.log(err);

                    alert("Error Loading Data");

                }

            });

        }

    </script>

</body>

</html>