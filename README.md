<script>
    // ===============================
    // STORE CURRENT ROW INDEX
    // ===============================
    let currentClayRowIndex = null;

    // ===============================
    // TOGGLE CUSTOM LIST
    // ===============================
    function toggleList(index) {

        // close other open lists
        document.querySelectorAll(".list-box").forEach(l => {
            l.style.display = "none";
        });

        let list = document.getElementById("list_" + index);
        if (list) {
            list.style.display = (list.style.display === "block") ? "none" : "block";
        }
    }

    // ===============================
    // LIST ITEM CLICK
    // ===============================
    function selectItem(el, index) {

        let selectedValue = el.innerText.trim();

        // set value in textbox
        document.getElementById("clayInput_" + index).value = selectedValue;

        // close list
        document.getElementById("list_" + index).style.display = "none";

        // IF OTHERS → OPEN MODAL
        if (selectedValue === "OTHERS") {

            currentClayRowIndex = index;

            // clear modal dropdowns
            document.getElementById("clay1").value = "";
            document.getElementById("clay2").value = "";
            document.getElementById("clay3").value = "";

            // open bootstrap modal
            let modal = bootstrap.Modal.getOrCreateInstance(
                document.getElementById("clayModal")
            );
            modal.show();
        }
    }

    // ===============================
    // SAVE MODAL DATA
    // ===============================
    function saveClay() {

        let c1 = document.getElementById("clay1").value;
        let c2 = document.getElementById("clay2").value;
        let c3 = document.getElementById("clay3").value;

        if (!c1 && !c2 && !c3) {
            alert("Please select at least one clay");
            return;
        }

        // combine values
        let finalValue = [c1, c2, c3].filter(x => x).join(" + ");

        // write back to SAME ROW textbox
        document.getElementById("clayInput_" + currentClayRowIndex).value = finalValue;

        // close modal
        bootstrap.Modal.getInstance(
            document.getElementById("clayModal")
        ).hide();
    }

    // ===============================
    // CLICK OUTSIDE CLOSE LIST
    // ===============================
    document.addEventListener("click", function (e) {
        if (!e.target.closest(".input-wrapper") &&
            !e.target.closest(".list-box")) {

            document.querySelectorAll(".list-box").forEach(l => {
                l.style.display = "none";
            });
        }
    });
</script>
