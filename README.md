<div class="Main">
        <div class="container">
            <h2 class="text-center page-title mb-4">Raw Material Consumption</h2>
            <div class="row">
                <div class="col-md-3">
                    <label for="tbFDatePick" class="LabelControl" style="font-family:Allan,cursive;font-size:18px;">Date:&nbsp;</label>
                    <a id="tbFDatePick" class="btn btn-primary">
                        <label id="currDate-value" style="font-size:12px;color:white"></label>
                    </a>
                    <input type="text" id="hiddenDate" style="position:absolute; opacity:0; height:0; width:0;" />
                    &nbsp;&nbsp;&nbsp;&nbsp;
                    <span>
                        <label style="font-family:Allan,cursive;font-size:18px;">Furnace</label>
                        <select id="ddlFurnace">
                            <option value="C">C</option>
                            <option value="E">E</option>
                            <option value="F">F</option>
                        </select>
                    </span>
                </div>
            </div>
            <!-- FLEX TABLE SECTION -->
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
                    <tbody></tbody>
                </table>
                <!-- TYPES TABLE -->
                <table id="types" class="table table-bordered">
                    <thead>
                        <tr>
                            <th>Types</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td>
                                <select id="ddlCoal" class="form-select">
                                    <option value=""></option>
                                    <option value="IPC">IPC</option>
                                    <option value="RPC">RPC</option>
                                    <option value="Curragh(N)+Aunthra">Curragh(N)+Aunthra</option>
                                    <option value="West Bokaro">West Bokaro</option>
                                    <option value="Jellinbah">Jellinbah</option>
                                    <option value="Foxleigh">Foxleigh</option>
                                </select>
                            </td>
                        </tr>
                        <tr>
                            <td>
                                <select id="ddlIO" class="form-select">
                                    <option value=""></option>
                                    <option value="BF Sized Banspani">BF Sized Banspani</option>
                                    <option value="BF Sized Joda">BF Sized Joda</option>
                                    <option value="BF Sized Khondbond">BF Sized Khondbond</option>
                                    <option value="BF Sized Noamundi">BF Sized Noamundi</option>
                                    <option value="LD Sized Noamundi">LD Sized Noamundi</option>
                                </select>
                            </td>
                        </tr>
                        <tr>
                            <td>
                                <select id="ddlPyro" class="form-select">
                                    <option value=""></option>
                                    <option value="Sukinda">Sukinda</option>
                                    <option value="Local">Local</option>
                                </select>
                            </td>
                        </tr>
                        <tr>
                            <td>
                                <select id="ddlLimestone" class="form-select">
                                    <option value=""></option>
                                    <option value="Gotan">Gotan</option>
                                    <option value="SP Grade">SP Grade</option>
                                </select>
                            </td>
                        </tr>
                        <tr>
                            <td>
                                <label style="font-family:Courier New, Courier, monospace;font-weight:bold;font-size:15px;"><strong>Theoretical Production</strong></label><br />
                                <input type="text" />
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>
      <style>
           .datepicker-days thead th {
            color: #000 !important;
            background-color: #f8f9fa !important;
            font-weight: bold;
        }

          
            .datepicker-days thead th.prev,
            .datepicker-days thead th.next {
                color: #000 !important;
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

        .page-title {
            font-weight: 700;
            color: #2c3e50;
        }


        /* ===== FLEXBOX FOR TABLES ===== */

        .Consumption {
            margin-left:5px;
            display: flex;
            gap: 5px;
            align-items: flex-start;
            flex-wrap: wrap;
            margin-top: 20px;
        }

        #materialTable {
            flex: 2;
            min-width: 40px;
            background: white;
        }

        #types {
            flex: 1;
            min-width: 100px;
            background: white;
        }

        #materialTable th {
            background: #000;
            color: white;
            text-align: center;
            font-family: Courier New;
            font-size: 16px;
        }

        #materialTable td {
            border: 1px solid #000;
            font-family: Courier New, monospace;
            font-weight: bold;
            font-size: 15px;
        }

        #types th {
            background: #000;
            color: white;
            text-align: center;
        }

        .medium-textbox {
            width: 100px;
            text-align: right;
            font-weight: bold;
        }

        .btn-custom {
            padding: 10px 40px;
            font-size: 15px;
            border-radius: 8px;
        }
    </style>
