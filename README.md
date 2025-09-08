<select id="PSW_BL1" name="PSW_BL1" onchange="CheckPSW_CONS1()" class="form-control">
    <option value="">Select</option>
    @if (ViewBag.PSW_BL1LIST != null)
    {
        foreach (var item in (List<SelectListItem>)ViewBag.PSW_BL1LIST)
        {
            <option value="@item.Value" @(item.Value == Convert.ToString(Model.PSW_BL1) ? "selected" : "")>
                @item.Text
            </option>
        }
    }
</select>