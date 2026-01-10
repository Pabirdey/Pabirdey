function selectItem(el, rowIndex) {

    var value = el.innerText.trim();
    var input = document.getElementById("clayInput_" + rowIndex);

    // Set value in textbox
    input.value = value;

    // Hide list
    document.getElementById("list_" + rowIndex).style.display = "none";

    // 🔥 IF OTHERS CLICKED → OPEN MODAL
    if (value === "OTHERS") {
        var modal = new bootstrap.Modal(document.getElementById('clayModal'));
        modal.show();
    }
}
