$.post('/Coke Plant/Get_Fugitive_Violin_Chart', {
    pTimestamp: yourDateValue,
    pOvenNo: yourOvenValue,
    pBatteryNo: yourBatteryValue
})
.done(function(data) {
    // render chart
})
.fail(function(xhr) {
    console.error("Server Error: ", xhr.responseText);
});