  function setDeclaredDate(dateInput) {
            debugger;
    if ($(dateInput).val() !== "") return;

    let declaredDate = $('#lsSelectedFDate').text().trim();
    if (declaredDate != "") {
        $(dateInput).val(declaredDate);
    }
}
