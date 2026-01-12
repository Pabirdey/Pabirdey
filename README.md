<script>
var activeRowIndex = null;

function toggleList(index) {
    var list = document.getElementById("list_" + index);
    list.style.display = (list.style.display === "block") ? "none" : "block";
}

function selectItem(el, index) {

    document.getElementById("clayInput_" + index).value = el.innerText;
    document.getElementById("list_" + index).style.display = "none";

    // ✅ IF OTHERS → OPEN MODAL
    if (el.innerText.trim() === "OTHERS") {

        activeRowIndex = index;   // store row index (important)

        var modal = new bootstrap.Modal(
            document.getElementById("clayModal")
        );
        modal.show();             // ✅ THIS OPENS MODAL
    }
}

// Close all lists when clicking outside
document.addEventListener("click", function (e) {
    if (!e.target.closest(".input-wrapper") &&
        !e.target.closest(".list-box")) {

        document.querySelectorAll(".list-box").forEach(function (l) {
            l.style.display = "none";
        });
    }
});
</script>
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>
