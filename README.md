  <select name="PSW_BL1" id="PSW_BL1" class="form-control">
        <option value="">Select</option>
        @foreach (var item in Model.PSW_BL1List)
        {
            <option value="@item.Value" @(item.Value == Model.PSW_BL1?.ToString() ? "selected" : "")>
                @item.Text
            </option>
        }
    </select>
