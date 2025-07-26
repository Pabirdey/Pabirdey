<!DOCTYPE html>
<html>
<head>
    <title>Datepicker Test</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap-datepicker@1.10.0/dist/css/bootstrap-datepicker.min.css" rel="stylesheet">
</head>
<body>
    <div class="container mt-5">
        <input type="text" id="myDate" class="form-control" placeholder="Select Date">
    </div>

    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap-datepicker@1.10.0/dist/js/bootstrap-datepicker.min.js"></script>
    <script>
        $(document).ready(function () {
            $('#myDate').datepicker({
                format: 'dd/mm/yyyy',
                autoclose: true
            });
        });
    </script>
</body>
</html>
