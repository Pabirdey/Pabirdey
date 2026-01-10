<div class="modal fade" id="clayModal" tabindex="-1">
    <div class="modal-dialog modal-md modal-dialog-centered">
        <div class="modal-content">

            <div class="modal-header bg-primary text-white">
                <h5 class="modal-title w-100 text-center">MG_CLAY</h5>
                <button type="button" class="btn-close btn-close-white" data-bs-dismiss="modal"></button>
            </div>

            <div class="modal-body">
                <div class="fw-bold text-center mb-3">Weightage of Clay</div>

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
<script>
function toggleList(index) {
    var list = document.getElementById("list_" + index);
    list.style.display = (list.style.display === "block") ? "none" : "block";
}

function selectItem(el, index) {

    document.getElementById("clayInput_" + index).value = el.innerText;
    document.getElementById("list_" + index).style.display = "none";

    // 🔥 WHEN OTHERS CLICKED → OPEN MODAL
    if (el.innerText.trim() === "OTHERS") {

        // store row index if needed later
        window.currentRowIndex = index;

        // open bootstrap modal
        var clayModal = new bootstrap.Modal(
            document.getElementById('clayModal')
        );
        clayModal.show();
    }
}

// Close list when clicking outside
document.addEventListener("click", function (e) {
    if (!e.target.closest(".input-wrapper") &&
        !e.target.closest(".list-box")) {

        document.querySelectorAll(".list-box").forEach(function (l) {
            l.style.display = "none";
        });
    }
});
</script>
<script>
function saveClay() {

    let c1 = document.getElementById("clay1").value;
    let c2 = document.getElementById("clay2").value;
    let c3 = document.getElementById("clay3").value;

    alert(
        "Row Index : " + window.currentRowIndex +
        "\nClay1: " + c1 +
        "\nClay2: " + c2 +
        "\nClay3: " + c3
    );

    // close modal
    bootstrap.Modal.getInstance(
        document.getElementById('clayModal')
    ).hide();
}
</script>
