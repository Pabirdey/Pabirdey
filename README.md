<!DOCTYPE html>
<html lang="en">
<head>
    <title>Cast House Details</title>

    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">

    <style>
        .input-wrapper {
            display: flex;
            border: 1px solid #999;
            position: relative;
        }

        .input-wrapper input {
            border: none;
            outline: none;
            width: 100%;
        }

        .arrow-btn {
            width: 30px;
            text-align: center;
            cursor: pointer;
            background: #f0f0f0;
        }

        .list-box {
            border: 1px solid #999;
            display: none;
            background: #fff;
            position: absolute;
            top: 100%;
            left: 0;
            width: 100%;
            z-index: 999;
        }

        .list-box div {
            padding: 6px;
            cursor: pointer;
        }

        .list-box div:hover {
            background: #e6e6e6;
        }
    </style>
</head>

<body>

<div class="container mt-3">

    <h3 class="text-center">Mudgun Details</h3>

    <table class="table table-bordered" id="Mudgun_Details">
        <thead>
            <tr>
                <th>Cast No</th>
                <th>MG Clay Type</th>
            </tr>
        </thead>
        <tbody></tbody>
    </table>
</div>

<!-- ================= MODAL ================= -->
<div class="modal fade" id="clayModal" tabindex="-1">
    <div class="modal-dialog modal-md modal-dialog-centered">
        <div class="modal-content">

            <div class="modal-header bg-primary text-white">
                <h5 class="modal-title w-100 text-center">MG CLAY DETAILS</h5>
                <button type="button" class="btn-close btn-close-white" data-bs-dismiss="modal"></button>
            </div>

            <div class="modal-body">

                <div class="row mb-2">
                    <div class="col-3">Clay1</div>
                    <div class="col-9">
                        <select class="form-select" id="clay1">
                            <option value="">Select</option>
                            <option>Clay A</option>
                            <option>Clay B</option>
                            <option>Clay C</option>
                        </select>
                    </div>
                </div>

                <div class="row mb-2">
                    <div class="col-3">Clay2</div>
                    <div class="col-9">
                        <select class="form-select" id="clay2">
                            <option value="">Select</option>
                            <option>Clay A</option>
                            <option>Clay B</option>
                            <option>Clay C</option>
                        </select>
                    </div>
                </div>

                <div class="row">
                    <div class="col-3">Clay3</div>
                    <div class="col-9">
                        <select class="form-select" id="clay3">
                            <option value="">Select</option>
                            <option>Clay A</option>
                            <option>Clay B</option>
                            <option>Clay C</option>
                        </select>
                    </div>
                </div>

            </div>

            <div class="modal-footer justify-content-center">
                <button class="btn btn-success" onclick="saveClay()">Save</button>
                <button class="btn btn-danger" data-bs-dismiss="modal">Exit</button>
            </div>

        </div>
    </div>
</div>

<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
