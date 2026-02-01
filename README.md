<tr>
    <td><input class="idno"></td>
    <td><input class="taphole"></td>
    <td><input type="date" class="castdate"></td>
    <td><input class="hh"></td>
    <td><input class="mm"></td>
    <td><input class="length"></td>
    <td>
        <select class="clay">
            <option value="Y">Yes</option>
            <option value="N">No</option>
        </select>
    </td>
    <td>
        <select class="type">
            <option value="NORMAL">NORMAL</option>
            <option value="EXCEPTION">EXCEPTION</option>
        </select>
    </td>
</tr>
<script>
function SaveExceptionCast() {

    var furnace = document.getElementById("ddlFurnace").value;
    if (furnace === "") {
        alert("Please select Furnace");
        return;
    }

    var rows = document.querySelectorAll("#exception_cast tbody tr");
    if (rows.length === 0) {
        alert("No data to save");
        return;
    }

    var dataList = [];

    for (var i = 0; i < rows.length; i++) {
        var r = rows[i];

        dataList.push({
            FURNACE: furnace,
            ID_NO: r.querySelector(".idno").value,
            TAPHOLE_NO: r.querySelector(".taphole").value,
            CAST_DATE: r.querySelector(".castdate").value,
            HH24: r.querySelector(".hh").value,
            MM: r.querySelector(".mm").value,
            TAPHOLE_LENGTH: r.querySelector(".length").value,
            CLAY_PAUSED: r.querySelector(".clay").value,
            TYPE: r.querySelector(".type").value
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
