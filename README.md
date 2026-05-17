$("#DISPLAY_ACT_H").val(
    Math.round(
        (item.ACTUAL || 0) +
        parseFloat($("#DisplayActual").val() || 0) +
        parseFloat($("#DISPLAY_ACT_G").val() || 0)
    )
);
