<script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>

<script>
function Display_Mudgun_Details(date, furnace) {

    $.ajax({
        url: '@Url.Action("Get_Display_Mudgun_Details","CastHouse")',
        type: 'GET',
        data: { Fdate: date, Fur: furnace },
        success: function (data) {

            let html = "";

            for (let i = 0; i < data.length; i++) {

                html += `<tr>
                    <td>${data[i].CAST_NO}</td>

                    <td>
                        <select class="form-select form-select-sm">
                            <option value=""></option>
                            <option value="MUDGUN" ${data[i].CLOSURE_MODE=="MUDGUN"?"selected":""}>MUDGUN</option>
                            <option value="NULL" ${data[i].CLOSURE_MODE=="NULL"?"selected":""}>NULL</option>
                        </select>
                    </td>

                    <td>
                        <input class="form-control form-control-sm" value="${data[i].CLAY_QUANTITY}">
                    </td>

                    <td>
                        <div class="mgClayWrapper">
                            <input class="form-control form-control-sm mgClayInput"
                                   value="${data[i].MG_CLAY}">
                            <button class="btn btn-sm btn-secondary"
                                    onclick="showDropdown(this)">▼</button>

                            <div class="mgClayList">
                                <div onclick="selectClay(this)">ACE</div>
                                <div onclick="selectClay(this)">BRL</div>
                                <div onclick="selectClay(this)">LRH</div>
                                <div onclick="selectClay(this)">UBQ</div>
                                <div onclick="selectClay(this, true)">OTHERS</div>
                            </div>
                        </div>
                    </td>

                    <td>${data[i].LOT_NO}</td>
                    <td>${data[i].NO_OF_BAGS}</td>
                </tr>`;
            }

            $("#Mudgun_Details tbody").html(html);
        }
    });
}

// dropdown show
function showDropdown(btn) {
    $(".mgClayList").hide();
    $(btn).next(".mgClayList").show();

    $(document).one("click", function () {
        $(".mgClayList").hide();
    });

    event.stopPropagation();
}

// select item
function selectClay(el, isOther) {
    let input = $(el).closest(".mgClayWrapper").find(".mgClayInput");

    if (isOther) {
        $("#txtOtherMGClay").val(input.val());
        $("#hdnRowIndex").val(input.closest("tr").index());

        new bootstrap.Modal("#mgClayOtherModal").show();
    } else {
        input.val($(el).text());
    }

    $(".mgClayList").hide();
}

// modal save
function saveOtherMGClay() {
    let rowIndex = $("#hdnRowIndex").val();
    let val = $("#txtOtherMGClay").val();

    $("#Mudgun_Details tbody tr").eq(rowIndex)
        .find(".mgClayInput").val(val);

    bootstrap.Modal.getInstance(
        document.getElementById("mgClayOtherModal")
    ).hide();
}
</script>
