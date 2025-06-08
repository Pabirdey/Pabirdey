<select name="Source" class="form-control" onchange="document.getElementById('rawMaterialForm').submit();">
    <option value="">Select Source</option>
    <option value="RMBB_KNR" @(Model?.Source == "RMBB_KNR" ? "selected" : "")>RMBB_KNR</option>
    <option value="RMBB" @(Model?.Source == "RMBB" ? "selected" : "")>RMBB</option>
    <option value="RMBBN" @(Model?.Source == "RMBBN" ? "selected" : "")>RMBBN</option>
</select>
