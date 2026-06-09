function GetDateTime(timeStr) {

    var shift = $("#ddlShift").val();
    var dateStr = $("#txtDate").val();

    var dt = new Date(dateStr);

    // Example: "11:20 PM"
    var parts = timeStr.split(' ');

    var timePart = parts[0];
    var ampm = parts[1];

    var arr = timePart.split(':');

    var hh = parseInt(arr[0]);
    var mm = parseInt(arr[1]);

    // Convert to 24 hour
    if (ampm === "PM" && hh < 12)
        hh += 12;

    if (ampm === "AM" && hh === 12)
        hh = 0;

    // Shift C logic
    if (shift === "C" && hh < 6)
        dt.setDate(dt.getDate() + 1);

    dt.setHours(hh, mm, 0, 0);

    return dt;
}