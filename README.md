<!DOCTYPE html>
<html>
<head>
    <title>Furnace High Line Log Sheet</title>

    <!-- Bootstrap -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">

    <style>
        body {
            background: #f4f6f9;
            font-family: Verdana;
            font-size: 12px;
            transform: scale(0.99);
            transform-origin: top left;
        }

        .container-fluid {
            max-width: 1600px;
        }

        /* HEADER */
        .header-box {
            background: #0d47a1;
            color: white;
            padding: 6px;
            border-radius: 6px;
        }

        .header-box h4 {
            font-size: 16px;
        }

        /* SECTION */
        .section-box {
            background: #1976d2;
            color: white;
            padding: 6px;
            border-radius: 6px;
            margin-top: 6px;
        }

        .section-title {
            font-size: 13px;
            font-weight: 600;
            margin-bottom: 4px;
        }

        /* TABLE */
        .table th {
            background: #1565c0;
            color: white;
            font-size: 11px;
            padding: 3px;
        }

        .table td {
            background: white;
            color: black;
            font-size: 11px;
            padding: 3px;
        }

        /* SMALL INPUT (Tab 1 & 2) */
        .table input,
        .table select {
            width: 100%;
            font-size: 8px;
            height: 24px;
            text-align: center;
        }

        /* ✅ MEDIUM INPUT ONLY FOR RAW MATERIAL TAB */
        .table-container input {
            height: 25px;
            font-size: 12px;
            border-radius: 6px;
            padding: 5px;
        }

        .table-custom td {
            vertical-align: middle;
        }

        textarea {
            height: 40px;
            font-size: 11px;
        }

        .form-control,
        .form-select {
            font-size: 12px;
            height: 28px;
        }

        .card-custom {
            background: linear-gradient(to right, #0d47a1, #1976d2);
            border-radius: 20px;
            padding: 10px;
            color: white;
        }

        /* TABS */
        .nav-tabs {
            border-bottom: 2px solid #1976d2;
        }

        .nav-tabs .nav-link {
            color: #1565c0;
            font-weight: 600;
            border-radius: 8px 8px 0 0;
            margin-right: 5px;
            background: #e3f2fd;
        }

        .nav-tabs .nav-link.active {
            background: linear-gradient(to right, #0d47a1, #1976d2);
            color: white !important;
        }

        .tab-pane {
            animation: fadeIn 0.3s ease-in-out;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(5px); }
            to { opacity: 1; transform: translateY(0); }
        }
    </style>

</head>

<body>

<div class="container-fluid mt-2">

    <!-- HEADER -->
    <div class="header-box position-relative d-flex align-items-center">

        <!-- CENTER TITLE -->
        <h4 class="m-0 position-absolute start-50 translate-middle-x">
            Furnace High Line Log Sheet
        </h4>

        <!-- RIGHT SIDE -->
        <div class="ms-auto d-flex gap-2">
            <input type="datetime-local" class="form-control">
            <select class="form-select">
                <option>A</option>
                <option>B</option>
                <option>C</option>
            </select>
        </div>

    </div>

    <!-- TABS -->
    <ul class="nav nav-tabs mt-2">
        <li class="nav-item">
            <a class="nav-link active" data-bs-toggle="tab" href="#tab1">🔥 Coke Unloading</a>
        </li>
        <li class="nav-item">
            <a class="nav-link" data-bs-toggle="tab" href="#tab2">📊 HighLine Log</a>
        </li>
        <li class="nav-item">
            <a class="nav-link" data-bs-toggle="tab" href="#tab3">📦 Bin Position</a>
        </li>
    </ul>

    <!-- TAB CONTENT -->
    <div class="tab-content">

        <!-- TAB 1 -->
        <div class="tab-pane fade show active" id="tab1">
            <div class="row mt-2">

                <div class="col-md-8">
                    <div class="section-box">
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
                </div>

                <div class="col-md-4">
                    <div class="section-box">
                        <div class="section-title">Remarks</div>
                        <textarea class="form-control"></textarea>
                    </div>
                </div>

            </div>
        </div>

        <!-- TAB 2 -->
        <div class="tab-pane fade" id="tab2">
            <div class="section-box mt-2">
                <div class="section-title">High Line Log</div>

                <table class="table table-bordered text-center">
                    <thead>
                        <tr>
                            <th>Material</th>
                            <th>Recd</th>
                            <th>Retd</th>
                            <th>Reason</th>
                            <th>U/L</th>
                            <th>Balance</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td>LRP</td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                            <td><input class="form-control"></td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>

        <!-- TAB 3 -->
        <div class="tab-pane fade" id="tab3">
            <div class="container mt-4">
                <div class="card-custom">
                    <h4 class="text-center mb-4" style="font-size:32px;">Raw Material Position</h4>
                    <div class="table-container">
                        <table class="table table-bordered table-custom">
                            <thead>
                                <tr>
                                    <th>Material</th>
                                    <th>Yard Position</th>
                                    <th>H.L. Position</th>
                                    <th>Stock Loaded</th>
                                    <th>C-BF</th>
                                    <th>E-BF</th>
                                    <th>F-BF</th>                                    
                                </tr>
                            </thead>

                            <tbody>
                                <tr>
                                    <td class="material-name">SINTER</td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>                                    
                                </tr>                            
                                <tr>
                                    <td class="material-name">TFO</td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>                                    
                                </tr>
                                <tr>
                                    <td class="material-name">LRP</td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>                                    
                                </tr>
                            <tr>
                                <td class="material-name">JODA</td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>                                
                            </tr>
                            <tr>
                                <td class="material-name">Pellet</td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>                                
                            </tr>
                            <tr>
                                <td class="material-name">Nut Coke</td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>                                
                            </tr>
                            <tr>
                                <td class="material-name">Limestone</td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                            </tr>
                            <tr>
                                <td class="material-name">Pyroxinite</td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                            </tr>
                            <tr>
                                <td class="material-name">ORT</td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>                                
                            </tr>
                            <tr>
                                <td class="material-name">Scrap</td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                            </tr>
                            <tr>
                               <td class="material-name">Coke(On Stock)</td> 
                               <td><input type="text" class="form-control"></td>
                               <td><input type="text" class="form-control"></td>
                               <td><input type="text" class="form-control"></td>
                               <td><input type="text" class="form-control"></td>
                               <td><input type="text" class="form-control"></td>
                               <td><input type="text" class="form-control"></td>
                            </tr>
                            <tr>
                                <td class="material-name">Low Ash Coke</td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                            </tr>
                            <tr>
                                <td class="material-name">High Ash Coke</td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                            </tr>
                        </tbody>
                        </table>
                    </div>

                </div>                
            </div>
            <div class="text-end mt-3">
                <button class="btn btn-success px-4" onclick="saveRawMaterial()">
                    💾 Save
                </button>
            </div>
            
        </div>

    </div>
</div>

<!-- Bootstrap JS -->
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>

<script>
function createRow() {
    return `
    <tr>
        <td><input type="date" class="form-control"></td>
        <td>
            <select class="form-control">
                <option>A</option>
                <option>B</option>
                <option>C</option>
            </select>
        </td>
        <td><input class="form-control"></td>
        <td><input class="form-control c" oninput="calcTotal(this)"></td>
        <td><input class="form-control e" oninput="calcTotal(this)"></td>
        <td><input class="form-control f" oninput="calcTotal(this)"></td>
        <td><input class="form-control total" readonly></td>
        <td><input class="form-control"></td>
        <td><input class="form-control"></td>
    </tr>`;
}

function calcTotal(el) {
    var row = el.closest("tr");

    var c = parseFloat(row.querySelector(".c").value) || 0;
    var e = parseFloat(row.querySelector(".e").value) || 0;
    var f = parseFloat(row.querySelector(".f").value) || 0;

    row.querySelector(".total").value = c + e + f;
}

// Generate rows
for (let i = 0; i < 5; i++) {
    document.getElementById("tblBody").innerHTML += createRow();
}
</script>

</body>
</html>
