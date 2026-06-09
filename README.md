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