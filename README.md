function Display_Mudgun_Details(lsSelectedFDate, IsSelectedFur) {
    $.ajax({
        url: '@Url.Action("Get_Display_Mudgun_Details", "CastHouse")',
        type: 'GET',
        data: { Fdate: lsSelectedFDate, Fur: IsSelectedFur },
        success: function (result_Mudgun_Details) {

            var parsedData = JSON.parse(result_Mudgun_Details);
            var tableBody = "";

            for (var i = 0; i < parsedData.length; i++) {

                tableBody += "<tr>";

                tableBody += `<td><input name="CAST_NO" class='form-control form-control-lg' 
                        value='${parsedData[i].CAST_NO}' readonly/></td>`;

                tableBody += `<td><input name="CLOSURE_MODE" class='form-control form-control-lg' 
                        value='${parsedData[i].CLOSURE_MODE}'/></td>`;

                tableBody += `<td><input name="CLAY_QUANTITY" class='form-control form-control-lg' 
                        value='${parsedData[i].CLAY_QUANTITY}'/></td>`;

                tableBody += `<td>
                    <select name="MG_CLAY_USED" 
                        class='form-select form-select-lg clayDropdown'>
                        <option value=""></option>
                        ${[
                            'ACE','BRL','LRH','UBQ','SARVESH','CALDYRS','HARIMA(S)','HARIMA(D)',
                            'CORUS','TRB','VISUVIUS','HARIMA-TWH4','HARIMA-CPH4',
                            'HARIMA(D)-TWH5','HARIMA(D)-TWH5K','HARIMA(D)-TWH-5T',
                            'HARIMA RWH-3','HARIMA RWH-4','HARIMA(S)-RW5F',
                            'HARIMA(S)-RG15K','OTHERS'
                        ]
                        .map(option => `<option 
                            value="${option}" 
                            ${parsedData[i].MG_CLAY_USED === option ? 'selected' : ''}>
                            ${option}
                        </option>`)
                        .join("")}
                    </select>
                </td>`;

                tableBody += "</tr>";
            }

            $("#Mudgun_Details tbody").html(tableBody);
        }
    });
}

<div class="modal fade" id="clayModal" tabindex="-1">
  <div class="modal-dialog">
    <div class="modal-content">

      <div class="modal-header bg-primary text-white">
        <h5 class="modal-title">Enter Other Clay Name</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
      </div>

      <div class="modal-body">
        <input type="text" id="txtOtherClay" class="form-control" placeholder="Enter Clay Name">
      </div>

      <div class="modal-footer">
        <button class="btn btn-success" id="btnSaveClay">Save</button>
      </div>

    </div>
  </div>
</div>


var currentClayDropdown = null;

$(document).on("change", ".clayDropdown", function () {

    if ($(this).val() === "OTHERS") {
        currentClayDropdown = $(this);
        $("#txtOtherClay").val("");
        $("#clayModal").modal("show");
    }
});

// Save Button Click
$("#btnSaveClay").click(function () {

    var val = $("#txtOtherClay").val().trim();

    if (val === "") {
        alert("Please enter clay name");
        return;
    }

    // Add as new option and select it
    currentClayDropdown.append(`<option value="${val}" selected>${val}</option>`);
    currentClayDropdown.val(val);

    $("#clayModal").modal("hide");
});