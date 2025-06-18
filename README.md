 [HttpPost]
        public ActionResult RawMaterialEntry(RawMaterialQuantity input,string SaveRawMaterial)
        {
            RawMaterialQuantity model = new RawMaterialQuantity()
            {
                Source = input.Source,
                PileNo = input.PileNo

            };
            if (!string.IsNullOrEmpty(SaveRawMaterial))
            {
                using (OracleConnection conn = new OracleConnection(mycon))
                {
                    conn.Open();

                    using (OracleCommand cmd = new OracleCommand("Proc_Save_Pile_RawMat_Quantity_Entry", conn))
                    {
                        cmd.CommandType = CommandType.StoredProcedure;
                        cmd.Parameters.Add("P_PileNo", OracleDbType.Varchar2).Value = model.PileNo ?? "";
                        cmd.Parameters.Add("P_Source", OracleDbType.Varchar2).Value = model.Source ?? "";
                        cmd.Parameters.Add("P_NoaFines", OracleDbType.Decimal).Value = model.NoaFines ?? 0;
                        cmd.Parameters.Add("P_JodaFines", OracleDbType.Decimal).Value = model.JodaFines ?? 0;
                        cmd.Parameters.Add("P_KBFines", OracleDbType.Decimal).Value = model.KBFines ?? 0;
                        cmd.Parameters.Add("P_YardFines", OracleDbType.Decimal).Value = model.YardFines ?? 0;

                        cmd.ExecuteNonQuery();
                    }
                }

                ViewBag.Message = "Data Saved Successfully";
            }
