$("#DISPLAY_ACT_G").val(
    Math.round(
        (item.ACTUAL || 0) +
        parseFloat($("#DisplayActual").val() || 0)
    )
);
