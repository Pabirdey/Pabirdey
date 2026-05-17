 <td>
        <input type="text"
               class="form-control reported"
               id="REPORTED_E"
               value="@Model.ReportedE"
               data-original="@Model.ReportedE" />
    </td>
    $(document).on("blur", ".reported", function () {

    let row = $(this).closest("tr");

    let current = parseFloat($(this).val()) || 0;

    let old = parseFloat($(this).attr("data-old")) || 0;

    let diff = current - old;

    // update ToDate
    let td = row.find("td:eq(4) input");
    td.val((parseFloat(td.val()) || 0) + diff);

    // update Balance
    let bal = row.find("td:eq(5) input");
    bal.val((parseFloat(bal.val()) || 0) - diff);

    // update stored value
    $(this).attr("data-old", current);
});
