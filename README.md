@{
    ViewBag.Title = "Cast House Details";
    Layout = null;
}
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Cast House Details</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap-datepicker@1.10.0/dist/css/bootstrap-datepicker.min.css" rel="stylesheet">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css" rel="stylesheet">
    <style>
        /* Force month/year heading visible */
        .datepicker-days thead th {
            color: #000 !important;
            background-color: #f8f9fa !important;
            font-weight: bold;
        }

            /* Prev / Next arrows */
            .datepicker-days thead th.prev,
            .datepicker-days thead th.next {
                color: #000 !important;
            }

        /* Fix Bootstrap 5 overlap */
        .datepicker {
            z-index: 1055 !important;
        }
        /* ===== Headings ===== */
        .Main-Heading {
            font-family: Allan, cursive;
            font-weight: bold;
            font-size: 6vh;
            text-align: center;
            padding: 20px;
            color: rgb(57,57,57);
            text-shadow: rgba(13, 0, 77, 0.08) 0px 2px 4px, rgba(13, 0, 77, 0.08) 0px 3px 6px, rgba(13, 0, 77, 0.08) 0px 8px 16px;
            border-radius: 10px;
            margin: 20px 0;
        }

        /* ===== Sections ===== */
        .form-section {
            background: #ffffff;
            padding: 20px;
            border-radius: 20px;
            box-shadow: 0 10px 20px rgba(0,0,0,0.1);
            margin-bottom: 25px;
            overflow: visible;
            border: 1px solid #ccc;
            font-family: Courier New, Courier, monospace;
        }

        .section-title,
        .section_Exception-title,
        .section-Drill-title {
            background: #EEB86D;
            color: black;
            padding: 5px 10px;
            font-weight: bold;
            border-radius: 10px;
            margin-bottom: 10px;
            font-family: Courier New, Courier, monospace;
        }

        .section-title {
            font-size: 18px;
        }

        .section_Exception-title {
            font-size: 15px;
            width: 15vh;
        }

        .section-Drill-title {
            font-size: 20px;
            border-radius: 4px;
        }

        /* ===== Forms ===== */
        .form-control-lg {
            font-size: 1.5rem;
            font-family: Courier New, Courier, monospace;
            color: black;
        }

        .form-group {
            border-radius: 25px;
            border: 4px solid #73AD21;
            padding: 10px;
            margin: 10px;
            width: 500px;
        }

        /* ===== Tables ===== */
        th {
            font-family: Courier New, Courier, monospace;
            font-size: 14px;
            font-weight: bold;
            border: 1px solid;
            color: white;
        }

        .table th,
        .table td {
            text-align: center;
            vertical-align: middle;
        }

        .scrollable-table {
            overflow-y: auto;
        }

        .table thead th {
            position: sticky;
            top: 0;
            z-index: 2;
            border: 1px solid;
        }

        /* ===== Column Widths ===== */
        .Long_Heading {
            min-width: 130px;
        }

        .Long_Heading_Medium {
            min-width: 100px;
        }

        .Heading_Tiny {
            width: 20px;
            white-space: nowrap;
        }

        .Heading_Small {
            width: 10px;
            white-space: nowrap;
        }

        /* ===== Inputs ===== */
        .table-input {
            font-size: 1rem;
            padding: 2px 4px;
            border: 2px solid;
        }

        .highlight {
            background-color: #ffe08a !important;
        }

        /* ===== Buttons ===== */
        .btnSaveCastHouse {
            background: linear-gradient(to bottom right, #EF4765, #FF9A5A);
            border: 0;
            border-radius: 10px;
            color: #FFFFFF;
            cursor: pointer;
            font-family: Courier New, Courier, monospace;
            font-size: 15px;
            font-weight: bold;
            line-height: 2.5;
            padding: 0 1rem;
            width: 12vh;
            margin-left: 30px;
            margin-top: 100px;
            transition: box-shadow .2s ease-in-out;
        }

            .btnSaveCastHouse:hover,
            .btnSaveCastHouse:focus {
                box-shadow: 0 0 .25rem rgba(0,0,0,.5), -.125rem -.125rem 1rem rgba(239,71,101,.5), .125rem .125rem 1rem rgba(255,154,90,.5);
            }

        .btnHMLogistics {
            margin: 10px;
            padding: 15px 30px;
            font-weight: bold;
            color: white;
            border-radius: 10px;
            border: 0;
            background-image: linear-gradient(45deg, #FF512F 0%, #F09819 51%, #FF512F 100%);
            background-size: 200% auto;
            cursor: pointer;
            transition: 0.5s;
            box-shadow: 0px 0px 14px -7px #f09819;
        }

            .btnHMLogistics:hover {
                background-position: right center;
            }

            .btnHMLogistics:active {
                transform: scale(0.95);
            }

        /* ===== SweetAlert ===== */
        .my-swal-popup {
            font-family: Arial, sans-serif;
        }

        .my-swal-title {
            font-family: Georgia, serif;
            font-size: 22px;
        }

        .my-swal-text {
            font-family: Verdana, sans-serif;
            font-size: 18px;
        }

        /* ===== Mudgun Clay Dropdown ===== */
        .mgClayWrapper {
            position: relative;
            display: flex;
            align-items: center;
        }

            .mgClayWrapper .mgClayInput {
                width: 100%;
            }

            .mgClayWrapper button {
                margin-left: 5px;
            }

        .mgClayList {
            display: none;
            position: absolute;
            background: white;
            border: 1px solid #ccc;
            z-index: 1000;
            top: 30px;
            left: 0;
            width: 200px;
            max-height: 200px;
            overflow-y: auto;
        }

            .mgClayList div {
                padding: 5px;
                cursor: pointer;
            }

                .mgClayList div:hover {
                    background: #eee;
                }

        /* ===== Misc ===== */
        #backgrcol_Tap_hole {
            font-weight: bold;
            padding: 8px;
        }

        fieldset {
            border: 2px solid #ccc !important;
            padding: 10px 12px 12px 12px;
        }

        legend {
            font-size: 24px;
            font-weight: 800;
            padding: 0 8px;
        }

        #Driling_Slag_Details tr.highlight td {
            background-color: yellow !important;
        }

        #TAP_Hot_Metal_Details tr.highlight td {
            background-color: yellow !important;
        }

        #Mudgun_Details tr.highlight td {
            background-color: yellow !important;
        }

        #Other_Details tr.highlight td {
            background-color: yellow !important;
        }
        /* ===== Tap Hole Freeze Column ===== */
        .freeze-col {
            position: sticky;
            left: 0;
            z-index: 3;
            background: #ffffff;
            border-right: 2px solid #666;
        }

        /* Header needs higher z-index */
        .table thead th.freeze-col {
            z-index: 5;
        }

        .modal-content {
            border-radius: 25px;
            border: none;
        }

        .modal-header {
            background: #0d6efd;
            color: #fff;
            border-radius: 25px 25px 0 0;
        }

        .title-box {
            background: #0d6efd;
            color: white;
            padding: 10px 25px;
            border-radius: 30px;
            text-align: center;
            font-size: 18px;
            font-weight: 600;
            margin-bottom: 20px;
        }

        .clay-box {
            background: #0d6efd;
            border-radius: 25px;
            padding: 20px;
            color: white;
        }

        .clay-label {
            font-weight: 600;
        }

        .clay-input {
            border-radius: 10px;
        }

        .btn-save {
            background: #198754;
            color: white;
            padding: 8px 30px;
            border-radius: 20px;
        }

        .btn-exit {
            background: #dc3545;
            color: white;
            padding: 8px 30px;
            border-radius: 20px;
        }
    </style>

