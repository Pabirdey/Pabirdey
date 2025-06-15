<input type="datetime-local" name="EntryTime" class="form-control"
       value="@(Model.EntryTime.HasValue ? Model.EntryTime.Value.ToString("yyyy-MM-ddTHH:mm") : "")" />