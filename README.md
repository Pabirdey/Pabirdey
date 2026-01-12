<script>
    // store which row opened the modal
    var activeRowIndex = null;

    // open / close dropdown list
    function toggleList(index) {
        $(".list-box").hide();            // close other lists
        $("#list_" + index).toggle();     // toggle current
    }

    // list item click
    function selectItem(el, index) {
        var selectedValue = el.innerText.trim();

        // set value to textbox
        $("#clayInput_" + index).val(selectedValue);

        // close list
        $("#list_" + index).hide();

        // 👉 IF OTHERS CLICKED → OPEN MODAL
        if (selectedValue === "OTHERS") {
            activeRowIndex = index;

            var modal = new bootstrap.Modal(
                document.getElementById("clayModal")
            );
            modal.show();
        }
    }

    // close dropdown when clicking outside
    $(document).on("click", function (e) {
        if (!$(e.target).closest(".input-wrapper, .list-box").length) {
            $(".list-box").hide();
        }
    });
</script>
