@foreach (var item in Model.PSW_BL1LIST)
                        {
                            <option value="@item.Value" @(Model.PSW_BL1 != null && item.Value == Model.PSW_BL1.ToString() ? "selected" : "")>
                                @item.Text
                            </option>
                        }
