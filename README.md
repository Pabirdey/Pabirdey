<div id="loader">Saving... Please Wait ⏳</div>

<div class="Main">
    <div class="container">
        <h2 class="text-center page-title mb-4">Raw Material Consumption</h2>

        <div class="row">
            <div class="col-md-3">
                <fieldset>
                    <legend>Date Selection</legend>
                    <a id="date-daily" class="btn btn-primary">
                        <span id="currDate-value"></span>
                    </a>
                </fieldset>
            </div>

            <div class="col-md-3">
                <fieldset>
                    <legend>Furnace Selection</legend>
                    <select class="form-select" id="ddlFurnace">
                        <option value="C">C</option>
                        <option value="E">E</option>
                        <option value="F">F</option>
                    </select>
                </fieldset>
            </div>
        </div>

        <div class="Consumption">

            <!-- MATERIAL TABLE -->
            <div id="materialTableContainer">
                <table id="materialTable" class="table table-bordered">
                    <thead>
                        <tr>
                            <th>Material</th>
                            <th>Value (Tons)</th>
                            <th>Value (Kgs)</th>
                        </tr>
                    </thead>
                    <tbody></tbody>
                </table>
            </div>

            <!-- TYPES -->
            <table id="types" class="table table-bordered">
                <thead>
                    <tr>
                        <th>Types</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td><select class="form-select"><option>IPC</option><option>RPC</option></select></td>
                    </tr>
                    <tr>
                        <td><select class="form-select"><option>BF Sized Joda</option></select></td>
                    </tr>
                    <tr>
                        <td><select class="form-select"><option>Sukinda</option></select></td>
                    </tr>
                    <tr>
                        <td><select class="form-select"><option>Gotan</option></select></td>
                    </tr>
                </tbody>
            </table>
        </div>

        <div class="text-center mt-4">
            <button class="btn btn-primary btn-custom" onclick="SaveBFRawMaterialCons()">Save</button>
        </div>
    </div>
</div>
