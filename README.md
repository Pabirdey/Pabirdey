<!-- Add in <head> or top of your view -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/flatpickr/dist/flatpickr.min.css">

<!-- Add before closing </body> -->
<script src="https://cdn.jsdelivr.net/npm/flatpickr"></script>

<input type="text" id="StartDate" name="StartDate" class="form-control" 
       value="@Model.StartDate.HasValue ? Model.StartDate.Value.ToString("yyyy-MM-dd HH:mm") : """ />


<script>
    flatpickr("#StartDate", {
        enableTime: true,
        dateFormat: "Y-m-d H:i",
        time_24hr: true
    });

    flatpickr("#EndDate", {
        enableTime: true,
        dateFormat: "Y-m-d H:i",
        time_24hr: true
    });

    flatpickr("#ConsStartDate", {
        enableTime: true,
        dateFormat: "Y-m-d H:i",
        time_24hr: true
    });
</script>

