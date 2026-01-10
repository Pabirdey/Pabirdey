<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Clay Weightage</title>

    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">

    <style>
        body {
            background: #f4f6f9;
            padding: 40px;
        }

        .modal-content {
            border-radius: 25px;
            border: none;
        }

        .modal-header {
            background: #0d6efd;
            color: #fff;
            border-radius: 25px 25px 0 0;
        }

        .title-box {
            background: #0d6efd;
            color: white;
            padding: 10px 25px;
            border-radius: 30px;
            text-align: center;
            font-size: 18px;
            font-weight: 600;
            margin-bottom: 20px;
        }

        .clay-box {
            background: #0d6efd;
            border-radius: 25px;
            padding: 20px;
            color: white;
        }

        .clay-label {
            font-weight: 600;
        }

        .clay-input {
            border-radius: 10px;
        }

        .btn-save {
            background: #198754;
            color: white;
            padding: 8px 30px;
            border-radius: 20px;
        }

        .btn-exit {
            background: #dc3545;
            color: white;
            padding: 8px 30px;
            border-radius: 20px;
        }
    </style>
</head>
<body>

<button class="btn btn-primary btn-md" data-bs-toggle="modal" data-bs-target="#clayModal">
    Open Clay Weightage
</button>

<div class="modal fade" id="clayModal" tabindex="-1">
    <div class="modal-dialog modal-md modal-dialog-centered">
        <div class="modal-content">

            <!-- HEADER -->
            <div class="modal-header">
                <h5 class="modal-title w-100 text-center">MG_CLAY</h5>
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
                            <select class="form-select clay-input" id="clay1">
                                <option value="">-- Select Clay1 --</option>
                                <option value="CLAY_A">Clay A</option>
                                <option value="CLAY_B">Clay B</option>
                                <option value="CLAY_C">Clay C</option>
                            </select>
                        </div>
                        <div class="col-3">
                            <select class="form-select clay-input">
                                <option></option>
                                <option></option>
                            </select>
                        </div>
                    </div>

                    <!-- Clay 2 -->
                    <div class="row align-items-center mb-3">
                        <div class="col-2 clay-label">Clay2</div>
                        <div class="col-7">
                            <!-- <input type="text" class="form-control clay-input" id="clay2"> -->
                             <select class="form-select clay-input" id="clay2">
                                <option value="">-- Select Clay2 --</option>
                                <option value="CLAY_A">Clay A</option>
                                <option value="CLAY_B">Clay B</option>
                                <option value="CLAY_C">Clay C</option>
                            </select>
                        </div>
                        <div class="col-3">
                            <select class="form-select clay-input">
                                <option></option>
                                <option></option>
                            </select>
                        </div>
                    </div>

                    <!-- Clay 3 -->
                    <div class="row align-items-center">
                        <div class="col-2 clay-label">Clay3</div>
                        <div class="col-7">
                            <!-- <input type="text" class="form-control clay-input" id="clay3"> -->
                             <select class="form-select clay-input" id="clay3">
                                <option value="">-- Select Clay3 --</option>
                                <option value="CLAY_A">Clay A</option>
                                <option value="CLAY_B">Clay B</option>
                                <option value="CLAY_C">Clay C</option>
                            </select>
                        </div>
                        <div class="col-3">
                            <select class="form-select clay-input">
                                <option></option>
                                <option></option>
                            </select>
                        </div>
                    </div>

                </div>

            </div>

            <!-- FOOTER -->
            <div class="modal-footer justify-content-center">
                <button class="btn btn-save" onclick="saveData()">Save</button>
                <button class="btn btn-exit" data-bs-dismiss="modal">Exit</button>
            </div>

        </div>
    </div>
</div>

<!-- Bootstrap JS -->
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>

<script>
    function saveData() {
        alert(
            "Clay1: " + document.getElementById("clay1").value +
            "\nClay2: " + document.getElementById("clay2").value +
            "\nClay3: " + document.getElementById("clay3").value
        );
    }
</script>

</body>
</html>
