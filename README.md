function SaveCastHouseData() {
    debugger;
    var rows = document.querySelectorAll("#TAP_Hot_Metal_Details tbody tr,#Driling_Slag_Details tbody tr");
    var CastHouse = [];

    rows.forEach(function (row) {
        var rowData = {};
        var inputs = row.querySelectorAll("input, select");
        inputs.forEach(function (input) {
            let val = input.value.trim();
            rowData[input.name] = val === "" ? null : val; // Empty → null
        });
        CastHouse.push(rowData);
    });

    var selectedDate = document.getElementById("tbFDatePick").value.trim();
    var selectedFurnace = document.getElementById("lstFur").value.trim();

    console.log(CastHouse);
    console.log(selectedDate);
    console.log(selectedFurnace);

    $.ajax({
        url: '/CastHouse/SaveCastHouseData',
        type: 'POST',
        contentType: 'application/json',
        data: JSON.stringify({
            data: CastHouse,
            Fdate: selectedDate,
            Fur: selectedFurnace
        }),
        success: function (response) {
            if (response.success) {
                Swal.fire({
                    icon: 'success',
                    text: 'Data Saved successfully!',
                    showConfirmButton: true,
                    customClass: {
                        popup: 'my-swal-popup',
                        title: 'my-swal-title',
                        htmlContainer: 'my-swal-text'
                    }
                });
            } else {
                Swal.fire({
                    icon: 'error',
                    title: 'Failed!',
                    text: response.message || 'Data could not be saved. Please try again.'
                });
            }
        },
        error: function () {
            Swal.fire({
                icon: 'error',
                title: 'Error!',
                text: 'Something went wrong while saving.'
            });
        }
    });
}


[HttpPost]
public JsonResult SaveCastHouseData(List<Dictionary<string, object>> data, string Fdate, string Fur)
{
    try
    {
        using (OracleConnection conn = new OracleConnection(iMonitorWebUtils.msConRWString))
        {
            conn.Open();

            string updateSql = @"
                UPDATE TEST.T_CAST_DETAILS SET
                    ch_ready_time = :ch_ready_time, 
                    splacing_wetness_time = :splacing_wetness_time,
                    cast_type = :cast_type,
                    cast_clay_cond = :cast_clay_cond,
                    taphole_behaviour = :taphole_behaviour,
                    hm_before_slag = :hm_before_slag,
                    hm_after_slag = :hm_after_slag,
                    hm_temp = :hm_temp 
                WHERE cast_no = :cast_no 
                  AND TRUNC(DATE_TIME) = TO_DATE(:Fdate, 'DD-MM-YYYY') 
                  AND FUR_NAME = :Fur";

            foreach (var row in data)
            {
                using (OracleCommand cmd = new OracleCommand(updateSql, conn))
                {
                    cmd.Parameters.Add(":ch_ready_time", row["ch_ready_time"] ?? DBNull.Value);
                    cmd.Parameters.Add(":splacing_wetness_time", row["splacing_wetness_time"] ?? DBNull.Value);
                    cmd.Parameters.Add(":cast_type", row["cast_type"] ?? DBNull.Value);
                    cmd.Parameters.Add(":cast_clay_cond", row["cast_clay_cond"] ?? DBNull.Value);
                    cmd.Parameters.Add(":taphole_behaviour", row["taphole_behaviour"] ?? DBNull.Value);
                    cmd.Parameters.Add(":hm_before_slag", row["hm_before_slag"] ?? DBNull.Value);
                    cmd.Parameters.Add(":hm_after_slag", row["hm_after_slag"] ?? DBNull.Value);
                    cmd.Parameters.Add(":hm_temp", row["hm_temp"] ?? DBNull.Value);
                    cmd.Parameters.Add(":cast_no", row["cast_no"] ?? DBNull.Value);
                    cmd.Parameters.Add(":Fdate", Fdate);
                    cmd.Parameters.Add(":Fur", Fur);

                    cmd.ExecuteNonQuery();
                }
            }
        }

        return Json(new { success = true });
    }
    catch (Exception ex)
    {
        return Json(new { success = false, message = ex.Message });
    }
}