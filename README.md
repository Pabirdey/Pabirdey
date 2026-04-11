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

    ids.forEach(function (id) {
        var val = parseFloat(document.getElementById(id).value) || 0;
        total += val;
    });

    document.getElementById("CtoFBF_ActOnDate").value = total;
}
