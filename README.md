 <div class="row material-row mb-2">               
                <div class="col-md-2">
                    <label class="form-label">Mgo</label>
                    <input class="form-control" type="text" value="@Model.PileChemMgo" name="PileChemMgo" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">C</label>
                    <input class="form-control" type="text" value="@Model.PileChemC" name="PileChemC" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Oil</label>
                    <input class="form-control" type="text" value="@Model.PileChemOil" name="PileChemOil" autocomplete="off">
                </div>
                <div class="col-md-2">
                    <label class="form-label">Feo</label>
                    <input class="form-control" type="text" value="@Model.PileChemFeo" name="PileChemFeo" autocomplete="off">
                </div>
                <div class="col-md-2">                                        
                    <input type="submit" value="Save" name="SaveRawMaterial" class="btn btn-primary"/>                    
                </div>
            </div>

               public ActionResult SaveRawMaterial(RawMaterialQuantity model)
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
                    cmd.Parameters.Add("P_JodaFines", OracleDbType.Decimal).Value = model.JodaFines ?? 0;
                    cmd.Parameters.Add("P_KBFines", OracleDbType.Decimal).Value = model.KBFines ?? 0;
                    cmd.Parameters.Add("P_NoaFines", OracleDbType.Decimal).Value = model.NoaFines ?? 0;
                    cmd.Parameters.Add("P_YardFines", OracleDbType.Decimal).Value = model.YardFines ?? 0;

                    cmd.ExecuteNonQuery();
                }
                conn.Close();
            }

            ViewBag.Message = "Data Saved Successfully";
            return View("RawMaterialQuantity",model); 
        }
