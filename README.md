@model YourNamespace.Models.RmbbPile
@{
    ViewBag.Title = "Raw Material Quantity";
}

<h4 class="mb-4" id="Main_Heading">Raw Material Quantity</h4>
<hr class="section-divider" />

@if (!string.IsNullOrEmpty(ViewBag.Message))
{
    <div class="alert alert-info">@ViewBag.Message</div>
}

<select name="Source" id="SourceSelect" class="form-control" onchange="document.getElementById('rawMaterialForm').submit();">                          
                            <option value="RMBB_KNR" @(Model != null && Model.Source == "RMBB_KNR" ? "selected" : "")>RMBB_KNR</option>
                            <option value="RMBB" @(Model != null && Model.Source == "RMBB" ? "selected" : "")>RMBB</option>
                            <option value="RMBBN" @(Model != null && Model.Source == "RMBBN" ? "selected" : "")>RMBBN</option>
                        </select>
