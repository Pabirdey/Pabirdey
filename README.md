<div class="main-content">
    <div class="container">
        <div class="card">

            <h3 class="text-center">📊 Pile Material Quality Data</h3>

            <div id="loader">Loading...</div>

            <table class="table text-center" id="finesTable">
                <thead>
                    <tr>
                        <th>Element</th>
                        <th>🔁 Return Fines</th>
                        <th>💧 Wet Fines</th>
                        <th>🔥 Dry Fines</th>
                        <th>⚙ Dry Fines 500TPH</th>
                    </tr>
                </thead>
                <tbody></tbody>
            </table>

        </div>
    </div>
</div>

body {
    background: #f5f7fa;
    padding: 20px;
    font-family: 'Segoe UI', sans-serif;
}

/* Card */
.card {
    margin: 20px auto;
    width: 850px;
    padding: 20px;
    border-radius: 15px;
    border: none;
    box-shadow: 0 10px 25px rgba(0,0,0,0.08);
    background: #fff;
}

/* Title */
.card h3 {
    font-weight: 600;
    color: #333;
    margin-bottom: 15px;
}

/* Table */
#finesTable {
    width: 100%;
    border-collapse: separate;
    border-spacing: 0;
    overflow: hidden;
    border-radius: 10px;
}

/* Header */
#finesTable thead {
    background: linear-gradient(45deg, #007bff, #00c6ff);
    color: white;
}

#finesTable th {
    padding: 12px;
    font-size: 14px;
    letter-spacing: 0.5px;
}

/* Body */
#finesTable td {
    padding: 10px;
    font-size: 14px;
}

/* Zebra rows */
#finesTable tbody tr:nth-child(even) {
    background: #f9fbfd;
}

/* Hover effect */
#finesTable tbody tr:hover {
    background: #eaf4ff;
    transform: scale(1.01);
    transition: 0.2s;
}

/* Clickable cells */
.chart-cell {
    cursor: pointer;
    color: #0d6efd;
    font-weight: 500;
}

.chart-cell:hover {
    color: #0a58ca;
    text-decoration: underline;
}

/* Loader */
#loader {
    display: none;
    text-align: center;
    font-weight: bold;
    color: #0d6efd;
    margin-bottom: 10px;
}
