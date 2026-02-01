<script>
function SaveExceptionCast() {
    var furnace = $('#lstFur').val();

    var rows = document.querySelectorAll("#exception_cast tbody tr"); 
    var dataList = [];

    for (var i = 0; i < rows.length; i++) {
        var r = rows[i];

        // Grab values safely, even if empty
        var id = r.querySelector(".idno") ? r.querySelector(".idno").value : null;
        var tapholeNo = r.querySelector(".TapholeNo") ? r.querySelector(".TapholeNo").value : null;
        var date = r.querySelector(".ExceptionDate") ? r.querySelector(".ExceptionDate").value : null;
        var hh = r.querySelector(".hh") ? r.querySelector(".hh").value : null;
        var mm = r.querySelector(".mm") ? r.querySelector(".mm").value : null;
        var tapLen = r.querySelector(".TapholeLength") ? r.querySelector(".TapholeLength").value : null;
        var clay = r.querySelector(".ClayPaused") ? r.querySelector(".ClayPaused").value : null;
        var type = r.querySelector(".Type") ? r.querySelector(".Type").value : null;

        dataList[dataList.length] = {
            FURNACE: furnace || null,
            ID_NO: id,
            TAPHOLE_NO: tapholeNo,
            EXCEPTION_DATE: date,
            HH24: hh,
            MM: mm,
            TAPHOLE_LENGTH: tapLen,
            CLAY_PAUSED: clay,
            TYPE: type
        };
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
