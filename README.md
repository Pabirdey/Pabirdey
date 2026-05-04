<div class="main-content">
        <div class="container">
            <div class="card">
                <h3 class="text-center">Pile Mat Wise Quality Data</h3>
                <div id="loader">Loading...</div>
                <table class="table table-bordered text-center" id="finesTable">
                    <thead>
                        <tr>
                            <th>Element</th>
                            <th>Return Fines</th>
                            <th>Wet Fines</th>
                            <th>Dry Fines</th>
                            <th>Dry Fines 500TPH</th>
                        </tr>
                    </thead>
                    <tbody></tbody>
                </table>
            </div>
        </div>
    </div>
    <style>
        body {
            background: white;
            padding: 20px;
        }

        .card {
            margin-top: 20px;
            margin-left: 300px;
            width: 750px;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
        }

        #loader {
            display: none;
            text-align: center;
            font-weight: bold;
            color: #0d6efd;
            margin-bottom: 10px;
        }

        .chart-cell {
            cursor: pointer;
            color: #0d6efd;
        }

            .chart-cell:hover {
                background: #f2f2f2;
            }
    </style>
