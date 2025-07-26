<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Cast House Details</title>

    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">

    <!-- Bootstrap Datepicker CSS -->
    <link href="https://cdnjs.cloudflare.com/ajax/libs/bootstrap-datepicker/1.10.0/css/bootstrap-datepicker3.min.css" rel="stylesheet"/>

    <!-- jQuery (required) -->
    <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>

    <!-- Bootstrap JS -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>

    <!-- Bootstrap Datepicker JS -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/bootstrap-datepicker/1.10.0/js/bootstrap-datepicker.min.js"></script>
</head>

<body>
    <div class="container-fluid mt-3">
        <div class="d-flex justify-content-between align-items-center mb-2">
            <h2>Cast House Details</h2>            
        </div>       

        <!-- Date Picker Input -->
        <div class="mb-3">
            <label for="date-daily1" class="form-label">Date:</label>
            <input type="text" id="date-daily1" class="form-control d-inline-block" style="width: 200px;" />                    
        </div>
    </div>

    <script>
        $(document).ready(function () {
            $('#date-daily1').datepicker({
                format: 'yyyy-mm-dd',
                autoclose: true,
                todayHighlight: true
            }).datepicker('update', new Date());
        });
    </script>
</body>
</html>
