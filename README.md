function Display_BFReportData(fDate)
{
    $.ajax({

        url: '@Url.Action("GET_GBF_IBF_ACTUAL_REPORT", "BF")',

        type: 'GET',

        data: { prodDate: fDate },

        success: function (res)
        {
            if (!res.success)
            {
                alert(res.message);
                return;
            }

            res.data.Furnaces.forEach(function (item)
            {

                // G FURNACE

                if (item.FURNACE === "G")
                {
                    $("#GBF_Furnace").val(item.FURNACE);

                    $("#GBF_ActOnDate").val(item.ACTUAL);

                    $("#GBF_ActToDate").val(item.ACTUAL_TD);

                    $("#GBF_ReportOnDate").val(item.REPORTED);

                    $("#GBF_ReportToDate").val(item.REPORTED_TD);

                    $("#GBF_Balance").val(item.BALANCE);
                }


                // H FURNACE

                if (item.FURNACE === "H")
                {
                    $("#HBF_Furnace").val(item.FURNACE);

                    $("#HBF_ActOnDate").val(item.ACTUAL);

                    $("#HBF_ActToDate").val(item.ACTUAL_TD);

                    $("#HBF_ReportOnDate").val(item.REPORTED);

                    $("#HBF_ReportToDate").val(item.REPORTED_TD);

                    $("#HBF_Balance").val(item.BALANCE);
                }


                // I FURNACE

                if (item.FURNACE === "I")
                {
                    $("#IBF_Furnace").val(item.FURNACE);

                    $("#IBF_ActOnDate").val(item.ACTUAL);

                    $("#IBF_ActToDate").val(item.ACTUAL_TD);

                    $("#IBF_ReportOnDate").val(item.REPORTED);

                    $("#IBF_ReportToDate").val(item.REPORTED_TD);

                    $("#IBF_Balance").val(item.BALANCE);
                }

            });

        },

        error: function ()
        {
            alert("Error Loading Data");
        }

    });
}

<tr>

    <td>
        <input class="form-control"
               type="text"
               readonly
               id="GBF_Furnace" />
    </td>

    <td>
        <input class="form-control"
               type="text"
               readonly
               id="GBF_ActOnDate" />
    </td>

    <td>
        <input class="form-control"
               type="text"
               readonly
               id="GBF_ActToDate" />
    </td>

    <td>
        <input class="form-control"
               type="text"
               id="GBF_ReportOnDate" />
    </td>

    <td>
        <input class="form-control"
               type="text"
               readonly
               id="GBF_ReportToDate" />
    </td>

    <td>
        <input class="form-control"
               type="text"
               readonly
               id="GBF_Balance" />
    </td>

</tr>
