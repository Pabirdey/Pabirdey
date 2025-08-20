<div class="row g-2 mb-3"> <!-- g-2 gives gutter spacing between columns -->
    <div class="col-md-2">
        <label for="NoaFines" class="form-label">Noa Fines</label>
        <input type="text" class="form-control" id="NoaFines" name="NoaFines" value="@Model.NoaFines" onblur="IOFinesSum()" autocomplete="off">
    </div>
    <div class="col-md-2">
        <label for="JodaFines" class="form-label">Joda Fines</label>
        <input type="text" class="form-control" id="JodaFines" name="JodaFines" value="@Model.JodaFines" onblur="IOFinesSum()" autocomplete="off">
    </div>
    <div class="col-md-2">
        <label for="KBFines" class="form-label">KB Fines</label>
        <input type="text" class="form-control" id="KBFines" name="KBFines" value="@Model.KBFines" onblur="IOFinesSum()" autocomplete="off">
    </div>
    <div class="col-md-2">
        <label for="YardFines" class="form-label">Yard Fines</label>
        <input type="text" class="form-control" id="YardFines" name="YardFines" value="@Model.YardFines" onblur="IOFinesSum()" autocomplete="off">
    </div>
    <div class="col-md-2">
        <label for="BHJ" class="form-label">BHJ</label>
        <input type="text" class="form-control" id="BHJ" name="BHJ" value="@Model.BHJ" onblur="IOFinesSum()" autocomplete="off">
    </div>
    <div class="col-md-2">
        <label for="Namisa" class="form-label">Namisa</label>
        <input type="text" class="form-control" id="Namisa" name="Namisa" value="@Model.Namisa" onblur="IMPOreFinesSum()" autocomplete="off">
    </div>
</div>