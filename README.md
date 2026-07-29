function SaveBFProdData() {
    var modelList = [];   
    if (bf === "BFCTRL") {
        var furnaces = ["C", "D", "E", "F", "A-F"];
        $.each(furnaces, function (i, f) {
            modelList.push({
                FURNACE: $("#FURNACE_" + f).val(),
                ACTUAL: Math.round(parseFloat($("#ACTUAL_" + f).val()) || 0),
                REPORTED: Math.round(parseFloat($("#REPORTED_" + f).val()) || 0),
                BALANCE: Math.round(parseFloat($("#BALANCE_" + f).val()) || 0),

                LD1Tons: Math.round(parseFloat($("#TXT_LD1_TONS").val()) || 0),
                LD2Tons: Math.round(parseFloat($("#TXT_LD2_TONS").val()) || 0),
                LD3Tons: Math.round(parseFloat($("#TXT_LD3_TONS").val()) || 0),
                MRDTPTons: Math.round(parseFloat($("#TXT_MRDTP_TONS").val()) || 0),
                NoOfTP: Math.round(parseFloat($("#NO_TP").val()) || 0),

                ACT_LD1_TONS: Math.round(parseFloat($("#TXTCTOFLD1TONS").val()) || 0),
                ACT_LD2_TONS: Math.round(parseFloat($("#TXTCTOFLD2TONS").val()) || 0),
                ACT_LD3_TONS: Math.round(parseFloat($("#TXTCTOFLD3TONS").val()) || 0),
                ACT_MRD_TP_TONS: Math.round(parseFloat($("#TXTCTOFMRDTPTONS").val()) || 0),

                PROD_DATE: lsSelectedFDate
            });

        });

    }

    // GBFCTRL -> Save only G
    else if (bf === "GBFCTRL") {

        modelList.push({
            FURNACE: $("#TXT_FURNACE_G").val(),
            ACTUAL: Math.round(parseFloat($("#TXT_ACTUAL_G").val()) || 0),
            REPORTED: Math.round(parseFloat($("#TXT_RPT_G").val()) || 0),
            BALANCE: Math.round(parseFloat($("#TXT_BAL_G").val()) || 0),

            LD1_TONS_G: Math.round(parseFloat($("#TXT_LD1_TONS_G").val()) || 0),
            LD2_TONS_G: Math.round(parseFloat($("#TXT_LD2_TONS_G").val()) || 0),
            LD3_TONS_G: Math.round(parseFloat($("#TXT_LD3_TONS_G").val()) || 0),
            MRDTP_TONS_G: Math.round(parseFloat($("#TXT_MRDTP_TONS_G").val()) || 0),

            LD1_TONS_ACTUAL_G: Math.round(parseFloat($("#TXTGBFLD1TONS").val()) || 0),
            LD2_TONS_ACTUAL_G: Math.round(parseFloat($("#TXTGBFLD2TONS").val()) || 0),
            LD3_TONS_ACTUAL_G: Math.round(parseFloat($("#TXTGBFLD3TONS").val()) || 0),
            MRDTP_TONS_ACTUAL_G: Math.round(parseFloat($("#TXTGBFMRDTPTONS").val()) || 0),

            PROD_DATE: lsSelectedFDate
        });

    }

    // HBFCTRL -> Save only H
    else if (bf === "HBFCTRL") {

        modelList.push({
            FURNACE: $("#TXT_FURNACE_H").val(),
            ACTUAL: Math.round(parseFloat($("#TXT_ACTUAL_H").val()) || 0),
            REPORTED: Math.round(parseFloat($("#TXT_RPT_H").val()) || 0),
            BALANCE: Math.round(parseFloat($("#TXT_BAL_H").val()) || 0),

            LD1_TONS_G: Math.round(parseFloat($("#TXT_LD1_TONS_G").val()) || 0),
            LD2_TONS_G: Math.round(parseFloat($("#TXT_LD2_TONS_G").val()) || 0),
            LD3_TONS_G: Math.round(parseFloat($("#TXT_LD3_TONS_G").val()) || 0),
            MRDTP_TONS_G: Math.round(parseFloat($("#TXT_MRDTP_TONS_G").val()) || 0),

            LD1_TONS_ACTUAL_G: Math.round(parseFloat($("#TXTGBFLD1TONS").val()) || 0),
            LD2_TONS_ACTUAL_G: Math.round(parseFloat($("#TXTGBFLD2TONS").val()) || 0),
            LD3_TONS_ACTUAL_G: Math.round(parseFloat($("#TXTGBFLD3TONS").val()) || 0),
            MRDTP_TONS_ACTUAL_G: Math.round(parseFloat($("#TXTGBFMRDTPTONS").val()) || 0),

            PROD_DATE: lsSelectedFDate
        });

    }

    // IBFCTRL -> Save only I
    else if (bf === "IBFCTRL") {

        modelList.push({
            FURNACE: $("#TXT_FURNACE_I").val(),
            ACTUAL: Math.round(parseFloat($("#TXT_ACTUAL_I").val()) || 0),
            REPORTED: Math.round(parseFloat($("#TXT_RPT_I").val()) || 0),
            BALANCE: Math.round(parseFloat($("#TXT_BAL_I").val()) || 0),

            LD1_TONS_G: Math.round(parseFloat($("#TXT_LD1_TONS_G").val()) || 0),
            LD2_TONS_G: Math.round(parseFloat($("#TXT_LD2_TONS_G").val()) || 0),
            LD3_TONS_G: Math.round(parseFloat($("#TXT_LD3_TONS_G").val()) || 0),
            MRDTP_TONS_G: Math.round(parseFloat($("#TXT_MRDTP_TONS_G").val()) || 0),

            LD1_TONS_ACTUAL_G: Math.round(parseFloat($("#TXTGBFLD1TONS").val()) || 0),
            LD2_TONS_ACTUAL_G: Math.round(parseFloat($("#TXTGBFLD2TONS").val()) || 0),
            LD3_TONS_ACTUAL_G: Math.round(parseFloat($("#TXTGBFLD3TONS").val()) || 0),
            MRDTP_TONS_ACTUAL_G: Math.round(parseFloat($("#TXTGBFMRDTPTONS").val()) || 0),

            PROD_DATE: lsSelectedFDate
        });

    }

    console.log(modelList);

    $.ajax({
        url: '/BF_Production/SaveBFProdData',
        type: 'POST',
        data: JSON.stringify(modelList),
        contentType: 'application/json; charset=utf-8',
        success: function (res) {
            if (res.success) {
                SaveDEMOBFProdData(modelList);
            } else {
                alert(res.message);
            }
        },
        error: function () {
            alert("Server Error");
        }
    });
}
