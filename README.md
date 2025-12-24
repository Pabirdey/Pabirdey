<script type="text/javascript">        
    $(document).ready(function () {
        var caldate1 = '@DateTime.Today.AddDays(-1).ToString("dd/MM/yyyy", new System.Globalization.CultureInfo("en-GB"))';                
        $('#currDate-value').html(caldate1);        
        $('#date-daily1').datepicker({
            format: "dd/mm/yyyy",
            autoclose: true,
            todayHighlight: true,
            changeMonth: true,
            changeYear: true,
            setDate: caldate1,
        });
        $('#date-daily1').on('changeDate', function (){            
            var getFormattedDate = $('#date-daily1').datepicker('getFormattedDate');
            $('#currDate-value').html(getFormattedDate);
            caldate1 = $('#date-daily1').datepicker('getFormattedDate');                     
            $('#currDate-value').html(caldate1);            
        });  
        function Display_Material(furnaceName,fDate) {
            $.ajax({
                url: '/HML/GetMaterialsByFurnace',
                type: 'GET',
                data: { pfurnace: furnaceName,pdate:fDate },
                success: function (data) {
                    var tbody = $("#materialTable tbody");
                    tbody.empty();
                    for (var i = 0; i < data.length; i++) {
                        var row = "<tr>" +
                            "<td class='fw-bold'>" + data[i].MATERIAL + "</td>" +
                            "<td><input type='text' class='form-control medium-textbox shadow-sm' value='" + data[i].VALUE_TON + "'></td>" +
                            "<td><input type='text' class='form-control medium-textbox shadow-sm' value='" + data[i].VALUE_KG + "'></td>" +
                            "</tr>";
                        tbody.append(row);
                    }
                }
            });
        }
    });   // docuemnt.ready closed
    </script>
