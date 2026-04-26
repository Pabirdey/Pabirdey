  <style>
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

        /* TABLE */
        .table th {
            background: #1565c0;
            color: white;
            font-size: 11px;
            padding: 3px;
        }

        .table td {
            background: white;
            color: black;
            font-size: 11px;
            padding: 3px;
        }

        /* SMALL INPUT (Tab 1 & 2) */
        .table input,
        .table select {
            width: 100%;
            font-size: 8px;
            height: 24px;
            text-align: center;
        }

        /* ✅ MEDIUM INPUT ONLY FOR RAW MATERIAL TAB */
        .table-container input {
            height: 25px;
            font-size: 12px;
            border-radius: 6px;
            padding: 5px;
        }

        .table-custom td {
            vertical-align: middle;
        }

        textarea {
            height: 40px;
            font-size: 11px;
        }

        .form-control,
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

        /* TABS */
        .nav-tabs {
            border-bottom: 2px solid #1976d2;
        }

        .nav-tabs .nav-link {
            color: #1565c0;
            font-weight: 600;
            border-radius: 8px 8px 0 0;
            margin-right: 5px;
            background: #e3f2fd;
        }

        .nav-tabs .nav-link.active {
            background: linear-gradient(to right, #0d47a1, #1976d2);
            color: white !important;
        }

        .tab-pane {
            animation: fadeIn 0.3s ease-in-out;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(5px); }
            to { opacity: 1; transform: translateY(0); }
        }
    </style>
       <!-- TAB 3 -->
        <div class="tab-pane fade" id="tab3">
            <div class="container mt-4">
                <div class="card-custom">
                    <h4 class="text-center mb-4" style="font-size:32px;">Raw Material Position</h4>
                    <div class="table-container">
                        <table class="table table-bordered table-custom">
                            <thead>
                                <tr>
                                    <th>Material</th>
                                    <th>Yard Position</th>
                                    <th>H.L. Position</th>
                                    <th>Stock Loaded</th>
                                    <th>C-BF</th>
                                    <th>E-BF</th>
                                    <th>F-BF</th>                                    
                                </tr>
                            </thead>

                            <tbody>
                                <tr>
                                    <td class="material-name">SINTER</td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>                                    
                                </tr>                            
                                <tr>
                                    <td class="material-name">TFO</td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>                                    
                                </tr>
                                <tr>
                                    <td class="material-name">LRP</td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>
                                    <td><input type="text" class="form-control"></td>                                    
                                </tr>
                            <tr>
                                <td class="material-name">JODA</td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>                                
                            </tr>
                            <tr>
                                <td class="material-name">Pellet</td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>                                
                            </tr>
                            <tr>
                                <td class="material-name">Nut Coke</td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>                                
                            </tr>
                            <tr>
                                <td class="material-name">Limestone</td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                            </tr>
                            <tr>
                                <td class="material-name">Pyroxinite</td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                            </tr>
                            <tr>
                                <td class="material-name">ORT</td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>                                
                            </tr>
                            <tr>
                                <td class="material-name">Scrap</td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                            </tr>
                            <tr>
                               <td class="material-name">Coke(On Stock)</td> 
                               <td><input type="text" class="form-control"></td>
                               <td><input type="text" class="form-control"></td>
                               <td><input type="text" class="form-control"></td>
                               <td><input type="text" class="form-control"></td>
                               <td><input type="text" class="form-control"></td>
                               <td><input type="text" class="form-control"></td>
                            </tr>
                            <tr>
                                <td class="material-name">Low Ash Coke</td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                            </tr>
                            <tr>
                                <td class="material-name">High Ash Coke</td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                                <td><input type="text" class="form-control"></td>
                            </tr>
                        </tbody>
                        </table>
                    </div>

                </div>

            </div>

        </div>
