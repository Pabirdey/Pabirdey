<input type="datetime-local" class="form-control" name="EndDate"
       value="@(Model.EndDate.HasValue ? Model.EndDate.Value.ToString("yyyy-MM-ddTHH:mm") : "")" />