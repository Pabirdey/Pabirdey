
<tr>
                                            <td><input type="text" class="form-control" id="FURNACE_E" readonly value="E" /></td>
                                            <td><input type="text" class="form-control" id="ACTUAL_E" readonly /></td>
                                            <td><input type="text" class="form-control" id="ACTUAL_E_TD" readonly /></td>
                                            <td><input type="text" class="form-control" data-original="@model.ReportedC" id="REPORTED_E" /></td>
                                            <td><input type="text" class="form-control" id="REPORTED_E_TD" readonly /></td>
                                            <td><input type="text" class="form-control" id="BALANCE_E" readonly /></td> 
                                        </tr>
$(document).ready(function () {

    // store server value as ORIGINAL reference
    $("#REPORTED_C").attr(
        "data-original",
        $("#REPORTED_C").val()
    );

});

$("#REPORTED_C").on("blur", function () {

    // current value (user input)
    let inputVal = parseFloat($(this).val()) || 0;

    // original server value
    let originalInput =
        parseFloat($(this).attr("data-original")) || 0;

    // difference
    let diff = inputVal - originalInput;

    // base values (fixed from DB)
    let baseToDate =
        parseFloat($("#REPORTED_C_TD").attr("data-base")) || 0;

    let baseBalance =
        parseFloat($("#BALANCE_C").attr("data-base")) || 0;

    // update values
    $("#REPORTED_C_TD").val(
        Math.round(baseToDate + diff)
    );

    $("#BALANCE_C").val(
        Math.round(baseBalance - diff)
    );

    // update new original (important for next edit)
    $(this).attr("data-original", inputVal);
});
