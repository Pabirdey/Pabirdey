<div class="input-group">
    <input type="text" id="StartDate" class="form-control" placeholder="Select Date" />
    <span class="input-group-text" id="calendarIcon">
        <i class="fa fa-calendar"></i> <!-- Font Awesome -->
    </span>
</div>
<i class="bi bi-calendar"></i> <!-- Bootstrap Icons -->
const fp = flatpickr("#StartDate", {
    enableTime: true,
    dateFormat: "d-M-Y H:i",
    time_24hr: true,
    defaultHour: 0
});

// Trigger calendar open when icon clicked
document.getElementById("calendarIcon").addEventListener("click", function () {
    fp.open();
});
<!-- Flatpickr CSS -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/flatpickr/dist/flatpickr.min.css">

<!-- Flatpickr JS -->
<script src="https://cdn.jsdelivr.net/npm/flatpickr"></script>

<!-- Font Awesome (optional) -->
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

<!-- Bootstrap Icons (optional) -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons/font/bootstrap-icons.css">
