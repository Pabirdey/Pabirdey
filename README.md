let currentIndex = null;

        function toggleList(i) {
            const list = document.getElementById("list_" + i);
            if (list) {
                list.classList.toggle("show");
            }
        }

        function selectItem(el, i) {
            const value = el.innerText;
            const input = document.getElementById("clayInput_" + i);
            const list = document.getElementById("list_" + i);

            if (input) {
                input.value = value;
            }

            if (list) {
                list.classList.remove("show");
            }

            // Handle "OTHERS" option
            if (value === "OTHERS") {
                debugger;
                currentIndex = i;
                const modalElement = document.getElementById("clayModal");
                if (modalElement) {
                    // Clear modal input if it exists
                    const modalInput = modalElement.querySelector('input[type="text"]');
                    if (modalInput) {
                        modalInput.value = "";
                    }
                    const modal = new bootstrap.Modal(modalElement);
                    modal.show();
                }
            }
        }
         <div class="modal fade" id="clayModal" tabindex="-1">
        <div class="modal-dialog modal-md modal-dialog-centered">
            <div class="modal-content">
                <div class="modal-header bg-primary text-white">
                    <h5 class="modal-title w-100 text-center">MG CLAY DETAILS</h5>
                    <button type="button" class="btn-close btn-close-white" data-bs-dismiss="modal"></button>
                </div>
                <div class="modal-body">
                    <div class="mb-3">
                        <label>Clay 1</label>
                        <select class="form-select">
                            <option>Clay A</option>
                            <option>Clay B</option>
                        </select>
                    </div>
                    <div class="mb-3">
                        <label>Clay 2</label>
                        <select class="form-select">
                            <option>Clay A</option>
                            <option>Clay B</option>
                        </select>
                    </div>
                    <div class="mb-3">
                        <label>Clay 3</label>
                        <select class="form-select">
                            <option>Clay A</option>
                            <option>Clay B</option>
                        </select>
                    </div>
                </div>
                <div class="modal-footer justify-content-center">
                    <button class="btn btn-success" data-bs-dismiss="modal">Save</button>
                    <button class="btn btn-danger" data-bs-dismiss="modal">Exit</button>
                </div>
            </div>
        </div>
    </div>
