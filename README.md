function saveCarbonPaste() {

    var dataList = [];

    var rows = document.querySelectorAll("#carbon_paste_inj tbody tr");

    for (var i = 0; i < rows.length; i++) {

        var dt     = rows[i].querySelector(".dt").value;
        var shift  = rows[i].querySelector(".shift").value;
        var tuyere = rows[i].querySelector(".tuyere").value;
        var drum   = rows[i].querySelector(".drum").value;

        var obj = {
            DATE_TIME: dt,
            SHIFT: shift,
            BELOW_TUYERE: tuyere,
            NO_OF_DRUM: drum
        };

        dataList.push(obj);
    }

    // ===== SAVE ONLY JAVASCRIPT =====
    localStorage.setItem(
        "CARBON_PASTE_DATA",
        JSON.stringify(dataList)
    );

    alert("Saved Successfully (No this keyword used)");

    loadCarbonPaste_JS();
}