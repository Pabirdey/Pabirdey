    <div class="container-fluid" style="margin-left:280px;">
                <div class="d-flex flex-nowrap gap-2 align-items-end">
                    <div style="width:8%;">
                        <label class="form-label" style="margin-left:40px;">Pile No</label>
                        <input type="text"  class="form-control" value="@Model.PileNo" placeholder="Pile No" >
                    </div>
                    <div style="width:8%;">
                        <label class="form-label" style="margin-left:40px;">Source</label>
                        <select name="Source" class="form-control" onchange="document.getElementById('rawMaterialForm').submit();">
                            <option value="">Select Source</option>
                            <option value="RMBB_KNR" @(Model !=null && Model.Source == "RMBB_KNR" ? "selected" : "")>RMBB_KNR</option>
                            <option value="RMBB" @(Model != null && Model.Source == "RMBB" ? "selected" : "")>RMBB</option>
                            <option value="RMBBN" @(Model != null && Model.Source == "RMBBN" ? "selected" : "")>RMBBN</option>
                        </select>

                    </div>
                    <div style="width:8%">
                        <label class="form-label" style="margin-left:40px;">Shift</label>
                        <select class="form-select">
                            <option value="A">A</option>
                            <option value="B">B</option>
                            <option value="C">C</option>iro
                        </select>
                    </div>
                    <div style="width:12%;">
                        <label class="form-label fw-bold" style="margin-left:40px;">Start Date</label>
                        <input type="datetime-local" class="form-control" value="@Model.StartDate">
                    </div>
                    <div style="width:12%;">
                        <label class="form-label" style="margin-left:40px;">End Date</label>
                        <input type="datetime-local" class="form-control" value="@Model.EndDate">
                    </div>
                    <div style="width:12%;">
                        <label class="form-label" style="margin-left:40px;">Cons.St.Date</label>
                        <input type="datetime-local" class="form-control" value="@Model.ConsStartDate">
                    </div>
                </div>
            </div>
