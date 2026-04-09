<form method="post">

<input type="date" name="DateTime" value="@Model.DateTime" class="form-control" />

<table class="table table-bordered text-center">
    <tr>
        <th>Furnace</th>
        <th>On Date</th>
        <th>To Date</th>
        <th>On Date</th>
        <th>To Date</th>
        <th>Balance</th>
    </tr>

    <!-- CBF -->
    <tr>
        <td><input type="text" name="CBF_Furnace" value="@Model.CBF_Furnace" readonly /></td>
        <td><input type="text" name="CBF_ActOnDate" value="@Model.CBF_ActOnDate" readonly /></td>
        <td><input type="text" name="CBF_ActToDate" value="@Model.CBF_ActToDate" readonly /></td>
        <td><input type="text" name="CBF_ReportOnDate" value="@Model.CBF_ReportOnDate" /></td>
        <td><input type="text" name="CBF_ReportToDate" value="@Model.CBF_ReportToDate" /></td>
        <td><input type="text" name="CBF_Balance" value="@Model.CBF_Balance" readonly /></td>
    </tr>

    <!-- EBF -->
    <tr>
        <td><input type="text" name="EBF_Furnace" value="@Model.EBF_Furnace" readonly /></td>
        <td><input type="text" name="EBF_ActOnDate" value="@Model.EBF_ActOnDate" readonly /></td>
        <td><input type="text" name="EBF_ActToDate" value="@Model.EBF_ActToDate" readonly /></td>
        <td><input type="text" name="EBF_ReportOnDate" value="@Model.EBF_ReportOnDate" /></td>
        <td><input type="text" name="EBF_ReportToDate" value="@Model.EBF_ReportToDate" /></td>
        <td><input type="text" name="EBF_Balance" value="@Model.EBF_Balance" readonly /></td>
    </tr>

</table>

<button type="submit" class="btn btn-success">Save</button>

</form>

public class BF_Production
{
    public string DateTime { get; set; }

    public string CBF_Furnace { get; set; }
    public decimal? CBF_ActOnDate { get; set; }
    public decimal? CBF_ActToDate { get; set; }
    public decimal? CBF_ReportOnDate { get; set; }
    public decimal? CBF_ReportToDate { get; set; }
    public decimal? CBF_Balance { get; set; }

    public string EBF_Furnace { get; set; }
    public decimal? EBF_ActOnDate { get; set; }
    public decimal? EBF_ActToDate { get; set; }
    public decimal? EBF_ReportOnDate { get; set; }
    public decimal? EBF_ReportToDate { get; set; }
    public decimal? EBF_Balance { get; set; }

    public string FBF_Furnace { get; set; }
    public decimal? FBF_ActOnDate { get; set; }
    public decimal? FBF_ActToDate { get; set; }
    public decimal? FBF_ReportOnDate { get; set; }
    public decimal? FBF_ReportToDate { get; set; }
    public decimal? FBF_Balance { get; set; }

    public string GBF_Furnace { get; set; }
    public decimal? GBF_ActOnDate { get; set; }
    public decimal? GBF_ActToDate { get; set; }
    public decimal? GBF_ReportOnDate { get; set; }
    public decimal? GBF_ReportToDate { get; set; }
    public decimal? GBF_Balance { get; set; }

    public string HBF_Furnace { get; set; }
    public decimal? HBF_ActOnDate { get; set; }
    public decimal? HBF_ActToDate { get; set; }
    public decimal? HBF_ReportOnDate { get; set; }
    public decimal? HBF_ReportToDate { get; set; }
    public decimal? HBF_Balance { get; set; }

    public string IBF_Furnace { get; set; }
    public decimal? IBF_ActOnDate { get; set; }
    public decimal? IBF_ActToDate { get; set; }
    public decimal? IBF_ReportOnDate { get; set; }
    public decimal? IBF_ReportToDate { get; set; }
    public decimal? IBF_Balance { get; set; }
}
