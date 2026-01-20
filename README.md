@{
    ViewBag.Title = "Carbon Paste Injection";
}

<!-- ===== Furnace Dropdown ===== -->
<select id="lstFur">
    <option value="FUR1">FUR1</option>
    <option value="FUR2">FUR2</option>
</select>

<table id="carbon_paste_inj" border="1">

<thead>
<tr>
    <th>Date</th>
    <th>Shift</th>
    <th>Below Tuyere</th>
    <th>No of Drum</th>
</tr>
</thead>

<tbody>

<tr>
<td><input name="DATE_TIME" value="20-JAN-2026" /></td>
<td><input name="SHIFT" value="A" /></td>
<td><input name="BELOW_TUYERE" value="10" /></td>
<td><input name="NO_OF_DRUM" value="5" /></td>
</tr>

<tr>
<td><input name="DATE_TIME" value="20-JAN-2026" /></td>
<td><input name="SHIFT" value="B" /></td>
<td><input name="BELOW_TUYERE" value="15" /></td>
<td><input name="NO_OF_DRUM" value="6" /></td>
</tr>

</tbody>
</table>

<button onclick="saveCarbonPaste()">SAVE</button>

<input type="hidden" id="saveUrl"
 value="@Url.Action("SaveCarbonPaste", "CastHouse")" />

<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>

<script>

function saveCarbonPaste() {

    var url = document.getElementById("saveUrl").value;

    var rows =
      document.querySelectorAll("#carbon_paste_inj tbody tr");

    for (var i = 0; i < rows.length; i++) {

        var dt =
          rows[i].querySelector("[name='DATE_TIME']").value;

        var shift =
          rows[i].querySelector("[name='SHIFT']").value;

        var tuyere =
          rows[i].querySelector("[name='BELOW_TUYERE']").value;

        var drum =
          rows[i].querySelector("[name='NO_OF_DRUM']").value;

        var selectedFurnace =
          document.getElementById("lstFur").value.trim();

        $.ajax({

            url: url,
            type: 'POST',

            contentType:
            "application/x-www-form-urlencoded; charset=UTF-8",

            data: {
                DATE_TIME: dt,
                SHIFT: shift,
                BELOW_TUYERE: tuyere,
                NO_OF_DRUM: drum,
                FUR: selectedFurnace
            },

            success: function (res) {
                console.log("Saved => " + res);
            },

            error: function (err) {
                console.log(err);
                alert("Controller not hit");
            }
        });
    }

    alert("Saved Successfully!");
}

</script>


using Oracle.ManagedDataAccess.Client;

[HttpPost]
public string SaveCarbonPaste(
    string DATE_TIME,
    string SHIFT,
    string BELOW_TUYERE,
    string NO_OF_DRUM,
    string FUR)
{
    OracleConnection con =
      new OracleConnection(iMonitorWebUtils.msConRWString);

    con.Open();

    // ===== UPDATE =====
    string updateSql = @"
    UPDATE TEST.T_FUR_CARBON_PASTE_INJECTION
    SET
        BELOW_TUYERE = :BELOW_TUYERE,
        NO_OF_DRUM = :NO_OF_DRUM
    WHERE TO_CHAR(DATE_TIME,'DD-MON-YYYY') = :DATE_TIME
    AND SHIFT = :SHIFT
    AND FUR_NAME = :FUR";

    OracleCommand upCmd =
        new OracleCommand(updateSql, con);

    upCmd.Parameters.Add(":BELOW_TUYERE",
        OracleDbType.Varchar2).Value =
        string.IsNullOrEmpty(BELOW_TUYERE)
        ? (object)DBNull.Value : BELOW_TUYERE;

    upCmd.Parameters.Add(":NO_OF_DRUM",
        OracleDbType.Varchar2).Value =
        string.IsNullOrEmpty(NO_OF_DRUM)
        ? (object)DBNull.Value : NO_OF_DRUM;

    upCmd.Parameters.Add(":DATE_TIME",
        OracleDbType.Varchar2).Value = DATE_TIME;

    upCmd.Parameters.Add(":SHIFT",
        OracleDbType.Varchar2).Value = SHIFT;

    upCmd.Parameters.Add(":FUR",
        OracleDbType.Varchar2).Value = FUR;

    int rows = upCmd.ExecuteNonQuery();

    // ===== INSERT =====
    if (rows == 0)
    {
        string insertSql = @"
        INSERT INTO TEST.T_FUR_CARBON_PASTE_INJECTION
        (DATE_TIME, SHIFT, FUR_NAME,
         BELOW_TUYERE, NO_OF_DRUM)

        VALUES
        (TO_DATE(:DATE_TIME,'DD-MON-YYYY'),
         :SHIFT, :FUR,
         :BELOW_TUYERE, :NO_OF_DRUM)";

        OracleCommand inCmd =
            new OracleCommand(insertSql, con);

        inCmd.Parameters.Add(":DATE_TIME",
            OracleDbType.Varchar2).Value = DATE_TIME;

        inCmd.Parameters.Add(":SHIFT",
            OracleDbType.Varchar2).Value = SHIFT;

        inCmd.Parameters.Add(":FUR",
            OracleDbType.Varchar2).Value = FUR;

        inCmd.Parameters.Add(":BELOW_TUYERE",
            OracleDbType.Varchar2).Value =
            string.IsNullOrEmpty(BELOW_TUYERE)
            ? (object)DBNull.Value : BELOW_TUYERE;

        inCmd.Parameters.Add(":NO_OF_DRUM",
            OracleDbType.Varchar2).Value =
            string.IsNullOrEmpty(NO_OF_DRUM)
            ? (object)DBNull.Value : NO_OF_DRUM;

        inCmd.ExecuteNonQuery();
    }

    con.Close();

    return "OK";
}