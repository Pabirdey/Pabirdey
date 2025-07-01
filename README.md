<!-- Include Flatpickr CSS & JS (if not already included) -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/flatpickr/dist/flatpickr.min.css">
<script src="https://cdn.jsdelivr.net/npm/flatpickr"></script>

<!-- Font Awesome for the calendar icon -->
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">

<!-- Your updated form field -->
<div style="width: 12%; position: relative;">
    <label class="form-label fw-bold" style="margin-left: 40px;">Start Date</label>
    
    <input type="text" class="form-control" name="StartDate" id="StartDate"
           value="@(Model.StartDate.HasValue ? Model.StartDate.Value.ToString("dd-MMM-yyyy HH:mm") : "")"
           style="padding-left: 35px;" />
    
    <!-- Calendar icon inside input -->
    <i class="fa fa-calendar" style="
        position: absolute;
        left: 10px;
        top: 55%;
        transform: translateY(-50%);
        color: #888;"></i>
</div>

<!-- Flatpickr script -->
<script>
    flatpickr("#StartDate", {
        enableTime: true,
        dateFormat: "d-M-Y H:i"
    });
</script>