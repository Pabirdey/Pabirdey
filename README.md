public class ProductionModel
{
    public string ProductionDate { get; set; }

    // Furnace values
    public decimal OnDate_C { get; set; }
    public decimal ToDate_C { get; set; }
    public decimal Balance_C { get; set; }

    public decimal OnDate_D { get; set; }
    public decimal ToDate_D { get; set; }
    public decimal Balance_D { get; set; }

    public decimal OnDate_E { get; set; }
    public decimal ToDate_E { get; set; }
    public decimal Balance_E { get; set; }

    // Actual Breakup
    public decimal LD1Tons { get; set; }
    public decimal LD2Tons { get; set; }
    public decimal LD3Tons { get; set; }
    public decimal MRDTPTons { get; set; }
    public decimal NoOfTP { get; set; }
    public decimal NoOfSlagLadle { get; set; }
}


public ActionResult Production()
{
    ProductionModel model = new ProductionModel();
    model.ProductionDate = DateTime.Now.ToString("dd-MMM-yyyy");

    return View(model);
}


@model YourProject.Models.ProductionModel

<div class="container">

    <h3>Production</h3>

    <!-- Date -->
    <label>Date</label>
    <input type="text" id="ProductionDate" 
           value="@Model.ProductionDate" class="form-control" />

    <br />

    <!-- Furnace Table -->
    <table class="table table-bordered">
        <tr>
            <th>Furnace</th>
            <th>On Date</th>
            <th>To Date</th>
            <th>Balance</th>
        </tr>

        <tr>
            <td>C</td>
            <td><input type="text" id="OnDate_C" value="@Model.OnDate_C" /></td>
            <td><input type="text" id="ToDate_C" value="@Model.ToDate_C" /></td>
            <td><input type="text" id="Balance_C" value="@Model.Balance_C" /></td>
        </tr>

        <tr>
            <td>D</td>
            <td><input type="text" id="OnDate_D" value="@Model.OnDate_D" /></td>
            <td><input type="text" id="ToDate_D" value="@Model.ToDate_D" /></td>
            <td><input type="text" id="Balance_D" value="@Model.Balance_D" /></td>
        </tr>

        <tr>
            <td>E</td>
            <td><input type="text" id="OnDate_E" value="@Model.OnDate_E" /></td>
            <td><input type="text" id="ToDate_E" value="@Model.ToDate_E" /></td>
            <td><input type="text" id="Balance_E" value="@Model.Balance_E" /></td>
        </tr>

    </table>

    <br />

    <!-- Actual Breakup -->
    <h4>Actual Breakup</h4>

    <label>LD1 Tons</label>
    <input type="text" id="LD1Tons" value="@Model.LD1Tons" />

    <label>LD2 Tons</label>
    <input type="text" id="LD2Tons" value="@Model.LD2Tons" />

    <label>LD3 Tons</label>
    <input type="text" id="LD3Tons" value="@Model.LD3Tons" />

    <label>MRD TP Tons</label>
    <input type="text" id="MRDTPTons" value="@Model.MRDTPTons" />

    <label>No Of TP</label>
    <input type="text" id="NoOfTP" value="@Model.NoOfTP" />

    <label>No Of Slag Ladle</label>
    <input type="text" id="NoOfSlagLadle" value="@Model.NoOfSlagLadle" />

    <br /><br />

    <button type="button" onclick="SaveProduction()">Save</button>

</div>

function SaveProduction() {

    var model = {
        ProductionDate: document.getElementById("ProductionDate").value,

        OnDate_C: document.getElementById("OnDate_C").value,
        ToDate_C: document.getElementById("ToDate_C").value,
        Balance_C: document.getElementById("Balance_C").value,

        OnDate_D: document.getElementById("OnDate_D").value,
        ToDate_D: document.getElementById("ToDate_D").value,
        Balance_D: document.getElementById("Balance_D").value,

        LD1Tons: document.getElementById("LD1Tons").value,
        LD2Tons: document.getElementById("LD2Tons").value,
        LD3Tons: document.getElementById("LD3Tons").value,
        MRDTPTons: document.getElementById("MRDTPTons").value,
        NoOfTP: document.getElementById("NoOfTP").value,
        NoOfSlagLadle: document.getElementById("NoOfSlagLadle").value
    };

    $.ajax({
        url: '/Production/SaveProduction',
        type: 'POST',
        data: JSON.stringify(model),
        contentType: 'application/json',
        success: function () {
            alert("Saved successfully");
        }
    });
}
