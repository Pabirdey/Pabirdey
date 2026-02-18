<style>
    .datepicker-days thead th {
        color: #000 !important;
        background-color: #f8f9fa !important;
        font-weight: bold;
    }

    .datepicker {
        z-index: 1055 !important;
    }

    body {
        background-color: #f4f6f9;
    }

    .Main {
        background-color: #ffffff;
        padding: 20px;
        border-radius: 10px;
    }

    .Main-Heading {
        font-family: Allan, cursive;
        font-weight: bold;
        font-size: 6vh;
        text-align: center;
        padding: 20px;
        color: rgb(57,57,57);
        margin: 20px 0;
    }

    .Consumption {
        display: flex;
        gap: 10px;
        align-items: flex-start;
        flex-wrap: wrap;
        margin-top: 20px;
    }

    #materialTable {
        flex: 0 0 550px;
        max-width: 550px;
        background: white;
        font-family: Courier New;
    }

    #types {
        flex: 0 0 310px;
        max-width: 310px;
        background: white;
        border: 1px solid;
    }

    #materialTable th {
        background: #8d15aa;
        color: white;
        text-align: center;
    }

    #materialTable td {
        border: 1px solid #000;
        font-weight: bold;
    }

    #types th {
        background: #8d15aa;
        color: white;
        text-align: center;
    }

    #types .btn {
        min-width: 90px;
        font-weight: bold;
        font-family: Courier New;
    }

    .medium-textbox {
        width: 100px;
        text-align: right;
        font-weight: bold;
    }
</style>


<div class="Main">
    <div class="container">

        <h2 class="Main-Heading">Raw Material Consumption</h2>

        <!-- FLEX SECTION -->
        <div class="Consumption">

            <!-- MATERIAL TABLE -->
            <table id="materialTable" class="table table-bordered">
                <thead>
                    <tr>
                        <th>Material</th>
                        <th>Value (Tons)</th>
                        <th>Value (Kgs)</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>Coke</td>
                        <td><input type="text" class="medium-textbox" /></td>
                        <td><input type="text" class="medium-textbox" /></td>
                    </tr>
                </tbody>
            </table>


            <!-- TYPES TABLE -->
            <table id="types" class="table table-bordered">
                <thead>
                    <tr>
                        <th>Types</th>
                    </tr>
                </thead>
                <tbody>

                    <!-- Coal -->
                    <tr>
                        <td>
                            <div style="display:flex;align-items:center;gap:10px;">
                                <select id="ddlCoal" class="form-select">
                                    <option value=""></option>
                                    <option>IPC</option>
                                    <option>RPC</option>
                                    <option>Curragh(N)+Aunthra</option>
                                    <option>West Bokaro</option>
                                    <option>Jellinbah</option>
                                    <option>Foxleigh</option>
                                </select>
                                <span style="font-weight:bold;">(Coal)</span>
                            </div>
                        </td>
                    </tr>

                    <!-- I/O -->
                    <tr>
                        <td>
                            <div style="display:flex;align-items:center;gap:10px;">
                                <select id="ddlIO" class="form-select">
                                    <option value=""></option>
                                    <option>BF Sized Banspani</option>
                                    <option>BF Sized Joda</option>
                                    <option>BF Sized Khondbond</option>
                                    <option>BF Sized Noamundi</option>
                                    <option>LD Sized Noamundi</option>
                                </select>
                                <span style="font-weight:bold;">(I/O)</span>
                            </div>
                        </td>
                    </tr>

                    <!-- Pyrox -->
                    <tr>
                        <td>
                            <div style="display:flex;align-items:center;gap:10px;">
                                <select id="ddlPyro" class="form-select">
                                    <option value=""></option>
                                    <option>Sukinda</option>
                                    <option>Local</option>
                                </select>
                                <span style="font-weight:bold;">(Pyrox)</span>
                            </div>
                        </td>
                    </tr>

                    <!-- Limestone -->
                    <tr>
                        <td>
                            <div style="display:flex;align-items:center;gap:10px;">
                                <select id="ddlLimestone" class="form-select">
                                    <option value=""></option>
                                    <option>Gotan</option>
                                    <option>SP Grade</option>
                                </select>
                                <span style="font-weight:bold;">(L/S)</span>
                            </div>
                        </td>
                    </tr>

                    <!-- Theoretical Production -->
                    <tr>
                        <td>
                            <label style="font-weight:bold;font-size:16px;">
                                Theoretical Production
                            </label><br />
                            <input type="text" class="form-control" />
                        </td>
                    </tr>

                    <!-- BUTTONS ROW -->
                    <tr>
                        <td style="text-align:center;padding-top:15px;">
                            <div style="display:flex;justify-content:center;gap:10px;flex-wrap:wrap;">
                                <button class="btn btn-success"
                                        onclick="SaveBFRawMaterialCons()">
                                    Save
                                </button>

                                <button class="btn btn-warning"
                                        onclick="goToBinDetails()">
                                    Bin Details
                                </button>

                                <button class="btn btn-primary"
                                        onclick="goBack()">
                                    Back
                                </button>
                            </div>
                        </td>
                    </tr>

                </tbody>
            </table>

        </div>
    </div>
</div>


<script>
    function SaveBFRawMaterialCons() {
        alert("Data Saved Successfully!");
        // Yaha AJAX call laga sakte ho
    }

    function goToBinDetails() {
        // MVC Navigation example
        window.location.href = '/YourController/BinDetails';
    }

    function goBack() {
        window.history.back();
    }
</script>