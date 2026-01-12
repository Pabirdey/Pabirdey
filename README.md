<script>
function toggleList(index) {
    $(".list-box").hide(); // close other lists
    $("#list_" + index).toggle();
}

function selectItem(el, index) {
    $("#clayInput_" + index).val(el.innerText);
    $("#list_" + index).hide();

    if (el.innerText === "OTHERS") {
        alert("OTHERS selected"); // later you can open modal
    }
}

// Close dropdown when clicking outside
document.addEventListener("click", function (e) {
    if (!e.target.closest(".input-wrapper")) {
        $(".list-box").hide();
    }
});
</script>