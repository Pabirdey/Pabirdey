<script>
function toggleList(index) {
    var list = document.getElementById("list_" + index);
    list.style.display = (list.style.display === "block") ? "none" : "block";
}

function selectItem(el, index) {
    document.getElementById("clayInput_" + index).value = el.innerText;
    document.getElementById("list_" + index).style.display = "none";

    // OPTIONAL: if OTHERS clicked
    if (el.innerText === "OTHERS") {
        // open modal / show textbox / anything
        console.log("OTHERS selected at row:", index);
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
