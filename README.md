 <select name="Source" class="form-control" onchange="document.getElementById('rawMaterialForm').submit();">
                            <option value="">Select Source</option>
                            <option value="RMBB_KNR" @(Model?.Source == "RMBB_KNR" ? "selected" : "")>RMBB_KNR</option>
                            <option value="RMBB" @(Model?.Source == "SOURCE_2" ? "selected" : "")>RMBB</option>
                            <option value="RMBBN" @(Model?.Source == "SOURCE_2" ? "selected" : "")>RMBBN</option>
                        </select>
