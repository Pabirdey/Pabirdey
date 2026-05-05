Alright — here is your complete working backend code (ASP.NET MVC + Oracle) for saving:
✔ Main table (Coke Unloading)
✔ Tonnage of Coke
✔ Tonnage of Nut Coke
✔ Insert + Update using MERGE
✔ No Type field (separate lists)
✅ 🔥 FULL CONTROLLER CODE
C#
[HttpPost]
public JsonResult SaveData(SaveModel model)
{
    using (OracleConnection con = new OracleConnection("YOUR_CONNECTION"))
    {
        con.Open();

        OracleTransaction trans = con.BeginTransaction();

        try
        {
            // ============================
            // 🔷 MAIN TABLE SAVE
            // ============================
            foreach (var item in model.main)
            {
                string query = @"
                MERGE INTO T_COKE_MAIN t
                USING dual
                ON (t.TDATE = TO_DATE(:TDATE,'DD/MM/YYYY') 
                    AND t.SHIFT = :SHIFT 
                    AND t.BUNKER = :BUNKER)

                WHEN MATCHED THEN
                    UPDATE SET 
                        t.C_BF = :C,
                        t.E_BF = :E,
                        t.F_BF = :F,
                        t.TOTAL = :TOTAL,
                        t.POSITION = :POSITION,
                        t.BALANCE = :BALANCE

                WHEN NOT MATCHED THEN
                    INSERT (TDATE, SHIFT, BUNKER, C_BF, E_BF, F_BF, TOTAL, POSITION, BALANCE)
                    VALUES (TO_DATE(:TDATE,'DD/MM/YYYY'), :SHIFT, :BUNKER, :C, :E, :F, :TOTAL, :POSITION, :BALANCE)";

                using (OracleCommand cmd = new OracleCommand(query, con))
                {
                    cmd.Transaction = trans;

                    cmd.Parameters.Add("TDATE", item.Date);
                    cmd.Parameters.Add("SHIFT", item.Shift);
                    cmd.Parameters.Add("BUNKER", item.Bunker);

                    cmd.Parameters.Add("C", string.IsNullOrEmpty(item.C) ? "0" : item.C);
                    cmd.Parameters.Add("E", string.IsNullOrEmpty(item.E) ? "0" : item.E);
                    cmd.Parameters.Add("F", string.IsNullOrEmpty(item.F) ? "0" : item.F);
                    cmd.Parameters.Add("TOTAL", string.IsNullOrEmpty(item.Total) ? "0" : item.Total);

                    cmd.Parameters.Add("POSITION", string.IsNullOrEmpty(item.Position) ? "0" : item.Position);
                    cmd.Parameters.Add("BALANCE", string.IsNullOrEmpty(item.Balance) ? "0" : item.Balance);

                    cmd.ExecuteNonQuery();
                }
            }

            // ============================
            // 🔷 COKE TONNAGE SAVE
            // ============================
            foreach (var item in model.coke)
            {
                string query = @"
                MERGE INTO T_COKE_TONNAGE t
                USING dual
                ON (t.BUNKER = :BUNKER AND t.TYPE = 'COKE')

                WHEN MATCHED THEN
                    UPDATE SET 
                        t.C_BF = :C,
                        t.E_BF = :E,
                        t.F_BF = :F,
                        t.TOTAL = :TOTAL

                WHEN NOT MATCHED THEN
                    INSERT (BUNKER, C_BF, E_BF, F_BF, TOTAL, TYPE)
                    VALUES (:BUNKER, :C, :E, :F, :TOTAL, 'COKE')";

                using (OracleCommand cmd = new OracleCommand(query, con))
                {
                    cmd.Transaction = trans;

                    cmd.Parameters.Add("BUNKER", item.Bunker);
                    cmd.Parameters.Add("C", string.IsNullOrEmpty(item.C) ? "0" : item.C);
                    cmd.Parameters.Add("E", string.IsNullOrEmpty(item.E) ? "0" : item.E);
                    cmd.Parameters.Add("F", string.IsNullOrEmpty(item.F) ? "0" : item.F);
                    cmd.Parameters.Add("TOTAL", string.IsNullOrEmpty(item.Total) ? "0" : item.Total);

                    cmd.ExecuteNonQuery();
                }
            }

            // ============================
            // 🔷 NUT TONNAGE SAVE
            // ============================
            foreach (var item in model.nut)
            {
                string query = @"
                MERGE INTO T_COKE_TONNAGE t
                USING dual
                ON (t.BUNKER = :BUNKER AND t.TYPE = 'NUT')

                WHEN MATCHED THEN
                    UPDATE SET 
                        t.C_BF = :C,
                        t.E_BF = :E,
                        t.F_BF = :F,
                        t.TOTAL = :TOTAL

                WHEN NOT MATCHED THEN
                    INSERT (BUNKER, C_BF, E_BF, F_BF, TOTAL, TYPE)
                    VALUES (:BUNKER, :C, :E, :F, :TOTAL, 'NUT')";

                using (OracleCommand cmd = new OracleCommand(query, con))
                {
                    cmd.Transaction = trans;

                    cmd.Parameters.Add("BUNKER", item.Bunker);
                    cmd.Parameters.Add("C", string.IsNullOrEmpty(item.C) ? "0" : item.C);
                    cmd.Parameters.Add("E", string.IsNullOrEmpty(item.E) ? "0" : item.E);
                    cmd.Parameters.Add("F", string.IsNullOrEmpty(item.F) ? "0" : item.F);
                    cmd.Parameters.Add("TOTAL", string.IsNullOrEmpty(item.Total) ? "0" : item.Total);

                    cmd.ExecuteNonQuery();
                }
            }

            // ✅ COMMIT
            trans.Commit();

            return Json("Success");
        }
        catch (Exception ex)
        {
            trans.Rollback();
            return Json("Error: " + ex.Message);
        }
    }
}
✅ 🔥 MODEL CLASSES
C#
public class SaveModel
{
    public List<MainData> main { get; set; }
    public List<TonnageData> coke { get; set; }
    public List<TonnageData> nut { get; set; }
}

