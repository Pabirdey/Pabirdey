<div class="modal fade" id="othersModal" tabindex="-1">
  <div class="modal-dialog">
    <div class="modal-content">

      <div class="modal-header">
        <h5 class="modal-title">Enter Other Clay Name</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
      </div>

      <div class="modal-body">
        <input type="text" id="otherClayName" class="form-control" placeholder="Enter Clay Name">
      </div>

      <div class="modal-footer">
        <button type="button" id="saveOtherClay" class="btn btn-primary">Save</button>
      </div>

    </div>
  </div>
</div>

var currentClayDropdown = null;

// Detect OTHERS click
$(document).on("change", "select[name='MG_CLAY_USED']", function () {

    if ($(this).val() === "OTHERS") {

        currentClayDropdown = this;

        var modal = new bootstrap.Modal(document.getElementById("othersModal"));
        modal.show();
    }
});

// Save custom clay
$("#saveOtherClay").click(function () {

    let value = $("#otherClayName").val().trim();

    if (value !== "" && currentClayDropdown) {

        $(currentClayDropdown).append(
            `<option selected>${value}</option>`
        );
    }

    bootstrap.Modal.getInstance(document.getElementById("othersModal")).hide();

    $("#otherClayName").val("");
});

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

                tableBody += `<td>
                    <input name="CAST_NO" class='form-control form-control-lg' 
                           value='${parsedData[i].CAST_NO}' readonly/>
                </td>`;

                tableBody += `<td>
                    <input name="CLAY_QUANTITY" class='form-control form-control-lg' 
                           value='${parsedData[i].CLAY_QUANTITY}'/>
                </td>`;

                tableBody += `<td>
                    <select name="MG_CLAY_USED" class='form-select form-select-lg'>
                        <option ${!parsedData[i].MG_CLAY_USED ? "selected" : ""} value=""></option>

                        ${[
                            'ACE','BRL','LRH','UBQ','SARVESH','CALDYRS','HARIMA(S)','HARIMA(D)',
                            'CORUS','TRB','VISUVIUS','HARIMA-TWH4','HARIMA-CPH4',
                            'HARIMA(D)-TWH5','HARIMA(D)-TWH5K','HARIMA(D)-TWH-5T',
                            'HARIMA RWH-3','HARIMA RWH-4','HARIMA(S)-RW5F',
                            'HARIMA(S)-RG15K','OTHERS'
                        ]
                        .map(option => 
                            `<option ${parsedData[i].MG_CLAY_USED === option ? "selected" : ""}>
                                ${option}
                             </option>`
                        ).join("")}

                    </select>
                </td>`;

                tableBody += "</tr>";
            }

            $("#Mudgun_Details tbody").html(tableBody);
        }
    });
}