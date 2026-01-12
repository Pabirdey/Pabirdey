<!DOCTYPE html>
<html lang="en">
<head>
    <title>Cast House Details</title>    
    <link rel="stylesheet" href="@Url.Content("~/bower_components/bootstrap-datepicker/dist/css/bootstrap-datepicker3.standalone.min.css")" media="screen">
    <link href="@Url.Content("~/bower_components/bootstrap-daterangepicker/bootstrap-daterangepicker-1.3.21.css")" rel="stylesheet" />
    <link href="~/bower_components/folder-explorer/font-awesome.min.css" rel="stylesheet" />
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
    <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>    
    <style>
        .table-input {
            font-size: 1rem;
            padding: 2px 4px;
            border: 2px solid;
        }

        .my-swal-popup {
            font-family: 'Arial', sans-serif;
        }

        .my-swal-title {
            font-family: 'Georgia', serif;
            font-size: 22px;
        }

        .my-swal-text {
            font-family: 'Verdana', sans-serif;
            font-size: 18px;
        }

        .form-section {
            background: #ffffff;
            padding: 20px;
            border-radius: 20px;
            box-shadow: 0 10px 20px rgba(0,0,0,0.1);
            margin-bottom: 25px;
            overflow: visible;
            font-family: Courier New, Courier, monospace;
        }

        .section-title {
            background: #EEB86D;
            color: black;
            padding: 5px 10px;
            margin-bottom: 10px;
            font-weight: bold;
            border-radius: 10px;
            text-align: left;
            font-family: Courier New, Courier, monospace;
            font-size: 18px;
        }

        .form-control-lg {
            font-size: 1rem;
            font-family: Courier New, Courier, monospace;
            color: black;
        }

        th {
            font-family: Courier New, Courier, monospace;
            font-size: 14px;
            font-weight: bold;
            border: 1px solid;
            color: white;
        }

        .scrollable-table {
            overflow-y: auto;
        }

        .table thead th {
            position: sticky;
            top: 0;
            z-index: 2;
            border: 5px solid;
        }

        .Long_Heading_Medium {
            min-width: 100px;
            border: 1px solid black;
        }

        .Heading_Tiny {
            width: 20px;
            white-space: nowrap;
        }

        .Long_Heading {
            min-width: 130px;
        }

        .section_Exception-title {
            background: #EEB86D;
            color: black;
            padding: 5px 10px;
            margin-bottom: 10px;
            font-weight: bold;
            border-radius: 10px;
            text-align: left;
            font-family: Courier New, Courier, monospace;
            font-size: 15px;
            width: 15vh;
        }

        .Heading_Small {
            width: 10px;
            white-space: nowrap;
        }

        .section-Drill-title {
            background: #EEB86D;
            color: black;
            padding: 5px 10px;
            margin-bottom: 10px;
            font-weight: bold;
            border-radius: 4px;
            text-align: left;
            font-family: Courier New, Courier, monospace;
            font-size: 20px;
        }

        .form-group {
            border-radius: 25px;
            border: 4px solid #73AD21;
            padding: 10px;
            margin: 10px;
            width: 500px;
        }

         
               select {
            appearance: auto !important;
            -webkit-a ppearance: auto !important;
            -moz-appearance: auto !important;
        }


        .Main-Heading {
            font-family: Allan,cursive;
            font-weight: bold;
            font-size: 6vh;
            text-align: center;
            padding: 20px;
            color: rgb(57,57,57);
            text-shadow: rgba(13, 0, 77, 0.08) 0px 2px 4px, rgba(13, 0, 77, 0.08) 0px 3px 6px, rgba(13, 0, 77, 0.08) 0px 8px 16px;
            border-radius: 10px;
        }

        #backgrcol_Tap_hole {
            color: white;
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

        .input-wrapper {
            display: flex;
            border: 1px solid #999;
        }

            .input-wrapper input {
                border: none;
                outline: none;
            }

        .arrow-btn {
            width: 30px;
            text-align: center;
            cursor: pointer;
            background: #f0f0f0;
        }

        .list-box {
            border: 1px solid #999;
            display: none;
            background: #fff;
            position: absolute;
            z-index: 999;
        }

            .list-box div {
                padding: 5px;
                cursor: pointer;
            }

                .list-box div:hover {
                    background: #e6e6e6;
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
    <div class="Main-Heading mt-0">Cast House Details</div>
    <div class="container-fluid mt-0">
        <div class="form-group">
            <label for="tbFDatePick" class="LabelControl" style="font-family:Allan,cursive;font-size:22px;">Date:&nbsp;</label>
            <input id="tbFDatePick" size="14" style="height:28px;text-align:center">
            &nbsp;&nbsp;&nbsp;&nbsp;
            <span>
                <lable style="font-family:Allan,cursive;font-size:25px;">Furnace</lable>
                <select id="lstFur">
                    <option value="C">C</option>
                    <option value="E">E</option>
                    <option value="F">F</option>
                    <option value="G">G</option>
                    <option value="H">H</option>
                    <option value="I">I</option>
                </select>
            </span>
        </div>
        <div class="mt-1">         
            <!-- Mudgun Details -->
            <div class="form-section">
                <div class="section-title">Mudgun Details</div>
                <div class="table-responsive scrollable-table" style="max-height:318px;">
                    <table class="table table-bordered table-sm text-center align-middle" id="Mudgun_Details">
                        <thead>
                            <tr>
                                <th class="Long_Heading_Medium">Cast No</th>
                                <th style="width:115px;min-width:115px;box-sizing:border-box;">Closure Mode</th>
                                <th style="width:115px;min-width:115px;box-sizing:border-box;">Clay Qty. Pushed</th>                              
                            </tr>
                        </thead>
                        <tbody></tbody>
                    </table>
                </div>
            </div>
                    
        </div>
    </div>  
   
    <div class="modal fade" id="clayModal" tabindex="-1">
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
                                <select class="form-select clay-input" id="clay1">
                                    <option value="">-- Select Clay1 --</option>
                                    <option value="CLAY_A">Clay A</option>
                                    <option value="CLAY_B">Clay B</option>
                                    <option value="CLAY_C">Clay C</option>
                                </select>
                            </div>
                            <div class="col-3">
                                <select class="form-select clay-input">
                                    <option></option>
                                    <option></option>
                                </select>
                            </div>
                        </div>

                        <!-- Clay 2 -->
                        <div class="row align-items-center mb-3">
                            <div class="col-2 clay-label">Clay2</div>
                            <div class="col-7">
                                <!-- <input type="text" class="form-control clay-input" id="clay2"> -->
                                <select class="form-select clay-input" id="clay2">
                                    <option value="">-- Select Clay2 --</option>
                                    <option value="CLAY_A">Clay A</option>
                                    <option value="CLAY_B">Clay B</option>
                                    <option value="CLAY_C">Clay C</option>
                                </select>
                            </div>
                            <div class="col-3">
                                <select class="form-select clay-input">
                                    <option></option>
                                    <option></option>
                                </select>
                            </div>
                        </div>

                        <!-- Clay 3 -->
                        <div class="row align-items-center">
                            <div class="col-2 clay-label">Clay3</div>
                            <div class="col-7">
                                <!-- <input type="text" class="form-control clay-input" id="clay3"> -->
                                <select class="form-select clay-input" id="clay3">
                                    <option value="">-- Select Clay3 --</option>
                                    <option value="CLAY_A">Clay A</option>
                                    <option value="CLAY_B">Clay B</option>
                                    <option value="CLAY_C">Clay C</option>
                                </select>
                            </div>
                            <div class="col-3">
                                <select class="form-select clay-input">
                                    <option></option>
                                    <option></option>
                                </select>
                            </div>
                        </div>

                    </div>

                </div>

                <!-- FOOTER -->
                <div class="modal-footer justify-content-center">
                    <button class="btn btn-save" onclick="saveData()">Save</button>
                    <button class="btn btn-exit" data-bs-dismiss="modal">Exit</button>
                </div>

            </div>
        </div>
    </div>


</body>
</html>
@section scripts {
    <script src="@Url.Content("~/bower_components/moment/moment.min.js")"></script>
    <script src="@Url.Content("~/bower_components/bootstrap-datepicker/dist/js/bootstrap-datepicker.min.js")"></script>        
    <script src="~/bower_components/sweetalert/dist/Swwt2Alert.js"></script>            
    <script type="text/javascript">
        let lsSelectedFDate, lsSelectedTDate;
        $(document).ready(function () {
            lsSelectedFDate = '@DateTime.Today.AddDays(0).ToString("dd/MM/yyyy", new System.Globalization.CultureInfo("en-GB"))';
            let today = '@DateTime.Today.AddDays(0).ToString("dd/MM/yyyy", new System.Globalization.CultureInfo("en-GB"))';
            $('#tbFDatePick').datepicker({
                format: "dd/mm/yyyy",
                autoclose: true,
                todayHighlight: true,
                changeMonth: true,
                changeYear: true,
                setDate: lsSelectedFDate,
            });
            var fData;
            $('#tbFDatePick').val(lsSelectedFDate);
            $('#tbFDatePick').on('changeDate', function () {
                let getFormattedDate = $('#tbFDatePick').datepicker('getFormattedDate');
                $('#tbFDatePick').val(getFormattedDate);
                lsSelectedFDate = $('#tbFDatePick').val();               
                Display_Mudgun_Details(lsSelectedFDate,IsSelectedFur);            
            });
            var IsSelectedFur;
            $('#lstFur').change(function () {
                IsSelectedFur = $('#lstFur option:selected').val();                
                Display_Mudgun_Details(lsSelectedFDate, IsSelectedFur);               
            });

        
            function Display_Mudgun_Details(lsSelectedFDate, IsSelectedFur) {
                $.ajax({
                    url: '@Url.Action("Get_Display_Mudgun_Details", "CastHouse")',
                    type: 'GET',
                    data: { Fdate: lsSelectedFDate, Fur: IsSelectedFur },
                    success: function (result_Mudgun_Details) {

                        var parsedData = JSON.parse(result_Mudgun_Details);
                        var tableBody = "";

                        for (var i = 0; i < parsedData.length; i++) {

                            tableBody += `<tr data-castno='${parsedData[i].CAST_NO}'>`;

                            tableBody += `<td>
                                <input name="CAST_NO"
                                       class='form-control form-control-lg'
                                       value='${parsedData[i].CAST_NO}' readonly/>
                              </td>`;

                            tableBody += `<td>
                    <select name="CLOSURE_MODE" class='form-select form-select-lg'>
                        <option ${!parsedData[i].CLOSURE_MODE ? 'selected' : ''} value=""></option>
                        <option ${parsedData[i].CLOSURE_MODE === 'MUDGUN' ? 'selected' : ''}>MUDGUN</option>
                        <option ${parsedData[i].CLOSURE_MODE === 'NULL' ? 'selected' : ''}>NULL</option>
                    </select>
                </td>`;

                            tableBody += `
                                        <td>
                                        <div class="input-wrapper">
                                        <input type="text" class="form-control form-control-lg clay-input" id="clayInput_${i}" name="MG_CLAY_USED" value="${parsedData[i].MG_CLAY_USED || ''}">
                                        <div class ="arrow-btn" onclick="toggleList(${i})">▼</div>
                                        </div>
                                        <div class="list-box" id="list_${i}">
                                        <div onclick="selectItem(this, ${i})">ACE</div>
                                        <div onclick="selectItem(this, ${i})">BRL</div>
                                        <div onclick="selectItem(this, ${i})">LRH</div>
                                        <div onclick="selectItem(this, ${i})">UBQ</div>
                                        <div onclick="selectItem(this, ${i})">OTHERS</div>                                       
                                </div>
                            </td>`;    
                            tableBody += `</tr>`;
                        }
                        $("#Mudgun_Details tbody").html(tableBody);
                    }
                });
            }           

     });
    </script>    
 <script>
var activeRowIndex = null;
debugger;
function toggleList(index) {
    var list = document.getElementById("list_" + index);
    list.style.display = (list.style.display === "block") ? "none" : "block";
}

function selectItem(el, index) {

    document.getElementById("clayInput_" + index).value = el.innerText;
    document.getElementById("list_" + index).style.display = "none";

    // ✅ IF OTHERS → OPEN MODAL
    if (el.innerText.trim() === "OTHERS") {
        debugger;
        activeRowIndex = index;   // store row index (important)

        var modal = new bootstrap.Modal(
            document.getElementById("clayModal")
        );
        modal.show();             // ✅ THIS OPENS MODAL
    }
}

// Close all lists when clicking outside
document.addEventListener("click", function (e) {
    if (!e.target.closest(".input-wrapper") &&
        !e.target.closest(".list-box")) {

        document.querySelectorAll(".list-box").forEach(function (l) {
            l.style.display = "none";
        });
    }
});
</script>

}
