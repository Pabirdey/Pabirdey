<script>
    var activeRowIndex = null;

    /* 🔥 MUST be window.function */
    window.toggleList = function (index) {
        var list = document.getElementById("list_" + index);
        if (!list) return;

        list.style.display = (list.style.display === "block") ? "none" : "block";
    };

    window.selectItem = function (event, el, index) {
        event.stopPropagation();

        document.getElementById("clayInput_" + index).value = el.innerText;
        document.getElementById("list_" + index).style.display = "none";

        if (el.innerText === "OTHERS") {
            activeRowIndex = index;
            bootstrap.Modal
                .getOrCreateInstance(document.getElementById("clayModal"))
                .show();
        }
    };

    document.addEventListener("click", function (e) {
        if (!e.target.closest(".input-wrapper")) {
            document.querySelectorAll(".list-box").forEach(x => x.style.display = "none");
        }
    });
</script>
