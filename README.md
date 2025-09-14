<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MTO System</title>
    <!-- Bootstrap 5 CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <!-- Bootstrap Icons -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.10.0/font/bootstrap-icons.css">
    <style>
        body {
            background-color: #f8f9fa;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        .header {
            background-color: #2c3e50;
            color: white;
            padding: 10px 0;
        }
        .system-title {
            font-weight: bold;
            font-size: 1.5rem;
        }
        .datetime {
            font-size: 1.2rem;
            text-align: right;
        }
        .card {
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            margin-bottom: 20px;
            border: none;
        }
        .card-header {
            background-color: #34495e;
            color: white;
            font-weight: bold;
        }
        .btn-primary {
            background-color: #3498db;
            border: none;
        }
        .btn-primary:hover {
            background-color: #2980b9;
        }
        .btn-outline-primary {
            color: #3498db;
            border-color: #3498db;
        }
        .btn-outline-primary:hover {
            background-color: #3498db;
            color: white;
        }
        .table th {
            background-color: #ecf0f1;
        }
        .nav-tabs .nav-link.active {
            font-weight: bold;
            border-bottom: 3px solid #3498db;
        }
        .analysis-table {
            font-size: 0.85rem;
        }
        .status-indicator {
            width: 12px;
            height: 12px;
            border-radius: 50%;
            display: inline-block;
            margin-right: 5px;
        }
        .status-active {
            background-color: #2ecc71;
        }
        .status-inactive {
            background-color: #e74c3c;
        }
        @media (max-width: 992px) {
            .table-responsive {
                font-size: 0.8rem;
            }
        }
    </style>
