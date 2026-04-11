function calculateAF_ActOnDate() {

    var total = 0;

    var ids = [
        "CBF_ActOnDate",
        "EBF_ActOnDate",
        "FBF_ActOnDate",
        "GBF_ActOnDate",
        "HBF_ActOnDate",
        "IBF_ActOnDate"
    ];

    for (var i = 0; i < ids.length; i++) {
        var val = parseFloat(document.getElementById(ids[i]).value);

        if (!isNaN(val)) {
            total += val;
        }
    }

    document.getElementById("CtoFBF_ActOnDate").value = total;
}
