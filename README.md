$("#ddlFurnace").on("change", function () {

    var furnace = $(this).val();

    $.ajax({
        url: "/YourController/GetConsumptionData",
        type: "POST",
        data: { furnace: furnace },
        success: function (data) {

            for (var i = 0; i < data.length; i++) {

                var item = data[i];

                if (item.TYPE_NAME === "COAL") {
                    $("#ddlCoal").val(item.DISPLAY_VALUE);
                }

                if (item.TYPE_NAME === "IOC") {
                    $("#ddlIOC").val(item.DISPLAY_VALUE);
                }

                if (item.TYPE_NAME === "PYROX") {
                    $("#ddlPyrox").val(item.DISPLAY_VALUE);
                }

                if (item.TYPE_NAME === "LS") {
                    $("#ddlLS").val(item.DISPLAY_VALUE);
                }

                $("#txtTheoretical").val(item.THEORETICAL_PROD);
            }
        },
        error: function () {
            alert("Error loading data");
        }
    });

});