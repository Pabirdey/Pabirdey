function SaveData() {

    var details = [];

    $("#tblBody tr").each(function () {

        var castNo = $(this).find("td:eq(0) input").val();

        if (castNo != "") {

            details.push({
                CAST_NO: castNo,
                CAST_ST_TIME: $(this).find("td:eq(1) input").val(),
                CAST_END_TIME: $(this).find("td:eq(2) input").val(),
                TRP_NO: $(this).find("td:eq(3) input").val(),
                LADLE_FLST_TIME: $(this).find("td:eq(4) input").val(),
                LADLE_FLEND_TIME: $(this).find("td:eq(5) input").val(),
                ARRIVED_FROM: $(this).find(".arrivedFrom").val(),
                GROSS_WT: $(this).find("td:eq(7) input").val(),
                TARE_WT: $(this).find("td:eq(8) input").val(),
                NET_WT: $(this).find("td:eq(9) input").val(),
                POURING_RATE: $(this).find("td:eq(10) input").val(),
                HMT: $(this).find("td:eq(11) input").val(),
                REASON_POURING: $(this).find("td:eq(12) input").val()
            });
        }
    });

    var model = {
        ProductionDate: $("#hiddenDate").val(),
        Shift: $("#ddlshift").val(),
        Details: details
    };

    $.ajax({
        url: '/Granshot/Save',
        type: 'POST',
        contentType: 'application/json; charset=utf-8',
        data: JSON.stringify(model),
        success: function (response) {

            if (response.success) {
                alert(response.message);
            }
            else {
                alert(response.message);
            }
        },
        error: function () {
            alert("Error occurred");
        }
    });
}
