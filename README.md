<div class="modal fade" id="messageModal" tabindex="-1" aria-labelledby="messageModalLabel" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="messageModalLabel">Message</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body" id="modalMessageText">
        <!-- Message goes here -->
      </div>
    </div>
  </div>
</div>

@if (!string.IsNullOrEmpty(ViewBag.Message))
{
    <script type="text/javascript">
        document.addEventListener("DOMContentLoaded", function () {
            document.getElementById("modalMessageText").innerText = '@ViewBag.Message';
            var myModal = new bootstrap.Modal(document.getElementById('messageModal'));
            myModal.show();
        });
    </script>
}
