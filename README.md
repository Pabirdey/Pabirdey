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

    <style>
        /* ===== Headings ===== */
        .Main-Heading {
            font-family: Allan, cursive;
            font-weight: bold;
            font-size: 6vh;
            text-align: center;
            padding: 20px;
            color: rgb(57,57,57);
            text-shadow: rgba(13,0,77,0.08) 0px 2px 4px;
            border-radius: 10px;
            margin: 20px 0;
        }

        /* ===== Sections ===== */
        .form-section {
            background: #fff;
            padding: 20px;
            border-radius: 20px;
            box-shadow: 0 10px 20px rgba(0,0,0,0.1);
            margin-bottom: 25px;
            border: 1px solid #ccc;
            font-family: Courier New, Courier, monospace;
        }

        .section-title {
            background: #EEB86D;
            padding: 5px 10px;
            font-weight: bold;
            border-radius: 10px;
            margin-bottom: 10px;
            font-size: 18px;
        }

        /* ===== Table ===== */
        .scrollable-table {
            max-height: 280px;
            overflow-y: auto;
        }

        /* HEADER FIX */
        .tap-header {
            background-color: #343a40 !important;
            color: white !important;
            font-weight: bold;
            font-size: 14px;
            border: 1px solid #000;
            position: sticky;
            top: 0;
            z-index: 10;
            text-align: center;
            vertical-align: middle;
        }

        .table td {
            text-align: center;
            vertical-align: middle;
        }

        /* Column widths */
        .Long_Heading { min-width: 130px; }
        .Long_Heading_Medium { min-width: 100px; }
    </style>
</head>

<body>

<div class="Main-Heading">Cast House Details</div>

<div class="container-fluid">
    <div class="form-group mb-3">
        <label style="font-family:Allan,cursive;font-size:22px;">Date :</label>
        <input id="tbFDatePick" size="14" style="height:28px;text-align:center">

        &nbsp;&nbsp;&nbsp;

        <label style="font-family:Allan,cursive;font-size:22px;">Furnace :</label>
        <select id="lstFur">
            <option value="C">C</option>
            <option value="D">D</option>
            <option value="E">E</option>
            <option value="F">F</option>
            <option value="G">G</option>
            <option value="H">H</option>
            <option value="I">I</option>
        </select>
    </div>

    <div class="form-section">
        <div class="section-title">Tap Hole Details / Hot Metal Details</div>

        <div class="table-responsive scrollable-table">
            <table class="table table-bordered table-sm" id="TAP_Hot_Metal_Details">
                <thead>
                <tr>
                    <th class="tap-header">Cast No</th>
                    <th class="tap-header">Trough No</th>
                    <th class="tap-header">Cast Start</th>
                    <th class="tap-header">Cast End</th>
                    <th class="tap-header">Gutko</th>
                    <th class="tap-header">Cast Duration</th>
                    <th class="tap-header">Casting Rate</th>
                    <th class="tap-header">TLC</th>
                    <th class="tap-header">OT</th>
                    <th class="tap-header">Cast Ready Time</th>
                    <th class="tap-header">Splashing / Wetness</th>
                    <th class="tap-header">Cast Type</th>
                    <th class="tap-header">Clay Condition</th>
                    <th class="tap-header">Taphole Behaviour</th>
                    <th class="tap-header">HMT Before Slag</th>
                    <th class="tap-header">HMT After Slag</th>
                    <th class="tap-header">Final HM Temp</th>
                    <th class="tap-header">HM Weight</th>
                </tr>
                </thead>
                <tbody></tbody>
            </table>
        </div>
    </div>
</div>

<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/bootstrap-datepicker@1.10.0/dist/js/bootstrap-datepicker.min.js"></script>

<script>
    let lsSelectedFDate;
    let IsSelectedFur;

    $(document).ready(function () {

        let today = new Date();
        lsSelectedFDate =
            ("0" + today.getDate()).slice(-2) + "/" +
            ("0" + (today.getMonth() + 1)).slice(-2) + "/" +
            today.getFullYear();

        $('#tbFDatePick').datepicker({
            format: "dd/mm/yyyy",
            autoclose: true,
            todayHighlight: true
        }).val(lsSelectedFDate);

        IsSelectedFur = $('#lstFur').val();
        Display_Tap_Hole_Details(lsSelectedFDate, IsSelectedFur);

        $('#lstFur').change(function () {
            IsSelectedFur = $(this).val();
            Display_Tap_Hole_Details(lsSelectedFDate, IsSelectedFur);
        });

        $('#tbFDatePick').on('changeDate', function () {
            lsSelectedFDate = $(this).val();
            Display_Tap_Hole_Details(lsSelectedFDate, IsSelectedFur);
        });
    });

    function Display_Tap_Hole_Details(date, fur) {
        $.ajax({
            url: '/CastHouse/Get_TAP_Hole_Metal_Details',
            type: 'GET',
            data: { Fdate: date, Fur: fur },
            success: function (result) {
                let data = JSON.parse(result);
                let rows = "";

                $.each(data, function (i, d) {
                    rows += `
                        <tr>
                            <td><input class="form-control form-control-sm" value="${d.CAST_NO}" readonly></td>
                            <td><input class="form-control form-control-sm" value="${d.TROUGH_NO}" readonly></td>
                            <td><input class="form-control form-control-sm" value="${d.CAST_ST_TIME}" readonly></td>
                            <td><input class="form-control form-control-sm" value="${d.CAST_END_TIME}" readonly></td>
                            <td><input class="form-control form-control-sm" value="${d.GUTKO}" readonly></td>
                            <td><input class="form-control form-control-sm" value="${d.CAST_DURATION}" readonly></td>
                            <td><input class="form-control form-control-sm" value="${d.SPEED}" readonly></td>
                            <td><input class="form-control form-control-sm" value="${d.NO_TLC}" readonly></td>
                            <td><input class="form-control form-control-sm" value="${d.NO_OT}" readonly></td>
                            <td><input class="form-control form-control-sm" value="${d.CH_READY_TIME}"></td>
                            <td><input class="form-control form-control-sm" value="${d.SPLACING_WETNESS_TIME}"></td>
                            <td><input class="form-control form-control-sm" value="${d.CAST_TYPE}"></td>
                            <td><input class="form-control form-control-sm" value="${d.CAST_CLAY_COND}"></td>
                            <td><input class="form-control form-control-sm" value="${d.TAPHOLE_BEHAVIOUR}"></td>
                            <td><input class="form-control form-control-sm" value="${d.HM_BEFORE_SLAG}"></td>
                            <td><input class="form-control form-control-sm" value="${d.HM_AFTER_SLAG}"></td>
                            <td><input class="form-control form-control-sm" value="${d.HM_TEMP}"></td>
                            <td><input class="form-control form-control-sm" value="${d.HM_WEIGHT}"></td>
                        </tr>`;
                });

                $("#TAP_Hot_Metal_Details tbody").html(rows);
            }
        });
    }
</script>

</body>
</html>