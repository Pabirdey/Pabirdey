if (bf !== "") {
        switch (bf) {
            case 'BFCTRL':               
                $(".reported_G").prop("readonly", true);
                $(".reported_H").prop("readonly", true);
                $(".reported_I").prop("readonly", true);
                $(".btn-box-wrapper").show();
                $(".CallProcedure").show();
                $(".RawMatCons").show();
                break;
            case 'GBFCTRL':                
                $(".reported_C").prop("readonly", true);
                $(".reported_E").prop("readonly", true);
                $(".reported_F").prop("readonly", true);
                $(".reported_H").prop("readonly", true);
                $(".reported_I").prop("readonly", true);
                $(".btn-box-wrapper").show();
                $(".CallProcedure").hide();
                $(".RawMatCons").hide();
                break;
            case 'HBFCTRL':                
                $(".reported_C").prop("readonly", true);
                $(".reported_E").prop("readonly", true);
                $(".reported_F").prop("readonly", true);
                $(".reported_G").prop("readonly", true);
                $(".reported_I").prop("readonly", true);
                $(".btn-box-wrapper").show();
                $(".CallProcedure").hide();
                $(".RawMatCons").hide();
                break;
            case 'IBFCTRL':               
                $(".reported_C").prop("readonly", true);
                $(".reported_E").prop("readonly", true);
                $(".reported_F").prop("readonly", true);
                $(".reported_G").prop("readonly", true);
                $(".reported_H").prop("readonly", true);
                $(".btn-box-wrapper").show();
                $(".CallProcedure").hide();
                $(".RawMatCons").hide();
                break;
            default:                
                $(".reported_C").prop("readonly", true);
                $(".reported_E").prop("readonly", true);
                $(".reported_F").prop("readonly", true);
                $(".reported_G").prop("readonly", true);
                $(".reported_H").prop("readonly", true);
                $(".reported_I").prop("readonly", true);
                $(".btn-box-wrapper").hide();
                $(".CallProcedure").hide();
                $(".RawMatCons").hide();
                break;
        }
    }
    @Html.ActionLink("Back", "HML_Home", "HML",null, new { @class = "btn btn-primary Back" })
