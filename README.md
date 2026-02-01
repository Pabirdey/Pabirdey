<script>
function SaveExceptionCast() {
    var furnace = $('#lstFur').val();
    if (furnace === "") {
        alert("Please select a furnace");
        return;
    }

    var rows = document.querySelectorAll("#exception_cast tbody tr"); 
    var dataList = [];

    for (var i = 0; i < rows.length; i++) {
        var r = rows[i];

        var id = r.querySelector(".idno").value;
        var date = r.querySelector(".ExceptionDate").value;

        // ❌ Skip rows where ID or Date is empty/null
        if (id === "" || date === "") {
            continue; // skip this row
        }

        // Only push rows with valid ID and Date
        dataList[dataList.length] = {
            FURNACE: furnace,
            ID_NO: id,
            TAPHOLE_NO: r.querySelector(".TapholeNo").value,
            EXCEPTION_DATE: date,
            HH24: r.querySelector(".hh").value,
            MM: r.querySelector(".mm").value,
            TAPHOLE_LENGTH: r.querySelector(".TapholeLength").value,
            CLAY_PAUSED: r.querySelector(".ClayPaused").value,
            TYPE: r.querySelector(".Type").value
        };
    }

    if (dataList.length === 0) {
        alert("No rows with ID and Date to save");
        return;
    }

    $.ajax({
        url: "/CastHouse/Save_Exception_Cast",
        type: "POST",
        data: JSON.stringify(dataList),
        contentType: "application/json",
        success: function (res) {
            alert(res);
        },
        error: function () {
            alert("Error while saving");
        }
    });
}
</script>
