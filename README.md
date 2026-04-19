function Dis_CTOFBFReportData(fDate) {
            $.ajax({
                url: '@Url.Action("GetCTOFBFReportDataByFurnace", "HML")',
                type: 'GET',
                data: { fDate: fDate },
                success: function (data) {
                    if (data.message) {
                        alert(data.message);
                        return;
                    }
                    data.forEach(function (item) {
                        if (item.FURNACE === "C") {
                            $("#CBF_Furnace").val(item.FURNACE);
                            $("#CBF_ActOnDate").val(item.ACT_ONDT);
                            $("#CBF_ActToDate").val(item.ACT_TODT);
                            $("#CBF_ReportOnDate").val(item.REPORT_ONDT);
                            $("#CBF_ReportToDate").val(item.REPORT_TODT);
                            $("#CBF_Balance").val(item.BALANCE);
                        }
                        if (item.FURNACE === "E") {
                            $("#EBF_Furnace").val(item.FURNACE);
                            $("#EBF_ActOnDate").val(item.ACT_ONDT);
                            $("#EBF_ActToDate").val(item.ACT_TODT);
                            $("#EBF_ReportOnDate").val(item.REPORT_ONDT);
                            $("#EBF_ReportToDate").val(item.REPORT_TODT);
                            $("#EBF_Balance").val(item.BALANCE);
                        }
                        if (item.FURNACE === "F") {
                            $("#FBF_Furnace").val(item.FURNACE);
                            $("#FBF_ActOnDate").val(item.ACT_ONDT);
                            $("#FBF_ActToDate").val(item.ACT_TODT);
                            $("#FBF_ReportOnDate").val(item.REPORT_ONDT);
                            $("#FBF_ReportToDate").val(item.REPORT_TODT);
                            $("#FBF_Balance").val(item.BALANCE);
                        }
                    });
                    Calc_AF_ActOnDate();
                    Calc_AG_ActOnDate();
                    Calc_AH_ActOnDate();
                    Calc_AI_ActOnDate();
                    Calc_AF_ActToDate();
                    Calc_AG_ActToDate();
                    Calc_AH_ActToDate();
                    Calc_AI_ActToDate();
                    Calc_AF_ReportOnDate();
                    Calc_AG_ReportOnDate();
                    Calc_AH_ReportOnDate();
                    Calc_AI_ReportOnDate();
                    Calc_AF_ReportToDate();
                    Calc_AG_ReportToDate();
                    Calc_AH_ReportToDate();
                    Calc_AI_ReportToDate();
                    Calc_AF_Balance();
                    Calc_AG_Balance();
                    Calc_AH_Balance();
                    Calc_AI_Balance();
                }
            });

        }
