 let urlBF = '@urlBF';
    var bf = '@ViewBag.bf';
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
@Html.ActionLink("Back", "BF_Prod ", "BF_Production", new { bf = @urlBF }, new { @class = "btn btn-primary Back" })
