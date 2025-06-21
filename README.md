function rawMaterialForm() {
        debugger;
        var source = document.getElementById("SourceSelect").value;
        var block = document.getElementById("pswBlock");
        if (source === 'RMBB_KNR') {
            block.style.display = "block";
        } else {
            block.style.display = "none";
        }

    }

     <select name="Source" id="SourceSelect" class="form-control" onchange="document.getElementById('rawMaterialForm').submit();">
                            <option value="">Select Source</option>
                            <option value="RMBB_KNR" @(Model !=null && Model.Source == "RMBB_KNR" ? "selected" : "")>RMBB_KNR</option>
                            <option value="RMBB" @(Model != null && Model.Source == "RMBB" ? "selected" : "")>RMBB</option>
                            <option value="RMBBN" @(Model != null && Model.Source == "RMBBN" ? "selected" : "")>RMBBN</option>
                        </select>
