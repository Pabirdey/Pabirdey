<!DOCTYPE html>
<html>
<head>
    <title>Furnace High Line Log Sheet</title>

    <!-- Bootstrap -->
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

        .small-input {
            width: 100%;
        }

        textarea {
            height: 150px;
        }
    </style>
</head>

<body>

<div class="container-fluid mt-3">
    <!-- HEADER -->
    <div class="header-box d-flex justify-content-between align-items-center">
        <h4><center>FURNACE HIGH LINE LOG SHEET</center></h4>
        <div class="d-flex gap-2">
            <input type="datetime-local" class="form-control">
            <select class="form-select">
                <option>Shift A</option>
                <option>Shift B</option>
                <option>Shift C</option>
            </select>
        </div>
    </div>    
    <ul class="nav nav-tabs mt-3">
        <li class="nav-item"><a class="nav-link active">Coke Unloading</a></li>
        <li class="nav-item"><a class="nav-link">High Line Log</a></li>
        <li class="nav-item"><a class="nav-link">Bin Position</a></li>
        <li class="nav-item"><a class="nav-link">Unloading Report</a></li>
    </ul>
    <!-- MAIN SECTION -->
    <div class="row">        
        <div class="col-md-6">
            <!-- Coke Unloading -->
            <div class="section-box">
                <h6>Coke Unloading</h6>
                <div class="table-responsive">
                    <table class="table table-bordered text-center bg-white">
                        <thead>
                            <tr>
                                <th>Date</th>
                                <th>Shift</th>
                                <th>Bunker Name</th>
                                <th>C-BF</th>
                                <th>E-BF</th>
                                <th>F-BF</th>
                                <th>Total</th>
                                <th>Position</th>
                                <th>Balance</th>
                            </tr>
                        </thead>
                        <tbody id="tblBody">
                            <!-- JS will generate rows -->
                        </tbody>
                    </table>
                </div>
            </div>            
        </div>      
        <div class="col-md-4">      
            <div class="section-box">
                <h6>Others</h6>
                <label>Stock Coke in Eastern Bunker</label>
                <input class="form-control mb-2" placeholder="Eastern Bunker">
                <label>Stock Coke in Western Bunker</label>
                <input class="form-control mb-2" placeholder="Western Bunker">
                <label>Behive Coke in Middle Bunker</label>
                <input class="form-control mb-2" placeholder="Middle Bunker">
            </div>  
            <div class="col-md-4">              
                <div class="section-box">
                    <h6>Coke & Nut Coke advised & Received</h6>
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

            <!-- Remarks -->
            <div class="section-box">
                <h6>Remarks & Delays</h6>
                <textarea class="form-control"></textarea>
            </div>

        </div>
    </div>

    <!-- FOOTER -->
    <div class="d-flex justify-content-end gap-2 mt-3">
        <button class="btn btn-success">Save</button>
        <button class="btn btn-danger">Delete</button>
        <button class="btn btn-secondary">Exit</button>
    </div>

</div>




</body>
</html>
