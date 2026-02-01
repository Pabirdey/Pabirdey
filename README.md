<script>
function SaveExceptionCast() {
    debugger;

    // Get furnace value
    var furnace = $('#lstFur').val();
    if (!furnace) {
        alert("Please select a furnace!");
        return;
    }

    // Get all rows from table body
    var rows = document.querySelectorAll("#exception_cast tbody tr");
    var dataList = [];

    for (var i = 0; i < rows.length; i++) {
        var r = rows[i];

        // Grab values safely
        var id = r.querySelector(".idno") ? r.querySelector(".idno").value.trim() : null;
        var tapholeNo = r.querySelector(".TapholeNo") ? r.querySelector(".TapholeNo").value.trim() : null;
        var date = r.querySelector(".ExceptionDate") ? r.querySelector(".ExceptionDate").value.trim() : null;
        var hh = r.querySelector(".hh") ? r.querySelector(".hh").value.trim() : "00";
        var mm = r.querySelector(".mm") ? r.querySelector(".mm").value.trim() : "00";
        var tapLen = r.querySelector(".TapholeLength") ? r.querySelector(".TapholeLength").value.trim() : null;
        var clay = r.querySelector(".Clay") ? r.querySelector(".Clay").value.trim() : null;
        var type = r.querySelector(".Type") ? r.querySelector(".Type").value.trim() : null;

        // Skip row if mandatory fields are missing
        if (!id || !date) continue;

        // Push object to array
        dataList.push({
            FURNACE: furnace,
            ID_NO: id,
            TAPHOLE_NO: tapholeNo,
            EXCEPTION_DATE: date,
            HH24: hh,
            MM: mm,
            TAPHOLE_LENGTH: tapLen,
            CLAY_PAUSED: clay,
            TYPE: type
        });
    }

    // Debug: show data in console before sending
    console.log("Sending data to controller:", dataList);

    // Send AJAX request
    $.ajax({
        url: "/CastHouse/Save_Exception_Cast",
        type: "POST",
        data: JSON.stringify(dataList),
        contentType: "application/json",
        success: function (res) {
            alert(res);
            console.log("Server response:", res);
        },
        error: function (xhr, status, error) {
            alert("Error while saving");
            console.error("AJAX error:", status, error, xhr.responseText);
        }
    });
}
</script>
