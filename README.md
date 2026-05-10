<script>

$("#ddlShift,#txtDate").change(function () {

    loadShiftData();

});

function loadShiftData() {

    var sDate = $("#txtDate").val();

    var sShift = $("#ddlShift").val();

    if (sDate == "" || sShift == "") {

        return;

    }

    $.ajax({

        url: '/Furnace_High_line/GetShiftData',

        type: 'GET',

        data: {

            sDate: sDate,
            sShift: sShift

        },

        success: function (res) {

            if (res.success == true) {

                // Set Signoff Data
                $("#txtUser").val(res.SIGNOFF_NAME);

                if (res.SO_CHECK == 1) {

                    $("#signoff").prop("checked", true);

                    // Disable Buttons
                    $("#PBSAVE").prop("disabled", true);

                    $("#PBDELETE").prop("disabled", true);
                }
                else {

                    $("#signoff").prop("checked", false);

                    $("#PBSAVE").prop("disabled", false);

                    $("#PBDELETE").prop("disabled", false);
                }

                // Call Table Load Functions
                LoadCokeUnloading();

                LoadHighlineData();

                LoadRawMaterial();

                LoadUnloadReport();
            }

        },

        error: function () {

            alert("Error Loading Data");

        }

    });

}

</script>
