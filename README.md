  <div class="container-fluid mt-4">
        <h4 class="mb-4" style="font-family:'Comic Sans MS';text-align:center;font-weight:bold;color:#4CAF50;font-size:xx-large;">Raw Material Quantity</h4>
        <hr class="section-divider">
        <form method="post" action="/Blast_Furnace/RawMaterial" id="rawMaterialForm">
            <div class="container-fluid" style="margin-left:280px;">
                <div class="d-flex flex-nowrap gap-2 align-items-end">
                    <div style="width:8%;">
                        <label class="form-label" style="margin-left:40px;">Pile No</label>
                        <input class="form-control" type="text" value="@Model.PileNo" name="PileNo" placeholder="Enter PileNo" autocomplete="off">
                    </div>
                    <div style="width:8%;">
                        <label class="form-label" style="margin-left:40px;">Select Source</label>
                        <select name="Source" class="form-control" onchange="document.getElementById('rawMaterialForm').submit();">
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
                            <option value="C">C</option>iro
                        </select>
                    </div>
                    <div style="width:12%;">
                        <label class="form-label fw-bold" style="margin-left:40px;">Start Date</label>
                        <input type="datetime-local" class="form-control" name="StartDate" value="@(Model.StartDate.HasValue ? Model.StartDate.Value.ToString("yyyy-MM-ddTHH:mm") : "")" />
                    </div>
                    <div style="width:12%;">
                        <label class="form-label" style="margin-left:40px;">End Date</label>
                        <input type="datetime-local" class="form-control" name="EndDate" value="@(Model.EndDate.HasValue ? Model.EndDate.Value.ToString("yyyy-MM-ddTHH:mm") : "")" />
                    </div>
                    <div style="width:12%;">
                        <label class="form-label" style="margin-left:40px;">Cons.St.Date</label>
                        <input type="datetime-local" class="form-control" name="ConsStartDate" value="@(Model.ConsStartDate.HasValue ? Model.ConsStartDate.Value.ToString("yyyy-MM-ddTHH:mm") : "")" />
                    </div>
                </div>
            </div>
            <hr class="section-divider">
            <!-- First row of materials -->
            <div class="row material-row mb-2">
                <div class="col-md-2">
                    <label class="form-label">Noa Fines</label>
                    <input class="form-control" type="text" value="@Model.NoaFines" name="NoaFines" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Joda Fines</label>
                    <input class="form-control" type="text" value="@Model.JodaFines" name="JodaFines" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">KB Fines</label>
                    <input class="form-control" type="text" value="@Model.KBFines" name="KBFines" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Yard Fines</label>
                    <input class="form-control" type="text" value="@Model.YardFines" name="YardFines" autocomplete="off">
                </div>                
            </div>
            
            <div class="row material-row mb-2">                
                <div class="col-md-2">
                    <input type="submit" value="Save" name="SaveRawMaterialM" class="btn btn-primary" />
                </div>
            </div>

            <hr class="section-divider">
         
          
        </form>
    </div>

    [HttpPost]
        public ActionResult RawMaterial(RawMaterial_M input)
        {
            RawMaterial_M model = new RawMaterial_M()
            {
                Source = input.Source,
                PileNo = input.PileNo

            };
            if (!string.IsNullOrEmpty(input.PileNo) && !string.IsNullOrEmpty(input.Source))
            {

                using (OracleConnection conn = new OracleConnection(mycon))
                {
                    conn.Open();
                    string query = "SELECT * FROM imtg.T_PILE_RAWMAT_QUANTITY_NEW WHERE PILE_NO ='" + input.PileNo + "' AND SOURCE ='" + input.Source + "'";
                    using (OracleCommand cmd = new OracleCommand(query, conn))
                    {

                        using (OracleDataReader reader = cmd.ExecuteReader())
                        {
                            if (reader.Read())
                            {
                                model.StartDate = reader["PREP_START_DATE"] == DBNull.Value ? (DateTime?)null : Convert.ToDateTime(reader["PREP_START_DATE"]);
                                model.EndDate = reader["PREP_END_DATE"] == DBNull.Value ? (DateTime?)null : Convert.ToDateTime(reader["PREP_END_DATE"]);
                                model.ConsStartDate = reader["CONS_ST_DATE"] == DBNull.Value ? (DateTime?)null : Convert.ToDateTime(reader["CONS_ST_DATE"]);
                                model.NoaFines = reader["NOA_FINES"] != DBNull.Value ? Convert.ToDecimal(reader["NOA_FINES"]) : 0;
                                model.JodaFines = reader["JODA_FINES"] != DBNull.Value ? Convert.ToDecimal(reader["JODA_FINES"]) : 0;
                                model.KBFines = reader["KB_FINES"] != DBNull.Value ? Convert.ToDecimal(reader["KB_FINES"]) : 0;
                                model.YardFines = reader["YARD_FINES"] != DBNull.Value ? Convert.ToDecimal(reader["YARD_FINES"]) : 0;
                              
                            }
                        }
                    }
                }
            }

            return View(model);
        }

        [HttpPost]
        public ActionResult RawMaterial(RawMaterial_M model)
        {

            using (OracleConnection conn = new OracleConnection(mycon))
            {
                conn.Open();

                using (OracleCommand cmd = new OracleCommand("Proc_Save_Pile_RawMat_Quantity_Entry", conn))
                {
                    cmd.CommandType = CommandType.StoredProcedure;

                    cmd.Parameters.Add("P_PileNo", OracleDbType.Varchar2).Value = model.PileNo ?? "";
                    cmd.Parameters.Add("P_Source", OracleDbType.Varchar2).Value = model.Source ?? "";
                    cmd.Parameters.Add("P_StartDate", OracleDbType.Date).Value = model.StartDate ?? (object)DBNull.Value;
                    cmd.Parameters.Add("P_EndDate", OracleDbType.Date).Value = model.EndDate ?? (object)DBNull.Value;
                    cmd.Parameters.Add("P_ConsStartDate", OracleDbType.Date).Value = model.ConsStartDate ?? (object)DBNull.Value;
                    cmd.Parameters.Add("P_NoaFines", OracleDbType.Decimal).Value = model.NoaFines ?? 0;
                    cmd.Parameters.Add("P_JodaFines", OracleDbType.Decimal).Value = model.JodaFines ?? 0;
                    cmd.Parameters.Add("P_KBFines", OracleDbType.Decimal).Value = model.KBFines ?? 0;                    
                    cmd.Parameters.Add("P_YardFines", OracleDbType.Decimal).Value = model.YardFines ?? 0;

                    cmd.ExecuteNonQuery();
                }
                conn.Close();
            }

            ViewBag.Message = "Data Saved Successfully";
            return View("RawMaterial_M", model);
        }
