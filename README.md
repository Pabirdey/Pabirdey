<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Find Lot No</title>

    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">

    <style>
        body {
            background-color: #f2f2f2;
            padding: 30px;
        }

        /* Medium modal width (Oracle Forms style) */
        .modal-medium {
            max-width: 350px;
        }

        .list-group-item.active {
            background-color: #0d6efd;
            border-color: #0d6efd;
        }
    </style>
</head>
<body>

<!-- Open button -->
<button class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#findModal">
    Find Lot No
</button>

<!-- Modal -->
<div class="modal fade" id="findModal" tabindex="-1">
    <div class="modal-dialog modal-medium modal-dialog-centered">
        <div class="modal-content">

            <!-- Header -->
            <div class="modal-header bg-dark text-white py-2">
                <h6 class="modal-title">Find</h6>
                <button type="button" class="btn-close btn-close-white" data-bs-dismiss="modal"></button>
            </div>

            <!-- Body -->
            <div class="modal-body">

                <!-- Find textbox -->
                <div class="mb-2">
                    <label class="fw-bold">Find</label>
                    <input type="text" id="searchLot" class="form-control" placeholder="BRL-E/0%">
                </div>

                <!-- List -->
                <div class="border" style="height:165px; overflow-y:auto;">
                    <ul class="list-group list-group-flush" id="lotList">
                        <li class="list-group-item list-group-item-action">BRL-E/08/31</li>
                        <li class="list-group-item list-group-item-action">BRL-E/08/39</li>
                        <li class="list-group-item list-group-item-action">BRL-E/08/40</li>
                        <li class="list-group-item list-group-item-action">BRL-E/08/42</li>
                        <li class="list-group-item list-group-item-action">BRL-E/08/43</li>
                        <li class="list-group-item list-group-item-action">BRL-E/09/01</li>
                        <li class="list-group-item list-group-item-action">BRL-E/09/02</li>
                        <li class="list-group-item list-group-item-action">BRL-E/09/03</li>
                        <li class="list-group-item list-group-item-action">BRL-E/09/04</li>
                    </ul>
                </div>

            </div>

            <!-- Footer -->
            <div class="modal-footer justify-content-center bg-primary py-2">
                <button class="btn btn-light btn-sm" id="btnOk">OK</button>
                <button class="btn btn-light btn-sm" data-bs-dismiss="modal">Cancel</button>
            </div>

        </div>
    </div>
</div>

<!-- Bootstrap JS -->
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>

<!-- Script -->
<script>
    let selectedLot = "";

    // Search filter
    document.getElementById("searchLot").addEventListener("keyup", function () {
        let filter = this.value.toUpperCase();
        let items = document.querySelectorAll("#lotList li");

        items.forEach(item => {
            item.style.display = item.textContent.toUpperCase().includes(filter)
                ? ""
                : "none";
        });
    });

    // Select row
    document.querySelectorAll("#lotList li").forEach(item => {
        item.addEventListener("click", function () {
            document.querySelectorAll("#lotList li").forEach(li => li.classList.remove("active"));
            this.classList.add("active");
            selectedLot = this.textContent;
        });

        // Double click = OK
        item.addEventListener("dblclick", function () {
            selectedLot = this.textContent;
            alert("Selected Lot No: " + selectedLot);
            bootstrap.Modal.getInstance(document.getElementById("findModal")).hide();
        });
    });

    // OK button
    document.getElementById("btnOk").addEventListener("click", function () {
        if (selectedLot === "") {
            alert("Please select a Lot No");
            return;
        }
        alert("Selected Lot No: " + selectedLot);
        bootstrap.Modal.getInstance(document.getElementById("findModal")).hide();
    });
</script>

</body>
</html>
