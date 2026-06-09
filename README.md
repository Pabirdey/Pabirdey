$(document).on("change", ".arrivedFrom", function () {

    var row = $(this).closest("tr");

    var arrivedFrom = $(this).val();

    // Check selected value
    if (arrivedFrom == "C") {
        console.log("C Selected");
    }
    else if (arrivedFrom == "E") {
        console.log("E Selected");
    }
    else if (arrivedFrom == "F") {
        console.log("F Selected");
    }
    else if (arrivedFrom == "G") {
        console.log("G Selected");
    }
    else if (arrivedFrom == "H") {
        console.log("H Selected");
    }
    else if (arrivedFrom == "I") {
        console.log("I Selected");
    }

    $.ajax({
        url: '/Granshot/CalculateLadle',
        type: 'POST',
        data: {
            lsSelectedFDate: $("#lsSelectedFDate").val(),
            ddlshift: $("#ddlshift").val(),
            TRP_NO: row.find("td:eq(3) input").val(),
            LADLE_FLST_TIME: row.find("td:eq(4) input").val(),
            LADLE_FLEND_TIME: row.find("td:eq(5) input").val(),
            ARRIVED_FROM: arrivedFrom
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

});
