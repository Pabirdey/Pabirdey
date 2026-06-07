<div class="tab-content">
            <!-- TAB 1 -->
            <div class="tab-pane fade show active" id="tab1">
                <div class="row mt-2">
                    <div class="col-md-11">
                        <div class="section-box">  
                            <div class="table-container">
                                <table class="table table-bordered text-center">
                                    <thead>
                                        <tr>
                                            <th>CastNo</th>
                                            <th>Start</th>
                                            <th>End</th>
                                            <th>Ladle No</th>
                                            <th>Start</th>
                                            <th>End</th>
                                            <th>Arrived From</th>
                                            <th>Gross</th>
                                            <th>Tare</th>
                                            <th>Net </th>
                                            <th>Pouring Rate</th>
                                            <th>HMT</th>
                                            <th>Reason For Outage</th>
                                            <th>Seq_No</th>
                                            <th>Delete</th>
                                        </tr>
                                    </thead>
                                    <tbody id="tblBody">
                                      <tr></tr>
                                    </tbody>
                                </table>
                            </div>                                                      
                         </div>                       
                        <div class="row">
                            <!-- Hot Metal Analysis -->
                            <div class="col-md-6 col-12">
                                <div class="section-box">
                                  <div class="section-title text-center">Hot Metal Analysis</div>
                                    <div class="table-container">
                                        <table class="table table-bordered text-center">
                                            <thead>
                                                <tr>
                                                    <th>CastNo</th>
                                                    <th>TrpNo</th>
                                                    <th>Time</th>
                                                    <th>C</th>
                                                    <th>Si</th>
                                                    <th>S</th>
                                                    <th>Mn</th>
                                                    <th>Ti</th>
                                                    <th>P</th>
                                                    <th>Cr</th>
                                                    <th>B</th>
                                                </tr>
                                            </thead>
                                            <tbody id="tblHotMetalBody"></tbody>
                                        </table>
                                    </div>
                                </div>
                            </div>                           
                            <div class="col-md-6 col-12">
                                <div class="section-box">
                                    <div class="section-title text-center">ONDate Production Summary</div>
                                    <table class="table table-bordered text-center" id="nutTable">
                                        <thead>
                                            <tr>
                                                <th></th>
                                                <th>LD1</th>
                                                <th>LD2</th>
                                                <th>LD3</th>
                                                <th>Granshot</th>
                                                <th>MRD</th>
                                                <th>TOT</th>
                                                <th>Exp Prod</th>
                                            </tr>
                                        </thead>
                                        <tbody style="width:10%">
                                            <!-- C -->
                                            <tr>
                                                <td class="row-title">C</td>
                                                <td><input class="prod-input" value="397"></td>
                                                <td><input class="prod-input" value="0"></td>
                                                <td><input class="prod-input" value="450.15"></td>
                                                <td><input class="prod-input" value="0"></td>
                                                <td><input class="prod-input" value="0"></td>
                                                <td class="tot-color">1214.4</td>
                                                <td class="exp-color">1943.0</td>
                                            </tr>
                                            <!-- E -->
                                            <tr>
                                                <td class="row-title">E</td>
                                                <td><input class="prod-input" value="459.98"></td>
                                                <td><input class="prod-input" value="0"></td>
                                                <td><input class="prod-input" value="0"></td>
                                                <td><input class="prod-input" value="0"></td>
                                                <td><input class="prod-input" value="0"></td>
                                                <td class="tot-color">564.9</td>
                                                <td class="exp-color">903.9</td>
                                            </tr>
                                            <!-- F -->
                                            <tr>
                                                <td class="row-title">F</td>
                                                <td><input class="prod-input" value="2166.01"></td>
                                                <td><input class="prod-input" value="0"></td>
                                                <td><input class="prod-input" value="0"></td>
                                                <td><input class="prod-input" value="344.4"></td>
                                                <td><input class="prod-input" value="0"></td>
                                                <td class="tot-color">2611.2</td>
                                                <td class="exp-color">4177.9</td>
                                            </tr>
                                            <!-- Total A-F -->
                                            <tr class="summary-row">
                                                <td>TotA-F</td>
                                                <td>3022.99</td>
                                                <td>0</td>
                                                <td>450.15</td>
                                                <td>344.4</td>
                                                <td>0</td>
                                                <td>4390.5</td>
                                                <td>7024.8</td>
                                            </tr>
                                            <!-- G -->
                                            <tr>
                                                <td class="row-title">G</td>
                                                <td><input class="prod-input" value="239"></td>
                                                <td><input class="prod-input" value="2758.14"></td>
                                                <td><input class="prod-input" value="946.7"></td>
                                                <td><input class="prod-input" value="0"></td>
                                                <td><input class="prod-input" value="0"></td>
                                                <td class="tot-color">4049.3</td>
                                                <td class="exp-color">6478.9</td>
                                            </tr>
                                            <!-- H -->
                                            <tr>
                                                <td class="row-title">H</td>
                                                <td><input class="prod-input" value="244.3"></td>
                                                <td><input class="prod-input" value="3465.35"></td>
                                                <td><input class="prod-input" value="1750"></td>
                                                <td><input class="prod-input" value="0"></td>
                                                <td><input class="prod-input" value="0"></td>
                                                <td class="tot-color">5459.7</td>
                                                <td class="exp-color">8735.4</td>
                                            </tr>
                                            <!-- I -->
                                            <tr>
                                                <td class="row-title">I</td>
                                                <td><input class="prod-input" value="2703.1"></td>
                                                <td><input class="prod-input" value="0"></td>
                                                <td><input class="prod-input" value="2066.76"></td>
                                                <td><input class="prod-input" value="744.2"></td>
                                                <td><input class="prod-input" value="0"></td>
                                                <td class="tot-color">5751.5</td>
                                                <td class="exp-color">9202.4</td>
                                            </tr>
                                            <!-- Total A-I -->
                                            <tr class="summary-row">
                                                <td>TotA-I</td>
                                                <td>6209.39</td>
                                                <td>6223.49</td>
                                                <td>6213.61</td>
                                                <td>1088.6</td>
                                                <td>0</td>
                                                <td>18669.3</td>
                                                <td>31441.5</td>
                                            </tr>
                                        </tbody>
                                    </table>
                                </div>
                            </div>
                          </div>        
                                                    
                    </div>                   
                </div>
            </div>         
        </div>
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
            background: #f4f6f9;
            font-family: Verdana;
            font-size: 12px;
            transform: scale(0.99);
            transform-origin: top left;
        }

        .container-fluid {
            max-width: 1600px;
        }

        /* HEADER */
        .header-box {
            background: #0d47a1;
            color: white;
            padding: 6px;
            border-radius: 6px;
        }

            .header-box h4 {
                font-size: 16px;
            }

        /* SECTION */
        .section-box {
            background: #1976d2;
            color: white;
            padding: 6px;
            border-radius: 6px;
            margin-top: 6px;
        }

        .section-title {
            font-size: 13px;
            font-weight: 600;
            margin-bottom: 4px;
        }

        .table th {
            background: #1565c0;
            color: white;
            font-size: 14px;
            padding: 3px;
        }

        .table td {
            background: white;
            color: black;
            font-size: 14px;
            padding: 3px;
        }

        


        .table-custom td {
            vertical-align: middle;
        }

        textarea {
            height: 40px;
            font-size: 11px;
        }

        .table-input,
        .form-select {
            font-size: 12px;
            height: 28px;
        }

        .card-custom {
            background: linear-gradient(to right, #0d47a1, #1976d2);
            border-radius: 20px;
            padding: 10px;
            color: white;
        }            
       
        /* Small Box */
        .blue-box {
            background: #0066ff;
            border-radius: 14px;
            padding: 10px 15px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            width: 320px;
            margin-top: 120px;
            box-shadow: 0 3px 8px rgba(0,0,0,0.2);
        }

        .left-section {
            width: 58%;
        }

        /* Small Input */
        .custom-input {
            height: 27px;
            border: 2px solid #999;
            border-radius: 5px;
            font-size: 13px;
            font-family: Arial;
            font-weight: bold;
            padding-left: 10px;
        }

            .custom-input:focus {
                box-shadow: none;
                border-color: #222;
            }       

        /* Small Checkbox */
        .form-check-input {
            width: 19px;
            height: 19px;
            cursor: pointer;
            margin-top: 0;
        }
       
         .table-container {
            max-height: 258px; /* Height of 8 rows approximately */
            overflow-y: auto;
            overflow-x: auto;
            border: 1px solid #ccc;
        }
            .table {
            margin-bottom: 0;
            white-space: nowrap;
        }

        .table th {
            background: #1565c0;
            color: white;
            font-size: 14px;
            padding: 5px;
            position: sticky;
            top: 0;
            z-index: 100;
        }

        .table td {
            background: white;
            color: black;
            font-size: 14px;
            padding: 5px;
        }
        .table-input {
            border: none !important;
            outline: none !important;
            box-shadow: none !important;
            background: transparent;
            width: 100%;
            padding: 2px;
            line-height:16px;
            height:16px;
            }

        .table-input:focus {
            border: none !important;
            outline: none !important;
            box-shadow: none !important;
        }
        
    </style>