public class MainData
{
    public string Date { get; set; }
    public string Shift { get; set; }
    public string Bunker { get; set; }

    public string C { get; set; }
    public string E { get; set; }
    public string F { get; set; }

    public string Total { get; set; }
    public string Position { get; set; }
    public string Balance { get; set; }
}

public class TonnageData
{
    public string Bunker { get; set; }

    public string C { get; set; }
    public string E { get; set; }
    public string F { get; set; }

    public string Total { get; set; }
}
✅ 🔥 Oracle Tables (Example)
SQL
-- MAIN TABLE
CREATE TABLE T_COKE_MAIN (
    TDATE DATE,
    SHIFT VARCHAR2(5),
    BUNKER VARCHAR2(50),
    C_BF NUMBER,
    E_BF NUMBER,
    F_BF NUMBER,
    TOTAL NUMBER,
    POSITION NUMBER,
    BALANCE NUMBER
);

-- TONNAGE TABLE
CREATE TABLE T_COKE_TONNAGE (
    BUNKER VARCHAR2(50),
    C_BF NUMBER,
    E_BF NUMBER,
    F_BF NUMBER,
    TOTAL NUMBER,
    TYPE VARCHAR2(10)
);
🔥 FINAL RESULT
✔ Save from your UI (image)
✔ 3 sections handled separately
✔ Insert + Update (MERGE)
✔ Transaction safe (commit/rollback)
✔ No duplicate data
🚀 Next (Recommended)
If you want I can help you:
✅ Load same data back into UI (Edit mode)
✅ Add validation (no empty bunker save)
✅ Highlight changed rows before save
✅ Performance optimization (bulk insert)
Just tell 👍