public JsonResult GetPlantData(string date)
{
    var list = new List<object>();

    string[] plants = { "C", "E", "F", "G", "H", "I" }; // adjust if needed

    using (OracleConnection con = new OracleConnection("YOUR_CONNECTION_STRING"))
    {
        con.Open();

        foreach (var plant in plants)
        {
            // ================= COUNT CHECK =================
            string countQuery = @"
                SELECT COUNT(*)
                FROM DEMO.T_LADLE
                WHERE TRUNC(DATE_TIME) = TO_DATE(:pDate,'DD-MON-YYYY')
                AND PLANT = :pPlant";

            int count = 0;

            using (OracleCommand cmd = new OracleCommand(countQuery, con))
            {
                cmd.Parameters.Add("pDate", date);
                cmd.Parameters.Add("pPlant", plant);

                count = Convert.ToInt32(cmd.ExecuteScalar());
            }

            // ================= IF NO DATA =================
            if (count == 0)
            {
                string dataQuery = @"
                    SELECT DATE_TIME, PLANT,
                           LD1_TONS, LD2_TONS, LD3_TONS, MRDTP_TONS,
                           NOOFTP,
                           LD1_TONS_ACTUAL, LD2_TONS_ACTUAL,
                           LD3_TONS_ACTUAL, MRDTP_TONS_ACTUAL
                    FROM DEMO.T_LADLE
                    WHERE TRUNC(DATE_TIME) = TO_DATE(:pDate,'DD-MON-YYYY')
                    AND PLANT = :pPlant";

                using (OracleCommand cmd = new OracleCommand(dataQuery, con))
                {
                    cmd.Parameters.Add("pDate", date);
                    cmd.Parameters.Add("pPlant", plant);

                    using (OracleDataReader dr = cmd.ExecuteReader())
                    {
                        while (dr.Read())
                        {
                            list.Add(new
                            {
                                PLANT = dr["PLANT"].ToString(),
                                DATE_TIME = dr["DATE_TIME"].ToString(),

                                LD1 = dr["LD1_TONS"],
                                LD2 = dr["LD2_TONS"],
                                LD3 = dr["LD3_TONS"],
                                MRDTP = dr["MRDTP_TONS"],
                                NOOFTP = dr["NOOFTP"],

                                LD1_ACT = dr["LD1_TONS_ACTUAL"],
                                LD2_ACT = dr["LD2_TONS_ACTUAL"],
                                LD3_ACT = dr["LD3_TONS_ACTUAL"],
                                MRDTP_ACT = dr["MRDTP_TONS_ACTUAL"]
                            });
                        }
                    }
                }
            }
        }
    }

    return Json(list, JsonRequestBehavior.AllowGet);
}