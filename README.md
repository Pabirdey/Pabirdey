   <div class="form-section">
            <div class="row g-0">
                <div class="col-md-12">
                    <div class="section-title">Tap Hole Details</div>
                    <div class="table-responsive scrollable-table">
                        <table class="table table-bordered table-sm text-center align-middle">
                            <thead class="table-light">
                                <tr>
                                    <th class="Long_Heading_Medium">Cast No</th>
                                    <th>Trough No</th>
                                    <th class="Long_Heading_Medium">Cast Start</th>
                                    <th class="Long_Heading_Medium">Cast End</th>
                                    <th class="Long_Heading_Medium">Gutko</th>
                                    <th class="Long_Heading_Medium">Cast Duration</th>
                                    <th class="Long_Heading_Medium">Casting Rate(t/min)</th>
                                    <th class="Long_Heading_Medium">TLC</th>
                                    <th class="Long_Heading_Medium">OT</th>
                                    <th class="Long_Heading_Medium">Cast Ready Time</th>
                                    <th class="Long_Heading_Medium" style="max-width:100px;white-space:normal;word-wrap:break-word;">Splashing/Wetness Time</th>
                                    <th class="Long_Heading_Medium">Cast Type</th>
                                    <th class="Long_Heading_Medium">Clay Condition</th>
                                    <th class="Long_Heading_Medium">Taphole Behaviour at End Cast</th>
                                    <th class="Long_Heading_Medium">HMT Before Slag</th>
                                    <th class="Long_Heading_Medium">HMT After Slag</th>
                                    <th class="Long_Heading_Medium">Final HM Temp</th>
                                    <th class="Long_Heading_Medium">HM Weight</th>
                                </tr>
                            </thead>
                            <tbody id="TAP_Hot_Metal_Details"></tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>
        <style>
        body {
            background-color: #f8f9fa;
        }

        .table-input {
            font-size: 0.80rem;
            padding: 2px 4px;
            border:2px solid;
        }

        .form-section {
                background: #ffffff;
                padding: 20px;
                border-radius: 12px;
                box-shadow: 0 10px 20px rgba(0,0,0,0.1); /* slightly stronger shadow */
                margin-bottom:20px;
                overflow: visible;
            }



        .section-title {
            background: #8053A8;
            color: #fff;
            padding: 5px 10px;
            margin-bottom: 10px;
            font-weight: bold;
            border-radius: 4px;
            text-align: left;
        }

        .form-control-lg {
            font-size: 1.7rem;
            font-family: Courier New, Courier, monospace;
        }

        th {
            font-family: Courier New, Courier, monospace;
            font-size: 16px;
            font-weight: bold;
            border:1px solid;
        }

        .scrollable-table {
            max-height:275px;
            overflow-y: auto;
        }

        .table thead th {
            position: sticky;
            top: 0;
            background-color: #e9ecef;
            z-index: 2;
            border:1px solid;
        }
        .Long_Heading_Medium{
            min-width:100px;
        }
    </style>
