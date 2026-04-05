@model YourProject.Models.FurnaceViewModel

@{
    ViewBag.Title = "Furnace Entry";
}

<h3>Furnace Entry Table</h3>

<form method="post">
<div class="table-responsive">
<table class="table table-bordered text-center">

    <thead>
        <tr>
            <th>Date Time</th>
            <th>Furnace</th>
            <th>On Date</th>
            <th>To Date</th>
            <th>On Date</th>
            <th>To Date</th>
            <th>Balance</th>
        </tr>
    </thead>

    <tbody>

        <!-- Row 1 -->
        <tr>
            <td><input type="text" name="Row1.DateTime" value="@Model.Row1.DateTime" class="form-control" /></td>
            <td><input type="text" name="Row1.Furnace" value="@Model.Row1.Furnace" class="form-control" /></td>
            <td><input type="date" name="Row1.OnDate1" value="@Model.Row1.OnDate1" class="form-control" /></td>
            <td><input type="date" name="Row1.ToDate1" value="@Model.Row1.ToDate1" class="form-control" /></td>
            <td><input type="date" name="Row1.OnDate2" value="@Model.Row1.OnDate2" class="form-control" /></td>
            <td><input type="date" name="Row1.ToDate2" value="@Model.Row1.ToDate2" class="form-control" /></td>
            <td><input type="text" name="Row1.Balance" value="@Model.Row1.Balance" class="form-control" /></td>
        </tr>

        <!-- Row 2 -->
        <tr>
            <td><input type="text" name="Row2.DateTime" value="@Model.Row2.DateTime" class="form-control" /></td>
            <td><input type="text" name="Row2.Furnace" value="@Model.Row2.Furnace" class="form-control" /></td>
            <td><input type="date" name="Row2.OnDate1" value="@Model.Row2.OnDate1" class="form-control" /></td>
            <td><input type="date" name="Row2.ToDate1" value="@Model.Row2.ToDate1" class="form-control" /></td>
            <td><input type="date" name="Row2.OnDate2" value="@Model.Row2.OnDate2" class="form-control" /></td>
            <td><input type="date" name="Row2.ToDate2" value="@Model.Row2.ToDate2" class="form-control" /></td>
            <td><input type="text" name="Row2.Balance" value="@Model.Row2.Balance" class="form-control" /></td>
        </tr>

        <!-- Row 3 -->
        <tr>
            <td><input type="text" name="Row3.DateTime" value="@Model.Row3.DateTime" class="form-control" /></td>
            <td><input type="text" name="Row3.Furnace" value="@Model.Row3.Furnace" class="form-control" /></td>
            <td><input type="date" name="Row3.OnDate1" value="@Model.Row3.OnDate1" class="form-control" /></td>
            <td><input type="date" name="Row3.ToDate1" value="@Model.Row3.ToDate1" class="form-control" /></td>
            <td><input type="date" name="Row3.OnDate2" value="@Model.Row3.OnDate2" class="form-control" /></td>
            <td><input type="date" name="Row3.ToDate2" value="@Model.Row3.ToDate2" class="form-control" /></td>
            <td><input type="text" name="Row3.Balance" value="@Model.Row3.Balance" class="form-control" /></td>
        </tr>

    </tbody>
</table>
</div>

<button type="submit" class="btn btn-success">Save</button>
</form>

@if (ViewBag.Message != null)
{
    <p style="color:green">@ViewBag.Message</p>
}
