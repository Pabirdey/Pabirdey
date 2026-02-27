<!DOCTYPE html>
<html>
<head>
    <title>Production</title>

    <!-- Bootstrap 5 -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">

    <style>
        .page-wrapper {
            max-width: 900px;   /* Small professional width */
            margin: auto;
        }
    </style>
</head>

<body class="bg-light">

<div class="container py-4 page-wrapper">
    <div class="card shadow-lg rounded-4">
        <div class="card-body">

            <!-- Header -->
            <div class="d-flex justify-content-between align-items-center mb-4 flex-wrap gap-3">
                <div class="d-flex align-items-center gap-3 flex-wrap">
                    <h4 class="fw-bold mb-0">Production</h4>
                    <label class="fw-semibold">Date</label>
                    <input type="date" class="form-control" style="width:150px" value="2026-02-26">
                </div>

                <button class="btn btn-primary">Refresh Balance</button>
            </div>

            <!-- ===================== MAIN TABLE ===================== -->

            <div class="table-responsive">
                <table class="table table-bordered table-hover text-center align-middle">
                    <thead class="table-dark">
                        <tr>
                            <th>Date Time</th>
                            <th>Furnace</th>
                            <th>On Date</th>
                            <th>To Date</th>
                            <th>On Date</th>
                            <th>To Date</th>
                            <th>Balance</th>
                        </tr>
                    </thead>

                    <tbody>
                        <tr>
                            <td>26-Feb-2026</td>
                            <td>C</td>
                            <td>2094.49</td>
                            <td>50700.21</td>
                            <td><input type="text" class="form-control form-control-sm text-center" value="2100"></td>
                            <td>50500</td>
                            <td class="fw-bold text-success">200.21</td>
                        </tr>

                        <tr>
                            <td>26-Feb-2026</td>
                            <td>D</td>
                            <td>-</td>
                            <td>-</td>
                            <td><input type="text" class="form-control form-control-sm text-center"></td>
                            <td>-</td>
                            <td>-</td>
                        </tr>

                        <tr>
                            <td>26-Feb-2026</td>
                            <td>E</td>
                            <td>1227.7</td>
                            <td>29949.52</td>
                            <td><input type="text" class="form-control form-control-sm text-center" value="1200"></td>
                            <td>30200</td>
                            <td class="fw-bold text-danger">-250.48</td>
                        </tr>

                        <tr>
                            <td>26-Feb-2026</td>
                            <td>F</td>
                            <td>4107.22</td>
                            <td>105014.29</td>
                            <td><input type="text" class="form-control form-control-sm text-center" value="4100"></td>
                            <td>105900</td>
                            <td class="fw-bold text-danger">-885.71</td>
                        </tr>

                        <tr>
                            <td>26-Feb-2026</td>
                            <td>G</td>
                            <td>2609.38</td>
                            <td>148145.01</td>
                            <td><input type="text" class="form-control form-control-sm text-center" value="2700"></td>
                            <td>148200</td>
                            <td class="fw-bold text-danger">-54.99</td>
                        </tr>

                        <tr>
                            <td>26-Feb-2026</td>
                            <td>H</td>
                            <td>8677.83</td>
                            <td>216254.89</td>
                            <td><input type="text" class="form-control form-control-sm text-center" value="8750"></td>
                            <td>216800</td>
                            <td class="fw-bold text-danger">-545.11</td>
                        </tr>

                        <tr>
                            <td>26-Feb-2026</td>
                            <td>I</td>
                            <td>9195.35</td>
                            <td>214289.53</td>
                            <td><input type="text" class="form-control form-control-sm text-center" value="9100"></td>
                            <td>214900</td>
                            <td class="fw-bold text-danger">-610.47</td>
                        </tr>

                        <!-- Summary -->
                        <tr class="table-secondary fw-bold">
                            <td></td>
                            <td>A-F</td>
                            <td>7429.41</td>
                            <td>185664.02</td>
                            <td>7400</td>
                            <td>186600</td>
                            <td>-935.98</td>
                        </tr>

                        <tr class="table-secondary fw-bold">
                            <td></td>
                            <td>A-G</td>
                            <td>10038.79</td>
                            <td>333809.03</td>
                            <td>10100</td>
                            <td>334800</td>
                            <td>-990.97</td>
                        </tr>

                        <tr class="table-secondary fw-bold">
                            <td></td>
                            <td>A-H</td>
                            <td>18716.62</td>
                            <td>550063.92</td>
                            <td>18850</td>
                            <td>551600</td>
                            <td>-1536.08</td>
                        </tr>

                        <tr class="table-secondary fw-bold">
                            <td></td>
                            <td>A-I</td>
                            <td>27911.97</td>
                            <td>764353.45</td>
                            <td>27950</td>
                            <td>766500</td>
                            <td>-2146.55</td>
                        </tr>

                    </tbody>
                </table>
            </div>

            <!-- ===================== ACTUAL BREAKUP ===================== -->

            <h5 class="mt-4 mb-3 fw-bold border-bottom pb-2">
                ACTUAL BREAKUP
            </h5>

            <div class="table-responsive">
                <table class="table table-bordered table-hover text-center align-middle">
                    <thead class="table-dark">
                        <tr>
                            <th></th>
                            <th>LD1 Tons</th>
                            <th>LD2 Tons</th>
                            <th>LD3 Tons</th>
                            <th>MRD TP Tons</th>
                            <th>No of TP</th>
                            <th>No of Slag Ladle</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td class="fw-bold">On Date</td>
                            <td>6443.75</td>
                            <td></td>
                            <td>985.66</td>
                            <td></td>
                            <td><input type="text" class="form-control form-control-sm text-center" value="35.35"></td>
                            <td><input type="text" class="form-control form-control-sm text-center"></td>
                        </tr>

                        <tr>
                            <td class="fw-bold">To Date A-F</td>
                            <td>152265.55</td>
                            <td>3876.55</td>
                            <td>24913.65</td>
                            <td>473</td>
                            <td colspan="2"></td>
                        </tr>

                        <tr>
                            <td class="fw-bold">To Date A-G</td>
                            <td>170707.67</td>
                            <td>11099.29</td>
                            <td>45829.1</td>
                            <td>831.6</td>
                            <td colspan="2"></td>
                        </tr>

                        <tr>
                            <td class="fw-bold">To Date A-H</td>
                            <td>187121.17</td>
                            <td>28767.9</td>
                            <td>67154.22</td>
                            <td>1613.36</td>
                            <td colspan="2"></td>
                        </tr>

                        <tr>
                            <td class="fw-bold">To Date A-I</td>
                            <td>255637.14</td>
                            <td>292949.04</td>
                            <td>205299.2</td>
                            <td>2403.55</td>
                            <td colspan="2"></td>
                        </tr>
                    </tbody>
                </table>
            </div>

            <!-- Buttons -->
            <div class="text-end mt-3">
                <button class="btn btn-success btn-sm">Calculate Now</button>
            </div>

            <div class="d-flex justify-content-center gap-2 flex-wrap mt-4">
                <button class="btn btn-outline-primary btn-sm">Save</button>
                <button class="btn btn-outline-secondary btn-sm">Back</button>
                <button class="btn btn-outline-info btn-sm">Raw Mat Cons</button>
                <button class="btn btn-outline-warning btn-sm">Prod Details</button>
                <button class="btn btn-outline-dark btn-sm">HM Distribution</button>
                <button class="btn btn-outline-danger btn-sm">Delay Details</button>
            </div>

        </div>
    </div>
</div>

</body>
</html>