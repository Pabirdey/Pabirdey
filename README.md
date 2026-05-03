<!DOCTYPE html>
<html>
<head>
    <title>Bunker Mapping</title>

    <!-- Bootstrap -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">

    <style>
        body { padding:20px; background:#f5f5f5; }

        .box {
            background:#0d6efd;
            padding:15px;
            border-radius:10px;
            color:white;
            margin-bottom:20px;
        }

        table input {
            width:70px;
            text-align:center;
        }

        .highlight1 { background: yellow !important; }
        .highlight2 { background: lightgreen !important; }
    </style>
</head>

<body>

<div class="container-fluid">

    <!-- 🔵 TOP TABLE -->
    <div class="box">
        <h5>Coke Unloading</h5>

        <table class="table table-bordered bg-white text-dark" id="topTable">
            <thead>
                <tr>
                    <th>Bunker</th>
                    <th>C-BF</th>
                    <th>E-BF</th>
                    <th>F-BF</th>
                </tr>
            </thead>

            <tbody>
                <tr>
                    <td>
                        <select class="form-select bunker">
                            <option value="">Select</option>
                            <option value="WESTERN">WESTERN</option>
                            <option value="MIDDLE">MIDDLE</option>
                            <option value="EASTERN">EASTERN</option>
                        </select>
                    </td>
                    <td><input class="form-control c-bf"></td>
                    <td><input class="form-control e-bf"></td>
                    <td><input class="form-control f-bf"></td>
                </tr>
            </tbody>
        </table>
    </div>


    <div class="row">

        <!-- 🔵 TONNAGE OF COKE -->
        <div class="col-md-6">
            <div class="box">
                <h5>Tonnage of Coke</h5>

                <table class="table table-bordered bg-white text-dark" id="tblCoke">
                    <tbody>
                        <tr data-bunker="WESTERN">
                            <td>WESTERN</td>
                            <td><input class="form-control c-bf"></td>
                            <td><input class="form-control e-bf"></td>
                            <td><input class="form-control f-bf"></td>
                        </tr>

                        <tr data-bunker="MIDDLE">
                            <td>MIDDLE</td>
                            <td><input class="form-control c-bf"></td>
                            <td><input class="form-control e-bf"></td>
                            <td><input class="form-control f-bf"></td>
                        </tr>

                        <tr data-bunker="EASTERN">
                            <td>EASTERN</td>
                            <td><input class="form-control c-bf"></td>
                            <td><input class="form-control e-bf"></td>
                            <td><input class="form-control f-bf"></td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>


        <!-- 🔵 TONNAGE OF NUT COKE -->
        <div class="col-md-6">
            <div class="box">
                <h5>Tonnage of Nut Coke</h5>

                <table class="table table-bordered bg-white text-dark" id="tblNutCoke">
                    <tbody>
                        <tr data-bunker="WESTERN">
                            <td>WESTERN</td>
                            <td><input class="form-control c-bf"></td>
                            <td><input class="form-control e-bf"></td>
                            <td><input class="form-control f-bf"></td>
                        </tr>

                        <tr data-bunker="MIDDLE">
                            <td>MIDDLE</td>
                            <td><input class="form-control c-bf"></td>
                            <td><input class="form-control e-bf"></td>
                            <td><input class="form-control f-bf"></td>
                        </tr>

                        <tr data-bunker="EASTERN">
                            <td>EASTERN</td>
                            <td><input class="form-control c-bf"></td>
                            <td><input class="form-control e-bf"></td>
                            <td><input class="form-control f-bf"></td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>

    </div>

</div>


<!-- 🔥 JAVASCRIPT -->
<script>

document.querySelectorAll(".bunker").forEach(drop => {

    drop.addEventListener("change", function () {

        let selected = this.value;

        // ❌ remove old highlight
        document.querySelectorAll("#tblCoke tr, #tblNutCoke tr").forEach(tr => {
            tr.classList.remove("highlight1", "highlight2");
        });

        // ✅ find rows
        let cokeRow = document.querySelector(`#tblCoke tr[data-bunker='${selected}']`);
        let nutRow  = document.querySelector(`#tblNutCoke tr[data-bunker='${selected}']`);

        // ✅ highlight
        if (cokeRow) cokeRow.classList.add("highlight1");
        if (nutRow)  nutRow.classList.add("highlight2");

        // ✅ copy values from top row
        let row = this.closest("tr");

        let c = row.querySelector(".c-bf").value || "";
        let e = row.querySelector(".e-bf").value || "";
        let f = row.querySelector(".f-bf").value || "";

        if (cokeRow) {
            cokeRow.querySelector(".c-bf").value = c;
            cokeRow.querySelector(".e-bf").value = e;
            cokeRow.querySelector(".f-bf").value = f;
        }

        if (nutRow) {
            nutRow.querySelector(".c-bf").value = c;
            nutRow.querySelector(".e-bf").value = e;
            nutRow.querySelector(".f-bf").value = f;
        }

        // ✅ focus first matched input
        if (cokeRow) {
            let input = cokeRow.querySelector("input");
            if (input) input.focus();
        }

    });

});

</script>

</body>
</html>