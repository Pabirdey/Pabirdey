// When page loads
calculateTotal();

// When value changes
$(document).on("keyup change", ".ul, .balance", function () {
    calculateTotal();
});

function calculateTotal() {

    var ulTotal = 0;
    var balanceTotal = 0;

    // Sum of U/L column
    $(".ul").each(function () {

        var val = parseFloat($(this).val()) || 0;
        ulTotal += val;

    });

    // Sum of Balance column
    $(".balance").each(function () {

        var val = parseFloat($(this).val()) || 0;
        balanceTotal += val;

    });

    // Grand Total
    var grandTotal = ulTotal + balanceTotal;

    $("#txtTotal").val(grandTotal);
}