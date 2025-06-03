<form class="container mt-4">
    <h3 class="text-success mb-4">Raw Material Quantity</h3>
    <div class="row g-3 align-items-center">

        <div class="col-md-2 d-flex align-items-center">
            <label for="pileNo" class="me-2">Pile No:</label>
            <input type="text" class="form-control" id="pileNo" placeholder="Pile No">
        </div>

        <div class="col-md-2 d-flex align-items-center">
            <label for="source" class="me-2">Source:</label>
            <input type="text" class="form-control" id="source" placeholder="Source">
        </div>

        <div class="col-md-2 d-flex align-items-center">
            <label for="shift" class="me-2">Shift:</label>
            <input type="text" class="form-control" id="shift" placeholder="Shift">
        </div>

        <div class="col-md-2 d-flex align-items-center">
            <label for="startDate" class="me-2">Start:</label>
            <input type="text" class="form-control" id="startDate" placeholder="Start Date">
        </div>

        <!-- Vertical stack for End Date and Cons ST Date -->
        <div class="col-md-2">
            <div class="d-flex align-items-center mb-2">
                <label for="endDate" class="me-2">End:</label>
                <input type="text" class="form-control" id="endDate" placeholder="End Date">
            </div>
            <div class="d-flex align-items-center">
                <label for="consStDate" class="me-2">Cons.:</label>
                <input type="text" class="form-control" id="consStDate" placeholder="Cons. ST. Date">
            </div>
        </div>

    </div>
</form>
