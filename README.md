<td>
        <input type="text"
               id="REPORTED_C"
               class="form-control"
               value="@Model.ReportedC"
               data-original="@Model.ReportedC" />
    </td>

    <td>
        <input type="text"
               id="REPORTED_C_TD"
               class="form-control"
               value="@Model.REPORTED_C_TD"
               data-base="@Model.REPORTED_C_TD"
               readonly />
    </td>

    <td>
        <input type="text"
               id="BALANCE_C"
               class="form-control"
               value="@Model.BalanceC"
               data-base="@Model.BalanceC"
               readonly />
    </td>

    $("#REPORTED_C").on("blur", function () {

    let inputVal = Number($(this).val()) || 0;

    // FORCE READ ATTRIBUTES SAFELY
    let originalInput = Number($(this).attr("data-original") || 0);

    let baseToDate = Number($("#REPORTED_C_TD").attr("data-base") || 0);

    let baseBalance = Number($("#BALANCE_C").attr("data-base") || 0);

    console.log("originalInput:", originalInput);
    console.log("baseToDate:", baseToDate);
    console.log("baseBalance:", baseBalance);

    let diff = inputVal - originalInput;

    $("#REPORTED_C_TD").val(Math.round(baseToDate + diff));
    $("#BALANCE_C").val(Math.round(baseBalance - diff));

    // update for next edit
    $(this).attr("data-original", inputVal);
});
