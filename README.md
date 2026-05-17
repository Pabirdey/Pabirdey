<input id="REPORTED_C"
       value="@Model.ReportedC"
       data-original="@Model.ReportedC" />

<input id="REPORTED_C_TD"
       value="@Model.REPORTED_C_TD"
       data-base="@Model.REPORTED_C_TD" />

<input id="BALANCE_C"
       value="@Model.BalanceC"
       data-base="@Model.BalanceC" />
       $("#REPORTED_C").on("blur", function () {

    let inputVal = Number($(this).val()) || 0;

    // ✔ try data-original FIRST, fallback to value
    let originalInput =
        Number($(this).attr("data-original")) ||
        Number($(this).val()) ||
        0;

    // ✔ TD value fallback
    let baseToDate =
        Number($("#REPORTED_C_TD").attr("data-base")) ||
        Number($("#REPORTED_C_TD").val()) ||
        0;

    // ✔ Balance fallback
    let baseBalance =
        Number($("#BALANCE_C").attr("data-base")) ||
        Number($("#BALANCE_C").val()) ||
        0;

    console.log("originalInput:", originalInput);
    console.log("baseToDate:", baseToDate);
    console.log("baseBalance:", baseBalance);

    let diff = inputVal - originalInput;

    $("#REPORTED_C_TD").val(Math.round(baseToDate + diff));
    $("#BALANCE_C").val(Math.round(baseBalance - diff));

    // update for next edit
    $(this).attr("data-original", inputVal);
});
