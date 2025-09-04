 foreach (var item in (List<SelectListItem>)ViewBag.PSW_BL1)
            {
                var selected = item.Value == Model.PSW_BL1?.ToString() ? "selected" : "";
                <option value="@item.Value" @selected>@item.Text</option>
            }
