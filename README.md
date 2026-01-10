<script>
let currentClayRowIndex = null;

// OPEN / CLOSE LIST
function toggleList(index, event) {
    event.stopPropagation();

    document.querySelectorAll(".list-box").forEach(l => l.style.display = "none");

    document.getElementById("list_" + index).style.display = "block";
}

// ITEM CLICK
function selectItem(el, index, event) {
    event.stopPropagation();

    let value = el.innerText.trim();

    document.getElementById("clayInput_" + index).value = value;
    document.getElementById("list_" + index).style.display = "none";

    if (value === "OTHERS") {
        currentClayRowIndex = index;

        clay1.value = "";
        clay2.value = "";
        clay3.value = "";

        new bootstrap.Modal(document.getElementById("clayModal")).show();
    }
}

// SAVE MODAL DATA
function saveClay() {

    let c1 = clay1.value;
    let c2 = clay2.value;
    let c3 = clay3.value;

    if (!c1 && !c2 && !c3) {
        alert("Select at least one clay");
        return;
    }

    let result = [c1, c2, c3].filter(x => x).join(" + ");

    document.getElementById("clayInput_" + currentClayRowIndex).value = result;

    bootstrap.Modal.getInstance(document.getElementById("clayModal")).hide();
}

// CLICK OUTSIDE CLOSE
document.addEventListener("click", function () {
    document.querySelectorAll(".list-box").forEach(l => l.style.display = "none");
});
</script>

</body>
</html>
