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

<form method="post" action="/RmbbPile/RmbbPile" id="rawMaterialForm">
    <div class="container-fluid" style="margin-left: 80px;">
        <div class="d-flex flex-nowrap gap-2 align-items-end">
            <div style="width:10%;">
                <label class="form-label">Pile No</label>
                <input class="form-control" type="text" name="PileNo" value="@Model.PileNo" autocomplete="off" />
            </div>
            <div style="width:12%;">
                <label class="form-label">Select Source</label>
                <select name="Source" class="form-control">
                    <option value="">Select Source</option>
                    <option value="RMBB_KNR" @(Model.Source == "RMBB_KNR" ? "selected" : "")>RMBB_KNR</option>
                    <option value="RMBB" @(Model.Source == "RMBB" ? "selected" : "")>RMBB</option>
                    <option value="RMBBN" @(Model.Source == "RMBBN" ? "selected" : "")>RMBBN</option>
                </select>
            </div>
            <div style="width:12%;">
                <label class="form-label">Start Date</label>
                <input class="form-control" type="text" name="StartDate" id="StartDate" value="@(Model.StartDate?.ToString("dd-MMM-yyyy HH:mm"))" />
            </div>
            <div style="width:12%;">
                <label class="form-label">End Date</label>
                <input class="form-control" type="text" name="EndDate" id="EndDate" value="@(Model.EndDate?.ToString("dd-MMM-yyyy HH:mm"))" />
            </div>
            <div style="width:12%;">
                <label class="form-label">Cons. Start Date</label>
                <input class="form-control" type="text" name="ConsStartDate" id="ConsStartDate" value="@(Model.ConsStartDate?.ToString("dd-MMM-yyyy HH:mm"))" />
            </div>
            <div>
                <button type="submit" class="btn btn-primary">Load</button>
                <button type="submit" class="btn btn-success" name="SaveRawMaterial" value="Save">Save</button>
            </div>
        </div>
    </div>

    <hr />

    <div class="row material-row mb-2" style="margin-left: 80px;">
        <div class="col-md-2">
            <label>Noa Fines</label>
            <input class="form-control" type="text" name="NOA_FINES" value="@Model.NOA_FINES" autocomplete="off" />
        </div>
        <div class="col-md-2">
            <label>Joda Fines</label>
            <input class="form-control" type="text" name="JODA_FINES" value="@Model.JODA_FINES" autocomplete="off" />
        </div>
        <div class="col-md-2">
            <label>KB Fines</label>
            <input class="form-control" type="text" name="KB_FINES" value="@Model.KB_FINES" autocomplete="off" />
        </div>
        <div class="col-md-2">
            <label>Yard Fines</label>
            <input class="form-control" type="text" name="YARD_FINES" value="@Model.YARD_FINES" autocomplete="off" />
        </div>
    </div>
</form>
