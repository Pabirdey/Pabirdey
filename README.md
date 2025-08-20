<div class="row material-row mb-2">
    <div class="col-md-2 d-flex align-items-center">
        <label for="NoaFines" class="me-2 mb-0">Noa Fines</label>
        <input class="form-control form-control-sm" type="text" 
               value="@Model.NoaFines" name="NoaFines" id="NoaFines" 
               onblur="IOFinesSum()" autocomplete="off">
    </div>

    <div class="col-md-2 d-flex align-items-center">
        <label for="JodaFines" class="me-2 mb-0">Joda Fines</label>
        <input class="form-control form-control-sm" type="text" 
               value="@Model.JodaFines" name="JodaFines" id="JodaFines" 
               onblur="IOFinesSum()" autocomplete="off">
    </div>

    <div class="col-md-2 d-flex align-items-center">
        <label for="KBFines" class="me-2 mb-0">KB Fines</label>
        <input class="form-control form-control-sm" type="text" 
               value="@Model.KBFines" name="KBFines" id="KBFines" 
               onblur="IOFinesSum()" autocomplete="off">
    </div>

    <div class="col-md-2 d-flex align-items-center">
        <label for="YardFines" class="me-2 mb-0">Yard Fines</label>
        <input class="form-control form-control-sm" type="text" 
               value="@Model.YardFines" name="YardFines" id="YardFines" 
               onblur="IOFinesSum()" autocomplete="off">
    </div>

    <div class="col-md-2 d-flex align-items-center">
        <label for="BHJ" class="me-2 mb-0">BHJ</label>
        <input class="form-control form-control-sm" type="text" 
               value="@Model.BHJ" name="BHJ" id="BHJ" 
               onblur="IOFinesSum()" autocomplete="off">
    </div>

    <div class="col-md-2 d-flex align-items-center">
        <label for="Namisa" class="me-2 mb-0">Namisa</label>
        <input class="form-control form-control-sm" type="text" 
               value="@Model.Namisa" name="Namisa" id="Namisa" 
               onblur="IMPOreFinesSum()" autocomplete="off">
    </div>
</div>