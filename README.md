 let urlBF = '@urlBF';
        debugger;
    var bf = '@ViewBag.bf';
    if (bf !== "") {
        switch (bf) {
            case 'BFCTRL':               
                $(".reported_G").prop("readonly", true);
                $(".reported_H").prop("readonly", true);
                $(".reported_I").prop("readonly", true);
                $(".NO_TP_SLAG").show();
                $(".LD_A_F").show();
                $(".LD_G").hide();                
                $(".btn-box-wrapper").show();
                $(".CallProcedure").show();
                $(".RawMatCons").show();
                $(".Backbtn").show();
                break;
            case 'GBFCTRL':                
                $(".reported_C").prop("readonly", true);
                $(".reported_D").prop("readonly", true);
                $(".reported_E").prop("readonly", true);
                $(".reported_F").prop("readonly", true);
                $(".reported_H").prop("readonly", true);
                $(".reported_I").prop("readonly", true);
                $(".NO_TP_SLAG").hide();
                $(".LD_A_F").hide();
                $(".LD_G").hide();
                $(".btn-box-wrapper").show();
                $(".CallProcedure").hide();
                $(".RawMatCons").hide();
                $(".Backbtn").show();
                break;
            case 'HBFCTRL':                
                $(".reported_C").prop("readonly", true);
                $(".reported_D").prop("readonly", true);
                $(".reported_E").prop("readonly", true);
                $(".reported_F").prop("readonly", true);
                $(".reported_G").prop("readonly", true);
                $(".reported_I").prop("readonly", true);
                $(".NO_TP_SLAG").hide();
                $(".LD_A_F").hide();
                $(".LD_G").hide();
                $(".btn-box-wrapper").show();
                $(".CallProcedure").hide();
                $(".RawMatCons").hide();
                $(".Backbtn").show();
                break;
            case 'IBFCTRL':               
                $(".reported_C").prop("readonly", true);
                $(".reported_D").prop("readonly", true);
                $(".reported_E").prop("readonly", true);
                $(".reported_F").prop("readonly", true);
                $(".reported_G").prop("readonly", true);
                $(".reported_H").prop("readonly", true);
                $(".NO_TP_SLAG").hide();
                $(".LD_A_F").hide();
                $(".LD_G").hide();
                $(".btn-box-wrapper").show();
                $(".CallProcedure").hide();
                $(".RawMatCons").hide();
                $(".Backbtn").show();
                break;
            default:                
                $(".reported_C").prop("readonly", true);
                $(".reported_D").prop("readonly", true);
                $(".reported_E").prop("readonly", true);
                $(".reported_F").prop("readonly", true);
                $(".reported_G").prop("readonly", true);
                $(".reported_H").prop("readonly", true);
                $(".NO_TP_SLAG").hide();
                $(".LD_A_F").hide();
                $(".LD_G").hide();
                $(".SabeBFProd").hide();                
                $(".CallProcedure").hide();
                $(".RawMatCons").hide();
                $(".Backbtn").show();
                break;
        }
         function SaveBFProdData() {
        var modelList = [];      
        var furnaces1 = ["C","D", "E", "F","A-F"];
        for (var i = 0; i < furnaces1.length; i++) {
            var f = furnaces1[i];
            var model = {
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
            };
            modelList.push(model);
        }
        
        var furnaces2 = ["G", "H", "I"];
        for (var j = 0; j < furnaces2.length; j++) {
            var f = furnaces2[j];
            var model = {
                FURNACE: $("#TXT_FURNACE_" + f).val(),
                ACTUAL: Math.round(parseFloat($("#TXT_ACTUAL_" + f).val()) || 0),
                REPORTED: Math.round(parseFloat($("#TXT_RPT_" + f).val()) || 0),
                BALANCE: Math.round(parseFloat($("#TXT_BAL_" + f).val()) || 0),
                LD1_TONS_G: Math.round(parseFloat($("#TXT_LD1_TONS_G").val()) || 0),
                LD2_TONS_G: Math.round(parseFloat($("#TXT_LD2_TONS_G").val()) || 0),
                LD3_TONS_G: Math.round(parseFloat($("#TXT_LD3_TONS_G").val()) || 0),
                MRDTP_TONS_G: Math.round(parseFloat($("#TXT_MRDTP_TONS_G").val()) || 0),
                LD1_TONS_ACTUAL_G: Math.round(parseFloat($("#TXTGBFLD1TONS").val()) || 0),
                LD2_TONS_ACTUAL_G: Math.round(parseFloat($("#TXTGBFLD2TONS").val()) || 0),
                LD3_TONS_ACTUAL_G: Math.round(parseFloat($("#TXTGBFLD3TONS").val()) || 0),
                MRDTP_TONS_ACTUAL_G: Math.round(parseFloat($("#TXTGBFMRDTPTONS").val()) || 0),                
                PROD_DATE: lsSelectedFDate
            };

            modelList.push(model);
        }

        console.log(modelList);


        // ================= FIRST SAVE =================

        $.ajax({
            url: '/BF_Production/SaveBFProdData',
            type: 'POST',
            data: JSON.stringify(modelList),
            contentType: 'application/json; charset=utf-8',
            dataType: 'json',
            success: function (res) {
                if (res.success) {
                    // ================= SECOND SAVE =================
                    SaveDEMOBFProdData(modelList);

                }
                else {
                    alert(res.message);
                }
            },

            error: function (xhr) {

                alert("Server Error");

                console.log(xhr.responseText);
            }
        });
    }
