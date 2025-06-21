using System.Collections.Generic;

[HttpPost]
public ActionResult RawMaterialEntry(RawMaterialQuantity input, string SaveRawMaterial)
{
    RawMaterialQuantity model = new RawMaterialQuantity();

    // STEP 1: Fetch Dropdown List Data (e.g., PileNo)
    List<string> pileList = new List<string>();
    using (OracleConnection conn = new OracleConnection(mycon))
    {
        conn.Open();
        string ddlQuery = "SELECT DISTINCT PILE_NO FROM imtg.T_PILE_RAWMAT_QUANTITY_NEW ORDER BY PILE_NO";
        using (OracleCommand cmd = new OracleCommand(ddlQuery, conn))
        {
            using (OracleDataReader reader = cmd.ExecuteReader())
            {
                while (reader.Read())
                {
                    pileList.Add(reader["PILE_NO"].ToString());
                }
            }
        }
    }
    ViewBag.PileList = pileList;

    // STEP 2: Save Logic
    if (!string.IsNullOrEmpty(SaveRawMaterial))
    {
        using (OracleConnection conn = new OracleConnection(mycon))
        {
            conn.Open();

            using (OracleCommand cmd = new OracleCommand("Proc_Save_Pile_RawMat_Quantity_Entry", conn))
            {
                cmd.CommandType = CommandType.StoredProcedure;
                cmd.Parameters.Add("P_PileNo", OracleDbType.Varchar2).Value = input.PileNo ?? "";
                cmd.Parameters.Add("P_Source", OracleDbType.Varchar2).Value = input.Source ?? "";
                cmd.Parameters.Add("P_NoaFines", OracleDbType.Decimal).Value = input.NoaFines ?? 0;
                cmd.Parameters.Add("P_JodaFines", OracleDbType.Decimal).Value = input.JodaFines ?? 0;
                cmd.Parameters.Add("P_KBFines", OracleDbType.Decimal).Value = input.KBFines ?? 0;
                cmd.Parameters.Add("P_YardFines", OracleDbType.Decimal).Value = input.YardFines ?? 0;

                cmd.ExecuteNonQuery();
            }
        }

        ViewBag.Message = "Data Saved Successfully";
        model = input;
    }
    // STEP 3: Retrieve Data if PileNo and Source Provided
    else if (!string.IsNullOrEmpty(input.PileNo) && !string.IsNullOrEmpty(input.Source))
    {
        using (OracleConnection conn = new OracleConnection(mycon))
        {
            conn.Open();
            string query = $"SELECT * FROM imtg.T_PILE_RAWMAT_QUANTITY_NEW WHERE PILE_NO ='{input.PileNo}' AND SOURCE ='{input.Source}'";
            using (OracleCommand cmd = new OracleCommand(query, conn))
            {
                using (OracleDataReader reader = cmd.ExecuteReader())
                {
                    if (reader.Read())
                    {
                        model.PileNo = input.PileNo;
                        model.Source = input.Source;
                        model.StartDate = reader["PREP_START_DATE"] == DBNull.Value ? (DateTime?)null : Convert.ToDateTime(reader["PREP_START_DATE"]);
                        model.EndDate = reader["PREP_END_DATE"] == DBNull.Value ? (DateTime?)null : Convert.ToDateTime(reader["PREP_END_DATE"]);
                        model.ConsStartDate = reader["CONS_ST_DATE"] == DBNull.Value ? (DateTime?)null : Convert.ToDateTime(reader["CONS_ST_DATE"]);
                        model.NoaFines = reader["NOA_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["NOA_FINES"]);
                        model.JodaFines = reader["JODA_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["JODA_FINES"]);
                        model.KBFines = reader["KB_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["KB_FINES"]);
                        model.YardFines = reader["YARD_FINES"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["YARD_FINES"]);
                        model.BHJ = reader["BHJ"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["BHJ"]);
                        model.Namisa = reader["IO_NAMISA"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["IO_NAMISA"]);
                        model.FortescueBF = reader["IO_FORTESCUE_BF"] == DBNull.Value ? (decimal?)null : Convert.ToDecimal(reader["IO_FORTESCUE_BF"]);
                    }
                }
            }
        }
    }

    return View(model);
}

<script>
    // Convert server data (passed via ViewBag) to JS array
    var pileList = @Html.Raw(Newtonsoft.Json.JsonConvert.SerializeObject(ViewBag.PileList));
</script>

<select id="pileDropdown" name="PileNo">
    <script>
        for (var i = 0; i < pileList.length; i++) {
            document.write("<option value='" + pileList[i] + "'>" + pileList[i] + "</option>");
        }
    </script>
</select>
