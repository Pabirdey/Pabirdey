function LoadCokeData() {
    $.ajax({
        url: '/Furnace_High_line/GetCokeData',
        type: 'GET',
        data: {
            sDate: $("#hiddenDate").val(),
            sShift: $("#ddlshift").val()
        },

        success: function (res) {
            $("#txtWestern")
                .val(res.STOCK_COKE);
            $("#txtMiddle")
                .val(res.BEHIVE_COKE);
            $("#txtEastern")
                .val(res.STOCK_EASTERN);
        },

        error: function () {
            alert("Error Loading Data");
        }
    });
}
public JsonResult GetCokeData(
    string sDate,
    string sShift)
{
    decimal STOCK_COKE = 0;
    decimal BEHIVE_COKE = 0;
    decimal STOCK_EASTERN = 0;

    using (OracleConnection con =
        new OracleConnection(
            iMonitorWebUtils.msConRWString))
    {
        con.Open();

        // =========================
        // WESTERN
        // =========================

        try
        {
            string q1 = @"
            SELECT NVL(STOCK_COKE,0)
            FROM T_BF_CK_CONTROL_UNLOADING
            WHERE TIMESTAMP =
            TO_DATE(:sDate,'DD/MM/YYYY')
            AND SHIFT = :sShift
            AND BUNKER = 'WESTERN'";

            OracleCommand cmd1 =
                new OracleCommand(q1, con);

            cmd1.Parameters.Add(
                "sDate",
                OracleDbType.Varchar2)
                .Value = sDate;

            cmd1.Parameters.Add(
                "sShift",
                OracleDbType.Varchar2)
                .Value = sShift;

            object obj1 =
                cmd1.ExecuteScalar();

            if (obj1 != null)
            {
                STOCK_COKE =
                    Convert.ToDecimal(obj1);
            }
        }

        catch
        {
            STOCK_COKE = 0;
        }

        // =========================
        // MIDDLE
        // =========================

        try
        {
            string q2 = @"
            SELECT NVL(BEHIVE_COKE,0)
            FROM T_BF_CK_CONTROL_UNLOADING
            WHERE TIMESTAMP =
            TO_DATE(:sDate,'DD/MM/YYYY')
            AND SHIFT = :sShift
            AND BUNKER = 'MIDDLE'";

            OracleCommand cmd2 =
                new OracleCommand(q2, con);

            cmd2.Parameters.Add(
                "sDate",
                OracleDbType.Varchar2)
                .Value = sDate;

            cmd2.Parameters.Add(
                "sShift",
                OracleDbType.Varchar2)
                .Value = sShift;

            object obj2 =
                cmd2.ExecuteScalar();

            if (obj2 != null)
            {
                BEHIVE_COKE =
                    Convert.ToDecimal(obj2);
            }
        }

        catch
        {
            BEHIVE_COKE = 0;
        }

        // =========================
        // EASTERN
        // =========================

        try
        {
            string q3 = @"
            SELECT NVL(STOCK_COKE,0)
            FROM T_BF_CK_CONTROL_UNLOADING
            WHERE TIMESTAMP =
            TO_DATE(:sDate,'DD/MM/YYYY')
            AND SHIFT = :sShift
            AND BUNKER = 'EASTERN'";

            OracleCommand cmd3 =
                new OracleCommand(q3, con);

            cmd3.Parameters.Add(
                "sDate",
                OracleDbType.Varchar2)
                .Value = sDate;

            cmd3.Parameters.Add(
                "sShift",
                OracleDbType.Varchar2)
                .Value = sShift;

            object obj3 =
                cmd3.ExecuteScalar();

            if (obj3 != null)
            {
                STOCK_EASTERN =
                    Convert.ToDecimal(obj3);
            }
        }

        catch
        {
            STOCK_EASTERN = 0;
        }

        // =========================
        // RETURN JSON
        // =========================

        return Json(new
        {
            STOCK_COKE = STOCK_COKE,
            BEHIVE_COKE = BEHIVE_COKE,
            STOCK_EASTERN = STOCK_EASTERN
        },
        JsonRequestBehavior.AllowGet);
    }
}
