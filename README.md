<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Side by Side Tables with Shared Scroll</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <style>
        .scroll-wrapper {
            max-height: 300px; /* scrollable height */
            overflow-y: auto;
            display: flex;
        }

        .table-container {
            min-width: 300px;
        }

        table {
            margin: 0;
        }

        th {
            position: sticky;
            top: 0;
            background: #f8f9fa;
        }

        td, th {
            text-align: center;
            vertical-align: middle;
        }
    </style>
</head>
<body>

<div class="container mt-4">
    <div class="scroll-wrapper border">
        <!-- First Table -->
        <div class="table-container">
            <table class="table table-bordered mb-0">
                <thead>
                    <tr>
                        <th>Item A1</th>
                        <th>Item A2</th>
                    </tr>
                </thead>
                <tbody>
                    <!-- Repeat rows as needed -->
                    <tr><td>1</td><td>One</td></tr>
                    <tr><td>2</td><td>Two</td></tr>
                    <tr><td>3</td><td>Three</td></tr>
                    <tr><td>4</td><td>Four</td></tr>
                    <tr><td>5</td><td>Five</td></tr>
                    <tr><td>6</td><td>Six</td></tr>
                </tbody>
            </table>
        </div>

        <!-- Second Table -->
        <div class="table-container">
            <table class="table table-bordered mb-0">
                <thead>
                    <tr>
                        <th>Item B1</th>
                        <th>Item B2</th>
                    </tr>
                </thead>
                <tbody>
                    <!-- Repeat rows as needed -->
                    <tr><td>A</td><td>Alpha</td></tr>
                    <tr><td>B</td><td>Beta</td></tr>
                    <tr><td>C</td><td>Gamma</td></tr>
                    <tr><td>D</td><td>Delta</td></tr>
                    <tr><td>E</td><td>Epsilon</td></tr>
                    <tr><td>F</td><td>Zeta</td></tr>
                </tbody>
            </table>
        </div>
    </div>
</div>

</body>
</html>