
@section css {
    <link rel="stylesheet" href="@Url.Content("~/bower_components/bootstrap/dist/css/bootstrap.min.css")">
    <link rel="stylesheet" href="@Url.Content("~/bower_components/bootstrap-datepicker/dist/css/bootstrap-datepicker3.standalone.min.css")" media="screen">
<style>
    body {
        background-color: #f4f6f9;
    }

    .page-title {
        font-weight: 600;
        color: #2c3e50;
    }

    .card-box {
        background: #ffffff;
        padding: 20px;
        border-radius: 14px;
        box-shadow: 0 4px 12px rgba(0,0,0,0.10);
    }

    table {
        background: white;
        border-radius: 10px;
        overflow: hidden;
    }

    thead {
        background: #2c3e50;
        color: white;
    }

    .table tbody tr:hover {
        background: #f1f1f1;
    }

    .medium-textbox {
        width: 80px;
        max-width: 80px;
        text-align: right;
    }

    .btn-custom {
        padding-left: 35px;
        padding-right: 35px;
        font-size: 16px;
        border-radius: 8px;
    }
</style>

}
<div class="app-content">    
    @Html.Partial("_Header")    
    <div class="main-content">
        <div class="container mt-5">
            <div class="card-box">
                <h3 class="text-center page-title mb-4">Raw Material Consumption</h3>
                <!-- Date & Furnace Row -->
                <div class="row mb-4">
                    <div class="col-md-3">
                        <label class="form-label fw-bold">Date</label>
                        <a id="date-daily1" class="drpickr btn btn-o btn-primary">
                            <i class="fa fa-calendar"></i> <label class="value" id="currDate-value" style="font-size:20px;color:blue"></label>
                        </a>
                    </div>
                    <div class="col-md-3">
                        <label class="form-label fw-bold">Furnace</label>
                        <select class="form-select shadow-sm">
                            <option>C</option>
                            <option>E</option>
                            <option>F</option>
                        </select>
                    </div>
                </div>
                <!-- Table -->
                <table id="materialTable" class="table table-bordered shadow-sm">
                    <thead>
                        <tr>
                            <th>Material</th>
                            <th>Value (Tons)</th>
                            <th>Value (Kgs)</th>
                        </tr>
                    </thead>
                    <tbody></tbody>
                </table>
                <!-- Buttons -->
                <div class="mt-4">
                    <button class="btn btn-primary btn-custom me-2">Save</button>
                    <button class="btn btn-secondary btn-custom">Back</button>
                </div>
            </div>
        </div>
    </div>
    
</div>
@section scripts {
    <script src="@Url.Content("~/bower_components/jquery/dist/jquery.min.js")"></script>
    <script src="@Url.Content("~/bower_components/bootstrap/dist/js/bootstrap.min.js")"></script>
    <script src="@Url.Content("~/bower_components/components-modernizr/modernizr.js")"></script>
    <script src="@Url.Content("~/bower_components/moment/moment.min.js")"></script>
    <script src="@Url.Content("~/bower_components/bootstrap-datepicker/dist/js/bootstrap-datepicker.min.js")"></script>        
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

    });   // docuemnt.ready closed


     

       

    </script>
}


