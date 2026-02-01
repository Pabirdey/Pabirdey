  <script>
        function SaveExceptionCast() {
            debugger;
            var furnace =$('#lstFur').val();
        var rows = document.querySelectorAll("#exception_cast tbody tr"); 
        var dataList = [];
    for (var i = 0; i < rows.length; i++) {
    var r = rows[i];
        dataList.push({
        FURNACE: furnace,
        ID_NO: r.querySelector(".idno").value,
        TAPHOLE_NO: r.querySelector(".TapholeNo").value,
        EXCEPTION_DATE: r.querySelector(".ExceptionDate").value,
        HH24: r.querySelector(".hh").value,
        MM: r.querySelector(".mm").value,
        TAPHOLE_LENGTH: r.querySelector(".TapholeLength").value,
        CLAY_PAUSED: r.querySelector(".Clay").value,
        TYPE: r.querySelector(".Type").value
        });
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
