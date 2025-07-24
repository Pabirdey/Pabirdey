<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Dropdown Trigger Modal</title>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body class="p-4">

  <!-- Dropdown -->
  <label for="selectOption" class="form-label">Select Option</label>
  <select id="selectOption" class="form-select" aria-label="Select example">
    <option value="">-- Select an option --</option>
    <option value="1">Option 1</option>
    <option value="2">Option 2</option>
  </select>

  <!-- Modal -->
  <div class="modal fade" id="infoModal" tabindex="-1" aria-labelledby="infoModalLabel" aria-hidden="true">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="infoModalLabel">Option Selected</h5>
          <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
        </div>
        <div class="modal-body" id="modalBody">
          You selected something!
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
        </div>
      </div>
    </div>
  </div>

  <!-- Bootstrap JS (with Popper) -->
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>

  <!-- JavaScript to trigger modal -->
  <script>
    document.getElementById('selectOption').addEventListener('change', function () {
      const selectedValue = this.value;
      if (selectedValue) {
        document.getElementById('modalBody').textContent = 'You selected: Option ' + selectedValue;

        // Show modal
        const modal = new bootstrap.Modal(document.getElementById('infoModal'));
        modal.show();
      }
    });
  </script>
</body>
</html>