</head>
<body>
    <div class="header">
        <div class="container">
            <div class="row align-items-center">
                <div class="col-md-6">
                    <div class="system-title">MTO System</div>
                </div>
                <div class="col-md-6 datetime">
                    <div>Y 04:08:22</div>
                    <div>Date: 14-SEP-2025 | Furnace: |H| | Shift: |A|</div>
                </div>
            </div>
        </div>
    </div>

    <div class="container mt-4">
        <div class="row">
            <div class="col-md-12">
                <div class="card">
                    <div class="card-header d-flex justify-content-between align-items-center">
                        <span>Control Panel</span>
                    </div>
                    <div class="card-body">
                        <div class="d-flex flex-wrap gap-2">
                            <button class="btn btn-primary"><i class="bi bi-info-circle"></i> Trough Details</button>
                            <button class="btn btn-outline-primary"><i class="bi bi-water"></i> Liquid-Level</button>
                            <button class="btn btn-outline-primary"><i class="bi bi-arrow-repeat"></i> Refresh All</button>
                            <button class="btn btn-outline-primary"><i class="bi bi-house-door"></i> Cast House</button>
                            <button class="btn btn-outline-danger"><i class="bi bi-box-arrow-right"></i> Exit</button>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <div class="row">
            <div class="col-md-12">
                <div class="card">
                    <div class="card-header">
                        Casting Operations
                    </div>
                    <div class="card-body">
                        <div class="table-responsive">
                            <table class="table table-bordered table-hover table-sm">
                                <thead class="table-light">
                                    <tr>
                                        <th>Cast No.</th>
                                        <th>Trough</th>
                                        <th>Start</th>
                                        <th>End</th>
                                        <th>Lade No.</th>
                                        <th>Place time</th>
                                        <th>Lasts</th>
                                        <th>Filling start</th>
                                        <th>Fat Stains</th>
                                        <th>Stag & Time</th>
                                        <th>Dedu</th>
                                        <th>Gross</th>
                                        <th>Tare</th>
                                        <th>Net</th>
                                        <th>Lade Filling Rate</th>
                                        <th>HMT</th>
                                        <th>Reason For Change</th>
                                        <th>Wastes Range</th>
                                        <th>Remark</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr>
                                        <td>9722</td>
                                        <td>I</td>
                                        <td>01:50</td>
                                        <td></td>
                                        <td>39</td>
                                        <td>03:52</td>
                                        <td>01:50</td>
                                        <td>03:55</td>
                                        <td>1</td>
                                        <td>01:56</td>
                                        <td>LD2</td>
                                        <td>S61</td>
                                        <td>303</td>
                                        <td>278</td>
                                        <td>3.70</td>
                                        <td>1462</td>
                                        <td>0</td>
                                        <td></td>
                                        <td>Remark</td>
                                    </tr>
                                    <tr>
                                        <td>67973</td>
                                        <td>I</td>
                                        <td>01:50</td>
                                        <td></td>
                                        <td>44</td>
                                        <td>02:20</td>
                                        <td>03:55</td>
                                        <td>1</td>
                                        <td>01:56</td>
                                        <td></td>
                                        <td></td>
                                        <td></td>
                                        <td></td>
                                        <td></td>
                                        <td></td>
                                        <td></td>
                                        <td></td>
                                        <td>Remark</td>
                                    </tr>
                                    <tr>
                                        <td>67974</td>
                                        <td>I</td>
                                        <td>01:50</td>
                                        <td></td>
                                        <td>24</td>
                                        <td>03:36</td>
                                        <td>1</td>
                                        <td>01:56</td>
                                        <td></td>
                                        <td></td>
                                        <td></td>
                                        <td></td>
                                        <td></td>
                                        <td></td>
                                        <td></td>
                                        <td></td>
                                        <td></td>
                                        <td>Remark</td>
                                    </tr>
                                    <tr>
                                        <td>67974</td>
                                        <td>I</td>
                                        <td>03:35</td>
                                        <td></td>
                                        <td>18</td>
                                        <td>03:37</td>
                                        <td>03:35</td>
                                        <td></td>
                                        <td></td>
                                        <td></td>
                                        <td></td>
                                        <td></td>
                                        <td></td>
                                        <td></td>
                                        <td></td>
                                        <td></td>
                                        <td></td>
                                        <td>Remark</td>
                                    </tr>
                                    <tr>
                                        <td>67974</td>
                                        <td>I</td>
                                        <td>03:35</td>
                                        <td></td>
                                        <td>42</td>
                                        <td>03:00</td>
                                        <td></td>
                                        <td></td>
                                        <td></td>
                                        <td></td>
                                        <td></td>
                                        <td></td>
                                        <td></td>
                                        <td></td>
                                        <td></td>
                                        <td></td>
                                        <td></td>
                                        <td>Remark</td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <div class="row">
            <div class="col-md-12">
                <div class="card">
                    <div class="card-header">
                        <ul class="nav nav-tabs card-header-tabs">
                            <li class="nav-item">
                                <a class="nav-link active" href="#hot-metal" data-bs-toggle="tab">Hot Metal Analysis</a>
                            </li>
                            <li class="nav-item">
                                <a class="nav-link" href="#slag" data-bs-toggle="tab">Slag Analysis</a>
                            </li>
                        </ul>
                    </div>
                    <div class="card-body">
                        <div class="tab-content">
                            <div class="tab-pane fade show active" id="hot-metal">
                                <div class="d-flex justify-content-between align-items-center mb-3">
                                    <h5 class="mb-0">Avg. HMT: 1484</h5>
                                </div>
                                <div class="table-responsive">
                                    <table class="table table-bordered analysis-table">
                                        <thead class="table-light">
                                            <tr>
                                                <th>Cast No.</th>
                                                <th>C</th>
                                                <th>Si</th>
                                                <th>Mn</th>
                                                <th>P</th>
                                                <th>S</th>
                                                <th>Ti</th>
                                                <th>Cr</th>
                                                <th>Cu</th>
                                                <th>Ni</th>
                                                <th>Mo</th>
                                                <th>V</th>
                                                <th>Nb</th>
                                                <th>Sn</th>
                                                <th>B</th>
                                                <th>Pb</th>
                                                <th>As</th>
                                                <th>Sb</th>
                                                <th>Bi</th>
                                                <th>Ca</th>
                                                <th>Al</th>
                                                <th>Zn</th>
                                                <th>Mg</th>
                                                <th>Co</th>
                                                <th>W</th>
                                                <th>Ce</th>
                                                <th>La</th>
                                                <th>Temperature</th>
                                            </tr>
                                        </thead>
                                        <tbody>
                                            <tr>
                                                <td>9722</td>
                                                <td>4.21</td>
                                                <td>0.38</td>
                                                <td>0.21</td>
                                                <td>0.087</td>
                                                <td>0.025</td>
                                                <td>0.012</td>
                                                <td>0.034</td>
                                                <td>0.078</td>
                                                <td>0.032</td>
                                                <td>0.005</td>
                                                <td>0.004</td>
                                                <td>0.001</td>
                                                <td>0.008</td>
                                                <td>0.0001</td>
                                                <td>0.0002</td>
                                                <td>0.0003</td>
                                                <td>0.0004</td>
                                                <td>0.0005</td>
                                                <td>0.0021</td>
                                                <td>0.0042</td>
                                                <td>0.0006</td>
                                                <td>0.0007</td>
                                                <td>0.0008</td>
                                                <td>0.0009</td>
                                                <td>0.0001</td>
                                                <td>0.0001</td>
                                                <td>1482°C</td>
                                            </tr>
                                        </tbody>
                                    </table>
                                </div>
                            </div>
                            <div class="tab-pane fade" id="slag">
                                <p class="text-center py-4">Slag analysis data will be displayed here.</p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Bootstrap JS and Popper.js -->
    <script src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.11.6/dist/umd/popper.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.min.js"></script>
</body>
</html>