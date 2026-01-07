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