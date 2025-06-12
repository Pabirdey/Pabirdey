  public ActionResult RawMaterialEntry(RawMaterialQuantity input)
        {
            RawMaterialQuantity model = new RawMaterialQuantity
            {
                Source= input.Source,
                PileNo= input.PileNo
            };           
                        

            using (OracleConnection conn = new OracleConnection(mycon))
            {
                conn.Open();

                //string query = "SELECT * FROM imtg.T_PILE_RAWMAT_QUANTITY_NEW WHERE PILE_NO ='"+input.PileNo+"'  AND SOURCE ='"+input.Source+"'";
                    string query = "SELECT * FROM imtg.T_PILE_RAWMAT_QUANTITY_NEW WHERE PILE_NO ='" + input.PileNo + "' AND SOURCE ='" + input.Source + "'";
                using (OracleCommand cmd = new OracleCommand(query, conn))
                {
                    
                    using (OracleDataReader reader = cmd.ExecuteReader())
                    {
                        if (reader.Read())
                        {                                                       
                            model.NoaFines = reader["NOA_FINES"] != DBNull.Value ? Convert.ToDecimal(reader["NOA_FINES"]) :0;                            
                            model.JodaFines = reader["JODA_FINES"] != DBNull.Value ? Convert.ToDecimal(reader["JODA_FINES"]) : 0;
                            model.KBFines = reader["KB_FINES"] != DBNull.Value ? Convert.ToDecimal(reader["KB_FINES"]) : 0;
                            model.YardFines=reader["YARD_FINES"] != DBNull.Value ? Convert.ToDecimal(reader["YARD_FINES"]) : 0;
                           
                        }
                    }
                }
            }

            return View(model);
        }

     <div style="width:8%;">
                        <label class="form-label" style="margin-left:40px;">Source</label>
                        <select name="Source" class="form-control" onchange="document.getElementById('rawMaterialForm').submit();">
                            <option value="">Select Source</option>
                            <option value="RMBB_KNR" @(Model !=null && Model.Source == "RMBB_KNR" ? "selected" : "")>RMBB_KNR</option>
                            <option value="RMBB" @(Model != null && Model.Source == "RMBB" ? "selected" : "")>RMBB</option>
                            <option value="RMBBN" @(Model != null && Model.Source == "RMBBN" ? "selected" : "")>RMBBN</option>
                        </select>

                    </div>
                    <div style="width:8%;">
                        <label class="form-label" style="margin-left:40px;">Pile No</label>
                        <input class="form-control" type="text" value="@Model.PileNo" )>
                    </div>
