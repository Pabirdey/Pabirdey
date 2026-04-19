<div class="container py-4">

    <!-- HEADER -->
    <div class="mb-4">
        <h4 class="fw-bold" style="font-family:Allan,cursive;">
            Production
        </h4>

        <div style="margin-top:5px;">
            <label style="font-family:Allan,cursive;font-size:18px;">
                Date:
            </label>

            <a id="tbFDatePick" class="btn btn-primary btn-sm">
                <label id="currDate-value" style="color:white"></label>
            </a>

            <input type="text" id="hiddenDate"
                   style="position:absolute; opacity:0; height:0; width:0;" />
        </div>
    </div>

    <!-- TABLES ROW -->
    <div class="row">

        <!-- LEFT TABLE -->
        <div class="col-md-7">
            <div class="table-responsive">
                <table class="table table-bordered text-center"
                       style="border:2px solid black;font-family:'Courier New';font-weight:bold;">
                    <!-- your same table -->
                </table>
            </div>
        </div>

        <!-- RIGHT TABLE -->
        <div class="col-md-5">
            <h5 class="fw-bold text-center mb-2"
                style="font-family:Allan,cursive;">
                Actual Breakup
            </h5>

            <div class="table-responsive">
                <table class="table table-bordered text-center"
                       style="border:2px solid black;font-family:'Courier New';font-weight:bold;">
                    <!-- your same table -->
                </table>
            </div>
        </div>

    </div>

    <!-- BUTTON -->
    <div class="text-center mt-3">
        <button type="button" onclick="saveAllData()" class="btn btn-success">
            Save
        </button>
    </div>

</div>
