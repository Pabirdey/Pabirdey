function TotUL() {

    var ids = [
        "R61",
        "R66",
        "R71",
        "R76",
        "R81",
        "R354",
        "R91",
        "R96",
        "R101",
        "R106",
        "R111",
        "R116",
        "R274"
    ];

    var total = 0;

    for (var i = 0; i < ids.length; i++) {

        var val =
            parseFloat(
                document.getElementById(ids[i]).value
            ) || 0;

        total += val;
    }

    document.getElementById("txtTotul").value =
        total.toFixed(2);
}
<input type="text"
       id="txtTotul"
       class="form-control"
       readonly>
