$("#REPORTED_C").on("blur", function () {

    let id = $(this).attr("id");

    let current = Number($(this).val()) || 0;

    let old = originalValues[id];   // ✔ ORIGINAL VALUE (1500)

    let diff = current - old;

    let baseTD = Number($("#REPORTED_C_TD").val()) || 0;

    let baseBal = Number($("#BALANCE_C").val()) || 0;

    $("#REPORTED_C_TD").val(baseTD + diff);
    $("#BALANCE_C").val(baseBal - diff);

    // update stored value for next edit
    originalValues[id] = current;
});

var originalValues = {};

$(document).ready(function () {

    $(".reported").each(function () {

        let id = $(this).attr("id");

        originalValues[id] = Number($(this).val()) || 0;

    });

});
