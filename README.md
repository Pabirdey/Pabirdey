<!DOCTYPE html>
<html>
<head>
    <title>Furnace High Line Log Sheet</title>

    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">

    <style>
        body {
            background: #f4f6f9;
        }

        .header-box {
            background: #0d47a1;
            color: white;
            padding: 10px;
            border-radius: 10px;
        }

        .section-box {
            background: #1976d2;
            color: white;
            padding: 10px;
            border-radius: 10px;
            margin-top: 10px;
        }

        .table input {
            width: 60px;
        }

        textarea {
            height: 120px;
        }
        .card-custom {
            background: linear-gradient(to right, #0d47a1, #1976d2);
            border-radius: 20px;
            padding: 20px;
            color: white;
        }

        .table-custom {
            background-color: white;
            border-radius: 10px;
            overflow: hidden;
        }

        .table-custom th {
            background-color: #1565c0;
            color: white;
            text-align: center;
            font-size: 14px;
        }

        .table-custom td {
            text-align: center;
            font-size: 13px;
            padding: 6px;
        }

        .table-custom td:hover {
            background-color: #e3f2fd;
            cursor: pointer;
        }

        .material-name {
            font-weight: bold;
            background-color: #e3f2fd;
        }

        .btn-custom {
            width: 120px;
            border-radius: 25px;
        }

        .table-container {
            max-height: 400px;
            overflow-y: auto;
        }
    </style>
</head>

<body>

<div class="container-fluid mt-3">

    <!-- HEADER -->
    <div class="header-box d-flex justify-content-between align-items-center">
        <h4 class="m-0">FURNACE HIGH LINE LOG SHEET</h4>
        <div class="d-flex gap-2">
            <input type="datetime-local" class="form-control">
            <select class="form-select">
                <option>Shift A</option>
                <option>Shift B</option>
                <option>Shift C</option>
            </select>
        </div>
    </div>

    <!-- TABS -->
    <ul class="nav nav-tabs mt-3">
        <li class="nav-item">
            <a class="nav-link active" data-bs-toggle="tab" href="#tab1">Coke Unloading</a>
        </li>
        <li class="nav-item">
            <a class="nav-link" data-bs-toggle="tab" href="#tab2">High Line Log</a>
        </li>
        <li class="nav-item">
            <a class="nav-link" data-bs-toggle="tab" href="#tab3">Bin Position</a>
        </li>      
    </ul>

    <!-- TAB CONTENT -->
    <div class="tab-content">

        <!-- TAB 1 -->
        <div class="tab-pane fade show active" id="tab1">
            <div class="row mt-2">
                <!-- LEFT TABLE -->
                <div class="col-md-8">
                    <div class="section-box">
                        <h6>Coke Unloading</h6>
                        <div class="table-responsive">
                            <table class="table table-bordered text-center bg-white">
                                <thead>
                                    <tr style="font-family:'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;font-size: 12px;">
                                        <th style="width:40px;">Date</th>
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
                </div>

                <!-- RIGHT SIDE -->
                <div class="col-md-4">
                    <div class="row">
                        <!-- Others -->
                        <div class="col-md-6">
                            <div class="section-box">
                                <h6>Others</h6>
                                <label style="word-wrap:break-word;">Stock Coke in Eastern Bunker</label>
                                <input class="form-control mb-2">
                                <label>Stock Coke in Western Bunker</label>
                                <input class="form-control mb-2">
                                <label>Behive Coke in Middle Bunker</label>
                                <input class="form-control mb-2">
                            </div>
                        </div>

                        <!-- Coke & Nut Coke -->
                        <div class="col-md-6">
                            <div class="section-box">
                                <h6>Coke & Nut Coke</h6>
                                <label>Material advised</label>        
                                <input class="form-control mb-2" placeholder="Material advised">
                                <label>Time advised</label>
                                <input class="form-control mb-2" placeholder="Time advised">
                                <label>Material received</label>
                                <input class="form-control mb-2" placeholder="Material received">
                                <label>Time received</label>
                                <input class="form-control mb-2" placeholder="Time received">
                                <label>Unloaded</label>
                                <input class="form-control mb-2" placeholder="Unloaded">
                                <label>Loco left</label>
                                <input class="form-control mb-2" placeholder="Loco left">
                                <label>Sent down</label>
                                <input class="form-control mb-2" placeholder="Sent down">
                                <label>Total</label>
                                <input class="form-control mb-2" placeholder="Total">
                            </div>
                        </div>

                    </div>

                    <!-- Remarks -->
                    <div class="section-box mt-2">
                        <h6>Remarks & Delays</h6>
                        <textarea class="form-control"></textarea>
                    </div>

                </div>

            </div>        
            <div class="tab-pane fade show active" id="tab2">
                <div class="container mt-4">

                    <div class="card-custom">
                
                        <h4 class="text-center mb-4">Raw Material Position</h4>
                
                        <div class="table-container">
                            <table class="table table-bordered table-custom">
                                <thead>
                                    <tr>
                                        <th>Material</th>
                                        <th>Yard</th>
                                        <th>H.L</th>
                                        <th>Stock</th>
                                        <th>A</th>
                                        <th>B</th>
                                        <th>C</th>
                                        <th>D</th>
                                        <th>E</th>
                                        <th>F</th>
                                    </tr>
                                </thead>
                
                                <tbody>
                                    <tr>
                                        <td class="material-name">SINTER</td>
                                        <td>R147</td><td>R148</td><td>R149</td>
                                        <td>R150</td><td>R151</td><td>R152</td>
                                        <td>R153</td><td>R154</td><td>R155</td>
                                    </tr>
                
                                    <tr>
                                        <td class="material-name">TFO</td>
                                        <td>R156</td><td>R157</td><td>R158</td>
                                        <td>R159</td><td>R160</td><td>R161</td>
                                        <td>R162</td><td>R163</td><td>R164</td>
                                    </tr>
                
                                    <tr>
                                        <td class="material-name">LRP</td>
                                        <td>R165</td><td>R166</td><td>R167</td>
                                        <td>R168</td><td>R169</td><td>R170</td>
                                        <td>R171</td><td>R172</td><td>R173</td>
                                    </tr>
                
                                    <tr>
                                        <td class="material-name">JODA</td>
                                        <td>R174</td><td>R175</td><td>R176</td>
                                        <td>R177</td><td>R178</td><td>R179</td>
                                        <td>R180</td><td>R181</td><td>R182</td>
                                    </tr>
                
                                    <tr>
                                        <td class="material-name">PELLET</td>
                                        <td>R383</td><td>R384</td><td>R385</td>
                                        <td>R386</td><td>R387</td><td>R388</td>
                                        <td>R389</td><td>R390</td><td>R391</td>
                                    </tr>
                
                                    <tr>
                                        <td class="material-name">NUT COKE</td>
                                        <td>R192</td><td>R193</td><td>R194</td>
                                        <td>R195</td><td>R196</td><td>R197</td>
                                        <td>R198</td><td>R199</td><td>R200</td>
                                    </tr>
                
                                    <tr>
                                        <td class="material-name">LIMESTONE</td>
                                        <td>R201</td><td>R202</td><td>R203</td>
                                        <td>R204</td><td>R205</td><td>R206</td>
                                        <td>R207</td><td>R208</td><td>R209</td>
                                    </tr>
                
                                    <tr>
                                        <td class="material-name">SCRAP</td>
                                        <td>R228</td><td>R229</td><td>R230</td>
                                        <td>R231</td><td>R232</td><td>R233</td>
                                        <td>R234</td><td>R235</td><td>R236</td>
                                    </tr>
                                </tbody>
                
                            </table>
                        </div>
                
                    </div>
                
                    <!-- Buttons -->
                    <div class="text-center mt-4">
                        <button class="btn btn-success btn-custom">Save</button>
                        <button class="btn btn-danger btn-custom">Delete</button>
                        <button class="btn btn-secondary btn-custom">Exit</button>
                    </div>
                
                </div>
      
      
        </div>

        <!-- OTHER TABS -->
        <div class="tab-pane fade" id="tab2">
            <h5 class="mt-3">High Line Log Content</h5>
        </div>

        <div class="tab-pane fade" id="tab3">
            <h5 class="mt-3">Bin Position Content</h5>
        </div>

        <div class="tab-pane fade" id="tab4">
            <h5 class="mt-3">Unloading Report Content</h5>
        </div>

    </div>

    <!-- FOOTER -->
    <div class="d-flex justify-content-end gap-2 mt-3">
        <button class="btn btn-success">Save</button>
        <button class="btn btn-danger">Delete</button>
        <button class="btn btn-secondary">Exit</button>
    </div>

</div>

<!-- Bootstrap JS -->
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>

<!-- JS FOR ROW GENERATION + TOTAL -->
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

    // Generate 5 rows
    for (let i = 0; i < 5; i++) {
        document.getElementById("tblBody").innerHTML += createRow();
    }

</script>

</body>
</html>