</head>
<body>
    <div class="Main-Heading mt-3">Cast House Details</div>
    <div class="container-fluid mt-3">
        <div class="form-group">
            <label for="tbFDatePick" class="LabelControl" style="font-family:Allan,cursive;font-size:22px;">Date:&nbsp;</label>
            <a id="tbFDatePick" class="btn btn-primary">
                <i class="fa fa-calendar"></i>
                <label id="currDate-value" style="font-size:12px;color:white"></label>
            </a>
            <input type="text" id="hiddenDate" style="position:absolute; opacity:0; height:0; width:0;" />
            &nbsp;&nbsp;&nbsp;&nbsp;
            <span>
                <lable style="font-family:Allan,cursive;font-size:25px;">Furnace</lable>
                <select id="lstFur">
                    <option value="C">C</option>
                    <option value="D">D</option>
                    <option value="E">E</option>
                    <option value="F">F</option>
                    <option value="G">G</option>
                    <option value="H">H</option>
                    <option value="I">I</option>
                </select>
            </span>
        </div>
        <div class="mt-3">           
            <!--Other Details-->
            <div class="form-section">
                <div class="row g-0">
                    <div class="col-md-4">
                        <div class="section-title">Other Details</div>
                        <div class="table-responsive scrollable-table" style="max-height:245px;">
                            <table class="table table-bordered table-sm text-center align-middle" id="Other_Details">
                                <thead>
                                    <tr>
                                        <th clas="freeze-col" style="width:100px;min-width:100px;box-sizing:border-box;">Cast No</th>
                                        <th style="width:20px;min-width:20px;box-sizing:border-box;">Main Runner HM Amt</th>
                                        <th style="width:20px;min-width:20px;box-sizing:border-box;">Tilting Runner HM Amt</th>
                                        <th style="width:350px;min-width:350px;box-sizing:border-box;">Remarks</th>
                                    </tr>
                                </thead>
                                <tbody></tbody>
                            </table>
                        </div>
                    </div>
                    <div class="col-md-6">
                        <!-- Exception Cast Box -->
                        <fieldset class="border rounded p-3 shadow-sm mb-4">
                            <legend class="float-none w-auto px-2">
                                Exception Cast
                            </legend>
                            <div class="d-flex justify-content-between align-items-center mb-2">
                                <span></span>
                                <button type="button" class="btn btn-success btn-sm" onclick="saveExceptionCast()">
                                    <b>Save</b>
                                </button>
                            </div>
                            <div class="table-responsive scrollable-table" style="max-height:282px; overflow-y:auto;">
                                <table class="table table-bordered table-sm text-center align-middle" id="exception_cast">
                                    <thead class="table-secondary sticky-top">
                                        <tr>
                                            <th style="width:150px;">ID No</th>
                                            <th style="width:180px;">Date</th>
                                            <th style="width:90px;">HH24</th>
                                            <th style="width:90px;">MM</th>
                                            <th>Taphole Length</th>
                                            <th>Clay Paused</th>
                                            <th style="width:240px;">Type</th>
                                        </tr>
                                    </thead>
                                    <tbody>
                                        <!-- rows created by JS -->
                                    </tbody>
                                </table>
                            </div>
                        </fieldset>
                        <!-- Carbon Paste Inj Box -->
                        <fieldset class="border rounded p-3 shadow-sm">
                            <legend class="float-none w-auto px-2">
                                Carbon Paste Inj
                            </legend>
                            <div class="d-flex justify-content-between align-items-center mb-2">
                                <span></span>
                                <button type="button" class="btn btn-success btn-sm" onclick="saveCarbonPaste()">
                                    <b>Save</b>
                                </button>
                                <input type="hidden" id="saveUrl" value="@Url.Action("SaveCarbonPaste", "CastHouse")" />
                            </div>

                            <div class="table-responsive scrollable-table" style="max-height:255px;">
                                <table class="table table-bordered table-sm text-center align-middle"
                                       id="carbon_paste_inj">

                                    <thead>
                                        <tr>
                                            <th class="Heading_Small">Date Time</th>
                                            <th class="Heading_Small">Shift</th>
                                            <th class="Heading_Small">Below Tuyere</th>
                                            <th class="Heading_Small">No of Drum</th>
                                        </tr>
                                    </thead>

                                    <tbody></tbody>

                                </table>
                            </div>
                        </fieldset>
                    </div>
                    <div class="col-md-2">
                        <div>
                            <div>
                                <div class="mb-2">
                                    <button type="button" class="btnSaveCastHouse" onclick="SaveCastHouseData()">Save</button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <!-- Modal for Other MG Clay -->
    <div class="modal fade" id="mgClayOtherModal" tabindex="-1">
        <div class="modal-dialog modal-md modal-dialog-centered">
            <div class="modal-content">
                <!-- HEADER -->
                <div class="modal-header">
                    <h5 class="modal-title w-100 text-center">MG_CLAY</h5>
                    <button type="button" class="btn-close btn-close-white" data-bs-dismiss="modal"></button>
                </div>
                <!-- BODY -->
                <div class="modal-body">
                    <div class="title-box">Weightage of Clay</div>
                    <div class="clay-box">
                        <!-- Clay 1 (DROPDOWN) -->
                        <div class="row align-items-center mb-3">
                            <div class="col-2 clay-label">Clay1</div>
                            <div class="col-7">
                                <select class="form-select clay-input" id="MG_CLAY1">
                                    <option value="">-- Select Clay1 --</option>
                                    <option>ACE</option>
                                    <option>BRL</option>
                                    <option>LRH</option>
                                    <option>UBQ</option>
                                    <option>CALDYRS</option>
                                    <option>HARIMA(S)</option>
                                    <option>HARIMA(D)</option>
                                    <option>CORUS</option>
                                    <option>TRB</option>
                                    <option>VISUVIUS</option>
                                    <option>HARIMA-TWH4</option>
                                    <option>HARIMA-CPH4</option>
                                    <option>HARIMA(D)-TWH5</option>
                                    <option>HARIMA(D)-TWH5K</option>
                                    <option>HARIMA(D)TWH-5T</option>
                                    <option>HARIMA RWH-3</option>
                                    <option>HARIMA RWH-4</option>
                                    <option>HARIMA(S)RW5F</option>
                                    <option>HARIMA RWH-5</option>
                                    <option>HARIMA RWH-6</option>
                                    <option>HARIMA CB1</option>
                                    <option>RW5F</option>
                                    <option>RG15</option>
                                    <option>RG15K</option>
                                    <option>HARIMA(D)TWH-7</option>
                                    <option>HARIMA CB2</option>
                                    <option>TWH5(BELPAHAR)</option>
                                    <option>CB2(BELPAHAR)</option>
                                    <option>TWH 8(BELPAHAR)</option>
                                    <option>TWH 8 K 1(BELPAHAR)</option>
                                </select>
                            </div>
                            <div class="col-3">
                                <select class="form-select clay-input" id="P1">
                                    <option value="">%</option>
                                    <option>5</option>
                                    <option>10</option>
                                    <option>15</option>
                                    <option>20</option>
                                    <option>25</option>
                                    <option>30</option>
                                    <option>35</option>
                                    <option>40</option>
                                    <option>45</option>
                                    <option>50</option>
                                    <option>55</option>
                                    <option>60</option>
                                    <option>65</option>
                                    <option>70</option>
                                    <option>75</option>
                                    <option>80</option>
                                    <option>85</option>
                                    <option>90</option>
                                    <option>95</option>
                                    <option>100</option>
                                </select>
                            </div>
                        </div>
                        <!-- Clay 2 -->
                        <div class="row align-items-center mb-3">
                            <div class="col-2 clay-label">Clay2</div>
                            <div class="col-7">
                                <select class="form-select clay-input" id="MG_CLAY2">
                                    <option value="">-- Select Clay2 --</option>
                                    <option>ACE</option>
                                    <option>BRL</option>
                                    <option>LRH</option>
                                    <option>UBQ</option>
                                    <option>CALDYRS</option>
                                    <option>HARIMA(S)</option>
                                    <option>HARIMA(D)</option>
                                    <option>CORUS</option>
                                    <option>TRB</option>
                                    <option>VISUVIUS</option>
                                    <option>HARIMA-TWH4</option>
                                    <option>HARIMA-CPH4</option>
                                    <option>HARIMA(D)-TWH5</option>
                                    <option>HARIMA(D)-TWH5K</option>
                                    <option>HARIMA(D)TWH-5T</option>
                                    <option>HARIMA RWH-3</option>
                                    <option>HARIMA RWH-4</option>
                                    <option>HARIMA(S)RW5F</option>
                                    <option>HARIMA RWH-5</option>
                                    <option>HARIMA RWH-6</option>
                                    <option>HARIMA CB1</option>
                                    <option>RW5F</option>
                                    <option>RG15</option>
                                    <option>RG15K</option>
                                    <option>HARIMA(D)TWH-7</option>
                                    <option>HARIMA CB2</option>
                                    <option>TWH5(BELPAHAR)</option>
                                    <option>CB2(BELPAHAR)</option>
                                    <option>TWH 8(BELPAHAR)</option>
                                    <option>TWH 8 K 1(BELPAHAR)</option>
                                </select>
                            </div>
                            <div class="col-3">
                                <select class="form-select clay-input" id="P2">
                                    <option value="">%</option>
                                    <option>5</option>
                                    <option>10</option>
                                    <option>15</option>
                                    <option>20</option>
                                    <option>25</option>
                                    <option>30</option>
                                    <option>35</option>
                                    <option>40</option>
                                    <option>45</option>
                                    <option>50</option>
                                    <option>55</option>
                                    <option>60</option>
                                    <option>65</option>
                                    <option>70</option>
                                    <option>75</option>
                                    <option>80</option>
                                    <option>85</option>
                                    <option>90</option>
                                    <option>95</option>
                                    <option>100</option>
                                </select>
                            </div>
                        </div>
                        <!-- Clay 3 -->
                        <div class="row align-items-center">
                            <div class="col-2 clay-label">Clay3</div>
                            <div class="col-7">
                                <select class="form-select clay-input" id="MG_CLAY3">
                                    <option value="">-- Select Clay3 --</option>
                                    <option>ACE</option>
                                    <option>BRL</option>
                                    <option>LRH</option>
                                    <option>UBQ</option>
                                    <option>CALDYRS</option>
                                    <option>HARIMA(S)</option>
                                    <option>HARIMA(D)</option>
                                    <option>CORUS</option>
                                    <option>TRB</option>
                                    <option>VISUVIUS</option>
                                    <option>HARIMA-TWH4</option>
                                    <option>HARIMA-CPH4</option>
                                    <option>HARIMA(D)-TWH5</option>
                                    <option>HARIMA(D)-TWH5K</option>
                                    <option>HARIMA(D)TWH-5T</option>
                                    <option>HARIMA RWH-3</option>
                                    <option>HARIMA RWH-4</option>
                                    <option>HARIMA(S)RW5F</option>
                                    <option>HARIMA RWH-5</option>
                                    <option>HARIMA RWH-6</option>
                                    <option>HARIMA CB1</option>
                                    <option>RW5F</option>
                                    <option>RG15</option>
                                    <option>RG15K</option>
                                    <option>HARIMA(D)TWH-7</option>
                                    <option>HARIMA CB2</option>
                                    <option>TWH5(BELPAHAR)</option>
                                    <option>CB2(BELPAHAR)</option>
                                    <option>TWH 8(BELPAHAR)</option>
                                    <option>TWH 8 K 1(BELPAHAR)</option>
                                </select>
                            </div>
                            <div class="col-3">
                                <select class="form-select clay-input" id="P3">
                                    <option value="">%</option>
                                    <option>5</option>
                                    <option>10</option>
                                    <option>15</option>
                                    <option>20</option>
                                    <option>25</option>
                                    <option>30</option>
                                    <option>35</option>
                                    <option>40</option>
                                    <option>45</option>
                                    <option>50</option>
                                    <option>55</option>
                                    <option>60</option>
                                    <option>65</option>
                                    <option>70</option>
                                    <option>75</option>
                                    <option>80</option>
                                    <option>85</option>
                                    <option>90</option>
                                    <option>95</option>
                                    <option>100</option>
                                </select>
                            </div>
                        </div>
                    </div>
                </div>
                <!-- FOOTER -->
                <div class="modal-footer justify-content-center">
                    <button class="btn btn-save" onclick="checkClay()">Save</button>
                    <button class="btn btn-exit" data-bs-dismiss="modal">Exit</button>
                </div>
            </div>
        </div>
    </div>

    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap-datepicker@1.10.0/dist/js/bootstrap-datepicker.min.js"></script>
    <script src="~/bower_components/sweetalert/dist/Swwt2Alert.js"></script>
    <script>
        let lsSelectedFDate;
        let IsSelectedFur;
    $(document).ready(function () {
        lsSelectedFDate = '@DateTime.Today.AddDays(0).ToString("dd/MM/yyyy", new System.Globalization.CultureInfo("en-GB"))';
        $('#currDate-value').text(lsSelectedFDate);
        $('#hiddenDate').datepicker({
            format: "dd/mm/yyyy",
            autoclose: true,
            todayHighlight: true
        }).datepicker('setDate', lsSelectedFDate);
        $('#tbFDatePick').on('click', function (e) {
            e.preventDefault();
            $('#hiddenDate').datepicker('show');
        });
        $('#hiddenDate').on('changeDate', function (e) {
            lsSelectedFDate = e.format('dd/mm/yyyy');
            $('#currDate-value').text(lsSelectedFDate);           
            Display_Exception_Cast(lsSelectedFDate, IsSelectedFur);

        });
        IsSelectedFur = $('#lstFur').val();
        $('#lstFur').change(function () {
            IsSelectedFur = $(this).val();            
            Display_Exception_Cast(lsSelectedFDate, IsSelectedFur);
        });        
        Display_Exception_Cast(lsSelectedFDate, IsSelectedFur);

    });     
        
        function Display_Exception_Cast(lsSelectedFDate, IsSelectedFur) {
            $.ajax({
                url: '@Url.Action("Get_Display_Exception_Cast", "CastHouse")',
                type: 'GET',
                data: { Fdate: lsSelectedFDate, Fur: IsSelectedFur },
                success: function (result_Exception_Cast) {
                    var parsedData = JSON.parse(result_Exception_Cast);
                    var tableBody = "";
                    for (var i = 0; i < parsedData.length; i++) {

                        tableBody += "<tr>";
                        tableBody += `<td><input name="ID_NO" class='form-control form-control-md' value='${parsedData[i].ID_NO}'/></td>`;
                        tableBody += `<td>
                                                <select name="TAPHOLE_NO" class ='form-select form-select-md'>
                                                <option ${!parsedData[i].TAPHOLE_NO ? 'selected' : ''} value=""></option>
                                                <option ${parsedData[i].TAPHOLE_NO === 1 ? 'selected' : ''}>1</option>
                                                <option ${parsedData[i].TAPHOLE_NO === 2 ? 'selected' : ''}>2</option>
                                                <option ${parsedData[i].TAPHOLE_NO === 3 ? 'selected' : ''}>3</option>
                                                <option ${parsedData[i].TAPHOLE_NO === 4 ? 'selected' : ''}>4</option>
                                                </select>
                                          </td>`;
                        tableBody += `<td><input name="DATE_TIME" class='form-control form-control-lg' value='${parsedData[i].DATE_TIME}'/></td>`;
                        tableBody += `<td>
                                                <select name="HH" class ='form-select form-select-md'>
                                                <option ${!parsedData[i].HH ? 'selected' : ''} value=""></option>
                                                <option ${parsedData[i].HH === 01 ? 'selected' : ''}>01</option>
                                                <option ${parsedData[i].HH === 02 ? 'selected' : ''}>02</option>
                                                <option ${parsedData[i].HH === 03 ? 'selected' : ''}>03</option>
                                                <option ${parsedData[i].HH === 04 ? 'selected' : ''}>04</option>
                                                <option ${parsedData[i].HH === 05 ? 'selected' : ''}>05</option>
                                                <option ${parsedData[i].HH === 06 ? 'selected' : ''}>06</option>
                                                <option ${parsedData[i].HH === 07 ? 'selected' : ''}>07</option>
                                                <option ${parsedData[i].HH === 08 ? 'selected' : ''}>08</option>
                                                <option ${parsedData[i].HH === 09 ? 'selected' : ''}>09</option>
                                                <option ${parsedData[i].HH === 10 ? 'selected' : ''}>10</option>
                                                <option ${parsedData[i].HH === 11 ? 'selected' : ''}>11</option>
                                                <option ${parsedData[i].HH === 12 ? 'selected' : ''}>12</option>
                                                <option ${parsedData[i].HH === 13 ? 'selected' : ''}>13</option>
                                                <option ${parsedData[i].HH === 14 ? 'selected' : ''}>14</option>
                                                <option ${parsedData[i].HH === 15 ? 'selected' : ''}>15</option>
                                                <option ${parsedData[i].HH === 16 ? 'selected' : ''}>16</option>
                                                <option ${parsedData[i].HH === 17 ? 'selected' : ''}>17</option>
                                                <option ${parsedData[i].HH === 18 ? 'selected' : ''}>18</option>
                                                <option ${parsedData[i].HH === 19 ? 'selected' : ''}>19</option>
                                                <option ${parsedData[i].HH === 20 ? 'selected' : ''}>20</option>
                                                <option ${parsedData[i].HH === 21 ? 'selected' : ''}>21</option>
                                                <option ${parsedData[i].HH === 22 ? 'selected' : ''}>22</option>
                                                <option ${parsedData[i].HH === 23 ? 'selected' : ''}>23</option>
                                                </select>
                                          </td>`;
                        tableBody += `<td>
                                                <select name="MM" class ='form-select form-select-md'>
                                                <option ${!parsedData[i].MM ? 'selected' : ''} value=""></option>
                                                <option ${parsedData[i].MM === 00 ? 'selected' : ''}>00</option>
                                                <option ${parsedData[i].MM === 05 ? 'selected' : ''}>05</option>
                                                <option ${parsedData[i].MM === 10 ? 'selected' : ''}>10</option>
                                                <option ${parsedData[i].MM === 15 ? 'selected' : ''}>15</option>
                                                <option ${parsedData[i].MM === 20 ? 'selected' : ''}>20</option>
                                                <option ${parsedData[i].MM === 25 ? 'selected' : ''}>25</option>
                                                <option ${parsedData[i].MM === 30 ? 'selected' : ''}>30</option>
                                                <option ${parsedData[i].MM === 35 ? 'selected' : ''}>35</option>
                                                <option ${parsedData[i].MM === 40 ? 'selected' : ''}>40</option>
                                                <option ${parsedData[i].MM === 45 ? 'selected' : ''}>45</option>
                                                <option ${parsedData[i].MM === 50 ? 'selected' : ''}>50</option>
                                                <option ${parsedData[i].MM === 55 ? 'selected' : ''}>55</option>
                                                </select>
                                          </td>`;
                        tableBody += `<td><input name="TAPHOLE_LENGTH" class='form-control form-control-md' value='${parsedData[i].TAPHOLE_LENGTH}'/></td>`;
                        tableBody += `<td><input name="CLAY_PUSHED" class='form-control form-control-md' value='${parsedData[i].CLAY_PUSHED}'/></td>`;
                        tableBody += `<td>
                                                <select name="TYPE" class ='form-select form-select-lg'>
                                                <option ${!parsedData[i].TYPE ? 'selected' : ''} value=""></option>
                                                <option ${parsedData[i].TYPE === 'BLEEDING HOLE' ? 'selected' : ''}>BLEEDING HOLE</option>
                                                <option ${parsedData[i].TYPE === 'HOLE THROUGH' ? 'selected' : ''}>HOLE THROUGH</option>
                                                <option ${parsedData[i].TYPE === 'BLANK PUSH' ? 'selected' : ''}>BLANK PUSH</option>
                                                </select>
                                          </td>`;
                        tableBody += "</tr>";
                    }
                    $("#exception_cast tbody").html(tableBody);
                },
            });
        }


    </script>   
    
    <script>
    document.addEventListener("DOMContentLoaded", function () {
         let tbody = document.querySelector("#exception_cast tbody");
            for (let i = 0; i < 4; i++) {
                addRow();
            }
    });
    document.addEventListener("keydown", function (e) {
          if (e.key === "ArrowDown") {
                let active = document.activeElement;
                if (!active || !active.closest("#exception_cast tbody tr")) return;
                let tbody = document.querySelector("#exception_cast tbody");
                let rows = tbody.querySelectorAll("tr");
                let currentRow = active.closest("tr");
                let lastRow = rows[rows.length - 1];
                    // If cursor is in last row → add new row
                    if (currentRow === lastRow) {
                    addRow();
                    // Auto scroll to bottom
                    let wrapper = document.querySelector(".scrollable-table");
                    wrapper.scrollTop = wrapper.scrollHeight;
                    // Focus first field of new row
                    tbody.lastElementChild.querySelector("input, select").focus();
                    }
        }
    });
                        function addRow() {
                              let tbody = document.querySelector("#exception_cast tbody");
                              let tr = document.createElement("tr");
                                tr.innerHTML = `
                                            <td><input type="text" class="form-control form-control-sm"></td>
                                            <td><input type="text" class="form-control form-control-sm"></td>
                                                <td>
                                                    <select class="form-select form-select-sm">
                                                        <option></option>
                                                        <option>00</option>
                                                        <option>01</option>
                                                        <option>02</option>
                                                        <option>03</option>
                                                        <option>04</option>
                                                        <option>05</option>
                                                        <option>06</option>
                                                        <option>07</option>
                                                        <option>08</option>
                                                        <option>09</option>
                                                        <option>10</option>
                                                        <option>11</option>
                                                        <option>12</option>
                                                        <option>13</option>
                                                        <option>14</option>
                                                        <option>15</option>
                                                        <option>16</option>
                                                        <option>17</option>
                                                        <option>18</option>
                                                        <option>19</option>
                                                        <option>20</option>
                                                        <option>21</option>
                                                        <option>22</option>
                                                        <option>23</option>
                                                </select>
                                            </td>
                                     <td>
                                           <select class="form-select form-select-sm">
                                                <option></option>
                                                <option>00</option>
                                                <option>05</option>
                                                <option>10</option>
                                                <option>15</option>
                                                <option>20</option>
                                                <option>25</option>
                                                <option>30</option>
                                                <option>35</option>
                                                <option>40</option>
                                                <option>45</option>
                                                <option>50</option>
                                                <option>55</option>
                                        </select>
                                    </td>
                                        <td><input type="text" class="form-control form-control-sm"></td>
                                        <td><input type="text" class="form-control form-control-sm"></td>
                                <td>
                                        <select class="form-select form-select-sm">
                                            <option></option>
                                            <option>BLEEDING HOLE</option>
                                            <option>HOLE THROUGH</option>
                                            <option>BLANK PUSH</option>
                                        </select>
                                </td>
                            `;
                         tbody.appendChild(tr);
                    }

    </script>
    

</body>
</html>
