$(document).ready(function () {
        $('#date-daily1').datepicker({
            format: 'yyyy-mm-dd',
            autoclose: true,
            todayHighlight: true
        }).datepicker('update', new Date());
    });

    <div class="mb-2">
    <label for="date-daily1">Date:</label>
    <input type="text" id="date-daily1" class="form-control d-inline-block" style="width: 200px;" />
</div>
