success: function (res) {

    if (res.success == true) {

        // Auto check checkbox
        $("#signoff").prop("checked", true);

        if (res.disableButton == true) {

            $("#CokeUnloading").prop("disabled", true);

        }
        else {

            $("#CokeUnloading").prop("disabled", false);

        }
    }
    else {

        alert(res.message);

    }
}

success: function (res) {

    if (res.success == true) {

        $("#signoff").prop("checked", res.SO_CHECK == 1);

        $("#CokeUnloading").prop("disabled", res.disableButton);

    }
    else {

        alert(res.message);

    }
}
