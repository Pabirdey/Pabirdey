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
let val1 = parseFloat(document.getElementById('box1').value) || 0;
    let val2 = parseFloat(document.getElementById('box2').value) || 0;
    let val3 = parseFloat(document.getElementById('box3').value) || 0;

    // Sum the values
    let sum = val1 + val2 + val3;

    // Display in the fourth text box
    document.getElementById('total').value = sum;
