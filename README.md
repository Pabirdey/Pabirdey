function CheckDateTime() {

    $("#tblBody tr").each(function () {

        var castStart = $(this).find(".castStart").val();
        var castEnd = $(this).find(".castEnd").val();
        var ladleStart = $(this).find(".ladleStart").val();
        var ladleEnd = $(this).find(".ladleEnd").val();

        var castStartDT = castStart ? GetDateTime(castStart) : null;
        var castEndDT = castEnd ? GetDateTime(castEnd) : null;
        var ladleStartDT = ladleStart ? GetDateTime(ladleStart) : null;
        var ladleEndDT = ladleEnd ? GetDateTime(ladleEnd) : null;

        console.log(castStartDT);
        console.log(castEndDT);
        console.log(ladleStartDT);
        console.log(ladleEndDT);

    });
}
<tr>
    <td><input type="time" class="castStart"></td>
    <td><input type="time" class="castEnd"></td>
    <td><input type="time" class="ladleStart"></td>
    <td><input type="time" class="ladleEnd"></td>
</tr>
$("#btnSave").click(function () {

    var data = [];

    $("#tblBody tr").each(function () {

        var row = {

            CAST_NO: $(this).find(".castNo").val(),

            CAST_START_DT: GetDateTime(
                $(this).find(".castStart").val()
            ),

            CAST_END_DT: GetDateTime(
                $(this).find(".castEnd").val()
            ),

            LADLE_START_DT: GetDateTime(
                $(this).find(".ladleStart").val()
            ),

            LADLE_END_DT: GetDateTime(
                $(this).find(".ladleEnd").val()
            )
        };

        data.push(row);
    });

    $.ajax({
        url: '/Granshot/SaveData',
        type: 'POST',
        contentType: 'application/json',
        data: JSON.stringify(data),
        success: function () {
            alert("Saved Successfully");
        }
    });

});
var rows = [];

$("#tblBody tr").each(function () {

    rows.push({
        CAST_NO: $(this).find(".castNo").val(),
        CAST_START_DT: castStartDateTime,
        CAST_END_DT: castEndDateTime,
        LADLE_START_DT: ladleStartDateTime,
        LADLE_END_DT: ladleEndDateTime,
        ARRIVED_FROM: $(this).find(".arrivedFrom").val(),
        GROSS: $(this).find(".gross").val(),
        TARE: $(this).find(".tare").val(),
        NET: $(this).find(".net").val()
    });
});

$.ajax({
    url: '/Granshot/SaveData',
    type: 'POST',
    contentType: 'application/json',
    data: JSON.stringify(rows)
});
