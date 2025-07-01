  <div style="width:12%;">
                        <label class="form-label fw-bold" style="margin-left:40px;">Start Date</label>
                        <input type="text" class="form-control" name="StartDate" id="StartDate" value="@(Model.StartDate.HasValue ? Model.StartDate.Value.ToString("dd-MMM-yyyy HH:mm") : "")" />                        
                    </div>
