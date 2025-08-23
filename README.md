 <h4 class="mb-4" id="Main_Heading">Raw Material Quantity</h4>
        <hr class="section-divider">
        <form method="post" action="/RmbbPile/RmbbPile" id="rawMaterialForm">
            <div class="container-fluid" style="margin-left:280px;">
                <div class="d-flex flex-nowrap gap-2 align-items-end">
                    <div style="width:8%;">
                        <label class="form-label" style="margin-left:40px;">Pile No</label>
                        <input class="form-control" type="text" value="@Model.PileNo" name="PileNo" placeholder="Enter PileNo" autocomplete="off">
                    </div>
                    <div style="width:8%;">
                        <label class="form-label" style="margin-left:40px;">Select Source</label>
                        <select name="Source" id="SourceSelect" class="form-control" onchange="document.getElementById('rawMaterialForm').submit();">
                            <option value="">Select Source</option>
                            <option value="RMBB_KNR" @(Model != null && Model.Source == "RMBB_KNR" ? "selected" : "")>RMBB_KNR</option>
                            <option value="RMBB" @(Model != null && Model.Source == "RMBB" ? "selected" : "")>RMBB</option>
                            <option value="RMBBN" @(Model != null && Model.Source == "RMBBN" ? "selected" : "")>RMBBN</option>
                        </select>


                    </div>
                    <div style="width:8%">
                        <label class="form-label" style="margin-left:40px;">Shift</label>
                        <select class="form-select">
                            <option value="A">A</option>
                            <option value="B">B</option>
                            <option value="C">C</option>
                        </select>
                    </div>
                    <div style="width:12%;">
                        <label class="form-label fw-bold" style="mar
    gin-left:40px;">Start Date</label>
                        <input type="text" class="form-control" name="StartDate" id="StartDate" value="@(Model.StartDate.HasValue ? Model.StartDate.Value.ToString("dd-MMM-yyyy HH:mm") : "")" />
                    </div>


                    <div style="width:12%;">
                        <label class="form-label" style="margin-left:40px;">End Date</label>
                        <input type="text" class="form-control" name="EndDate" id="EndDate" value="@(Model.EndDate.HasValue ? Model.EndDate.Value.ToString("dd-MMM-yyyy HH:mm") : "")" />
                    </div>
                    <div style="width:12%;">
                        <label class="form-label" style="margin-left:40px;">Cons.St.Date</label>
                        <input type="text" class="form-control" name="ConsStartDate" id="ConsStartDate" value="@(Model.ConsStartDate.HasValue ? Model.ConsStartDate.Value.ToString("dd-MMM-yyyy HH:mm") : "")" />
                    </div>
                </div>
            </div>
            <hr class="section-divider">
            <!-- First row of materials -->
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Noa Fines</label>
                    <input class="form-control" type="text" value="@Model.NOA_FINES" name="NOA_FINES" id="NOA_FINES" onblur="IOFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Joda Fines</label>
                    <input class="form-control" type="text" value="@Model.JODA_FINES" name="JODA_FINES" id="JODA_FINES" onblur="IOFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">KB Fines</label>
                    <input class="form-control" type="text" value="@Model.KB_FINES" name="KB_FINES" id="KB_FINES" onblur="IOFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Yard Fines</label>
                    <input class="form-control" type="text" value="@Model.YARD_FINES" name="YARD_FINES" id="YARD_FINES" onblur="IOFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">BHJ</label>
                    <input class="form-control" type="text" value="@Model.TXT_BHJ" name="TXT_BHJ" id="TXT_BHJ" onblur="IOFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Namisa</label>
                    <input class="form-control" type="text" value="@Model.IO_NAMISA" name="IO_NAMISA" id="IO_NAMISA" onblur="IMPOreFinesSum()" autocomplete="off">
                </div>
            </div>
            <!-- Second row of materials -->
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Fortescue BF</label>
                    <input class="form-control" type="text" value="@Model.IO_FORTESCUE_BF" name="IO_FORTESCUE_BF" id="IO_FORTESCUE_BF" onblur="IMPOreFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Noa Crushed</label>
                    <input class="form-control" type="text" value="@Model.IRON_ORE_NOA_CRUSHED" name="IRON_ORE_NOA_CRUSHED" id="IRON_ORE_NOA_CRUSHED" onblur="IOFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Joda Crushed</label>
                    <input class="form-control" type="text" value="@Model.IRON_ORE_JODA_CRUSHED" name="IRON_ORE_JODA_CRUSHED" id="IRON_ORE_JODA_CRUSHED" onblur="IOFinesSum()" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">KB Crushed</label>
                    <input class="form-control" type="text" value="@Model.IRON_ORE_KB_CRUSHED" name="IRON_ORE_KB_CRUSHED" id="IRON_ORE_KB_CRUSHED" onblur="IOFinesSum()" autocomplete="off">
                </div>
