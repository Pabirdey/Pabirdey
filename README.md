<input type="text"
       id="REPORTED_C"
       class="form-control"
       value="@Model.REPORTED_C"
       data-original="@Model.REPORTED_C" />
       <input type="text"
       id="REPORTED_C_TD"
       class="form-control"
       value="@Model.REPORTED_C_TD"
       data-base="@Model.REPORTED_C_TD"
       readonly />
       <input type="text"
       id="REPORTED_C_TD"
       class="form-control"
       value="@Model.REPORTED_C_TD"
       data-base="@Model.REPORTED_C_TD"
       readonly />

<input type="text"
       id="BALANCE_C"
       class="form-control"
       value="@Model.BALANCE_C"
       data-base="@Model.BALANCE_C"
       readonly />

<input type="text"
       id="BALANCE_C"
       class="form-control"
       value="@Model.BALANCE_C"
       data-base="@Model.BALANCE_C"
       readonly />

       $("#REPORTED_C").on("blur", function () {

    // current value
    let inputVal = parseFloat($(this).val()) || 0;

    // original server value
    let originalInput = parseFloat($(this).attr("data-original")) || 0;

    // difference
    let diff = inputVal - originalInput;

    // base values
    let baseToDate = parseFloat($("#REPORTED_C_TD").attr("data-base")) || 0;

    let baseBalance = parseFloat($("#BALANCE_C").attr("data-base")) || 0;

    // update values
    $("#REPORTED_C_TD").val(Math.round(baseToDate + diff));
    $("#BALANCE_C").val(Math.round(baseBalance - diff));

    // update original for next edit
    $(this).attr("data-original", inputVal);
});
