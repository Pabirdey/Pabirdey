$(document).on("change", ".arrivedFrom", function () {

    var row = $(this).closest("tr");

    $.ajax({
        url: '/Granshot/CalculateLadle',
        type: 'POST',
        data: {
            lsSelectedFDate: $("#lsSelectedFDate").val(),
            ddlshift: $("#ddlshift").val(),
            TRP_NO: row.find("td:eq(3) input").val(),
            LADLE_FLST_TIME: row.find("td:eq(4) input").val(),
            LADLE_FLEND_TIME: row.find("td:eq(5) input").val(),
            ARRIVED_FROM: $(this).val()
        },
        success: function (response) {

            if (response.success) {

                row.find("td:eq(7) input").val(response.data.GROSS_WT);
                row.find("td:eq(8) input").val(response.data.TARE_WT);
                row.find("td:eq(9) input").val(response.data.NET_WT);
                row.find("td:eq(10) input").val(response.data.POURING_RATE);
                row.find("td:eq(11) input").val(response.data.HMT);
            }
            else {
                alert(response.message);
            }
        },
        error: function () {
            alert("Error occurred");
        }
    });

});<td><input type="text" class="table-input trpNo"></td>
<td><input type="time" class="table-input ladleStart"></td>
<td><input type="time" class="table-input ladleEnd"></td>

<td style="background-color:#c0f9fa;">
    <input type="text" class="table-input grossWt" readonly>
</td>
<td style="background-color:#c0f9fa;">
    <input type="text" class="table-input tareWt" readonly>
</td>
<td style="background-color:#c0f9fa;">
    <input type="text" class="table-input netWt" readonly>
</td>
<td style="background-color:#c0f9fa;">
    <input type="text" class="table-input pouringRate" readonly>
</td>
<td style="background-color:#c0f9fa;">
    <input type="text" class="table-input hmt" readonly>
</td>
