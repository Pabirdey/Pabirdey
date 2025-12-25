 <script type="text/javascript">
    $(document).ready(function () {        
        var caldate1 = '@DateTime.Today.AddDays(-1).ToString("dd/MM/yyyy",new System.Globalization.CultureInfo("en-GB"))';
        $('#currDate-value').html(caldate1);
        $('#date-daily1').datepicker({
            format: "dd/mm/yyyy",
            autoclose: true,
            todayHighlight: true
        }).datepicker("setDate", caldate1);

        $('#date-daily1').on('changeDate', function () {
            caldate1 = $('#date-daily1').datepicker('getFormattedDate');
            $('#currDate-value').html(caldate1);
            var furnace = $("#ddlFurnace").val();
            Display_Material(furnace, caldate1);
        });

        
        $("#ddlFurnace").change(function () {
            var furnace = $("#ddlFurnace").val();            
            var fDate = $('#date-daily1').datepicker('getFormattedDate');
            Display_Material(furnace, fDate);
        });
        
        function Display_Material(furnace, fDate) {
            $.ajax({
                url: '@Url.Action("GetRawMaterialByFurnace","HML")',
                type: 'GET',
                data: { furnace: furnace, fdate: fDate },
                success: function (data) {
                    var tbody = $("#materialTable tbody");
                    tbody.empty();
                    for (var i = 0; i < data.length; i++) {
                        var row = "<tr>" +
                            "<td class='fw-bold'>" + data[i].MATERIAL + "</td>" +
                            "<td><input type='text' class='form-control large-textbox' value='" + data[i].VALUE_TON + "'></td>" +
                            "<td><input type='text' class='form-control large-textbox' value='" + data[i].VALUE_KG + "'></td>" +
                            "</tr>";
                        tbody.append(row);
                    }
                },
                error: function (xhr) {
                    alert("Error Occurred: " + xhr.responseText);
                }
            });
        }        
        Display_Material($("#ddlFurnace").val(), caldate1);
    });
</script>
