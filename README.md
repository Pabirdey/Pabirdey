function toggleList(index) {
        $("#list_" + index).toggle();
    }

    function selectItem(event, el, index) {
        event.stopPropagation(); // 🔥 CRITICAL FIX

        $("#clayInput_" + index).val(el.innerText);
        $("#list_" + index).hide();

        if (el.innerText === "OTHERS") {
            activeRowIndex = index;
            bootstrap.Modal.getOrCreateInstance(
                document.getElementById("clayModal")
            ).show();
        }
    }

    document.addEventListener("click", function (e) {
        if (!e.target.closest(".input-wrapper")) {
            $(".list-box").hide();
        }
    });
