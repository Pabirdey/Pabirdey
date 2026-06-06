$.ajax({
    url: '@Url.Action("GetGranShotDetails","HML")',
    type: 'GET',
    data: {
        txtdt: $("#TXTDT").val(),
        txtshift: $("#TXTSHIFT").val(),
        txtfur: $("#TXTFUR").val()
    },
    success: function (result) {
        BindTable(result);
    }
});
