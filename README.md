<!DOCTYPE html>
<html>
<head>
    <title>Steel Plant Table Theme</title>

    <style>
        /* ====== TABLE BORDER ====== */
        #TAP_Hot_Metal_Details {
            border: 2px solid #6c757d;   /* steel grey */
            background-color: #ffffff;
        }

        /* ====== TABLE HEADER ====== */
        #TAP_Hot_Metal_Details thead th {
            background: linear-gradient(180deg, #5a6d7c, #3f4f5c); /* steel blue-grey */
            color: #ffffff;
            font-weight: 700;            /* bold heading */
            border: 1px solid #2f3e46;
            text-align: center;
            vertical-align: middle;
            padding: 8px;
        }

        /* ====== TABLE BODY ====== */
        #TAP_Hot_Metal_Details tbody td {
            border: 1px solid #b0b8bf;
            padding: 6px;
            background-color: #f8f9fa;
        }

        /* ====== ROW HOVER ====== */
        #TAP_Hot_Metal_Details tbody tr:hover {
            background-color: #e3edf5;
        }

        /* ====== STICKY HEADER FOR SCROLL ====== */
        .scrollable-table thead th {
            position: sticky;
            top: 0;
            z-index: 2;
        }

        /* ====== OPTIONAL: HEADING FONT ====== */
        .Long_Heading,
        .Long_Heading_Medium {
            font-size: 13px;
            letter-spacing: 0.4px;
        }
    </style>
</head>

<body>

<div class="table-responsive scrollable-table" style="max-height:300px;">
    <table class="table table-bordered table-sm text-center align-middle" id="TAP_Hot_Metal_Details">
        <thead>
            <tr>
                <th class="Long_Heading_Medium">Cast No</th>
                <th>Trough No</th>
                <th class="Long_Heading_Medium">Cast Start</th>
                <th class="Long_Heading_Medium">Cast End</th>
                <th class="Long_Heading_Medium">Gutko</th>
                <th class="Long_Heading_Medium">Cast Duration</th>
                <th class="Long_Heading_Medium">Casting Rate (t/min)</th>
                <th class="Long_Heading_Medium">TLC</th>
                <th class="Long_Heading_Medium">OT</th>
                <th class="Long_Heading_Medium">Cast Ready Time</th>
                <th class="Long_Heading_Medium" style="max-width:90px;white-space:normal;">
                    Splashing / Wetness Time
                </th>
                <th class="Long_Heading" style="width:132px;">Cast Type</th>
                <th style="width:132px;">Clay Condition</th>
                <th style="width:220px;">Taphole Behaviour at End Cast</th>
                <th class="Long_Heading_Medium">HMT Before Slag</th>
                <th class="Long_Heading_Medium">HMT After Slag</th>
                <th class="Long_Heading_Medium">Final HM Temp</th>
                <th class="Long_Heading_Medium">HM Weight</th>
            </tr>
        </thead>
        <tbody>
            <!-- Data rows -->
        </tbody>
    </table>
</div>

</body>
</html>