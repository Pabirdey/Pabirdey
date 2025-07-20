<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Dashboard Layout</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <style>
        body {
            background-color: #f8f9fa;
        }

        .scroll-box {
            max-height: 400px;
            overflow-y: auto;
        }

        .card-header {
            background-color: #0d6efd;
            color: white;
        }

        .table th, .table td {
            vertical-align: middle;
            text-align: center;
        }

        /* Sync Scroll between two divs */
        .scroll-sync {
            overflow-y: scroll;
            height: 400px;
        }

        .scroll-sync::-webkit-scrollbar {
            width: 8px;
        }

        .scroll-sync::-webkit-scrollbar-thumb {
            background-color: rgba(0,0,0,0.1);
        }
    </style>
</head>
<body>
    <div class="container-fluid p-3">
        <!-- Header -->
        <div class="mb-4">
            <h2 class="text-center">Dashboard Layout</h2>
        </div>

        <!-- Side by side tables with shared scroll -->
        <div class="row">
            <!-- Left Panel -->
            <div class="col-md-6">
                <div class="card">
                    <div class="card-header">Panel A</div>
                    <div class="card-body p-0 scroll-sync" id="scrollLeft">
                        <table class="table table-bordered mb-0">
                            <thead class="table-light">
                                <tr>
                                    <th>#</th>
                                    <th>Item A1</th>
                                    <th>Item A2</th>
                                </tr>
                            </thead>
                            <tbody>
                                <!-- Sample rows -->
                                <tr><td>1</td><td>Data A1</td><td>Data A2</td></tr>
                                <tr><td>2</td><td>Data A1</td><td>Data A2</td></tr>
                                <tr><td>3</td><td>Data A1</td><td>Data A2</td></tr>
                                <!-- Add more rows as needed -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>

            <!-- Right Panel -->
            <div class="col-md-6">
                <div class="card">
                    <div class="card-header">Panel B</div>
                    <div class="card-body p-0 scroll-sync" id="scrollRight">
                        <table class="table table-bordered mb-0">
                            <thead class="table-light">
                                <tr>
                                    <th>#</th>
                                    <th>Item B1</th>
                                    <th>Item B2</th>
                                </tr>
                            </thead>
                            <tbody>
                                <!-- Sample rows -->
                                <tr><td>1</td><td>Data B1</td><td>Data B2</td></tr>
                                <tr><td>2</td><td>Data B1</td><td>Data B2</td></tr>
                                <tr><td>3</td><td>Data B1</td><td>Data B2</td></tr>
                                <!-- Add more rows as needed -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Scroll sync logic -->
    <script>
        const left = document.getElementById("scrollLeft");
        const right = document.getElementById("scrollRight");

        left.addEventListener("scroll", () => {
            right.scrollTop = left.scrollTop;
        });

        right.addEventListener("scroll", () => {
            left.scrollTop = right.scrollTop;
        });
    </script>
</body>
</html>