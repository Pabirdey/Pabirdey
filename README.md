tableBody += `<td>
  <div class="input-group">
    <input name="LOT_NO" class='form-control form-control-lg' value='${parsedData[i].LOT_NO}'/>
    <button type="button" class="btn btn-outline-primary openLotModal" data-index="${i}" data-bs-toggle="modal" data-bs-target="#lotModal">
      <i class="fa fa-search"></i>
    </button>
  </div>
</td>`;

<!-- LOT Modal -->
<div class="modal fade" id="lotModal" tabindex="-1" aria-labelledby="lotModalLabel" aria-hidden="true">
  <div class="modal-dialog modal-dialog-centered">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="lotModalLabel">Select LOT NO</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
        <!-- You can add a list of LOTs or a search box here -->
        <input type="text" class="form-control mb-2" placeholder="Search LOT...">
        <ul class="list-group">
          <li class="list-group-item lot-item">LOT1234</li>
          <li class="list-group-item lot-item">LOT5678</li>
          <li class="list-group-item lot-item">LOT9012</li>
        </ul>
      </div>
    </div>
  </div>
</div>

$(document).ready(function () {
    let selectedRowIndex = null;

    // Open modal and store index of clicked row
    $(document).on('click', '.openLotModal', function () {
        selectedRowIndex = $(this).data('index');
    });

    // On click of lot item in modal
    $(document).on('click', '.lot-item', function () {
        const selectedLot = $(this).text();
        const row = $("#Mudgun_Details tbody tr").eq(selectedRowIndex);
        row.find('input[name="LOT_NO"]').val(selectedLot);
        $('#lotModal').modal('hide'); // Close modal
    });
});
