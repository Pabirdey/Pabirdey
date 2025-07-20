<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Two Tables Shared Scroll</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">

    <style>
        .scroll-container {
            max-height: 300px; /* Set the height for vertical scroll */
            overflow-y: auto; /* Enable vertical scroll */
            display: flex;
            border: 1px solid #ccc;
        }

        .table-wrapper {
            flex: 1;
            min-width: 300px;
        }

        table {
            width: 100%;
            margin: 0;
        }

        th {
            position: sticky;
            top: 0;
            background-color: #f8f9fa;
        }

        td, th {
            text-align: center;
            vertical-align: middle;
        }
    </style>
</head>
<body>

<div class="container mt-4">
    <div class="scroll-container">
        <!-- Table 1 -->
        <div class="table-wrapper">
            <table class="table table-bordered">
                <thead>
                    <tr>
                        <th>Sr</th>
                        <th>Name</th>
                    </tr>
                </thead>
                <tbody>
                    <tr><td>1</td><td>John</td></tr>
                    <tr><td>2</td><td>Jane</td></tr>
                    <tr><td>3</td><td>Alex</td></tr>
                    <tr><td>4</td><td>Maria</td></tr>
                    <tr><td>5</td><td>Mike</td></tr>
                    <tr><td>6</td><td>Linda</td></tr>
                    <tr><td>7</td><td>Steve</td></tr>
                </tbody>
            </table>
        </div>

        <!-- Table 2 -->
        <div class="table-wrapper">
            <table class="table table-bordered">
                <thead>
                    <tr>
                        <th>ID</th>
                        <th>City</th>
                    </tr>
                </thead>
                <tbody>
                    <tr><td>101</td><td>New York</td></tr>
                    <tr><td>102</td><td>London</td></tr>
                    <tr><td>103</td><td>Tokyo</td></tr>
                    <tr><td>104</td><td>Sydney</td></tr>
                    <tr><td>105</td><td>Paris</td></tr>
                    <tr><td>106</td><td>Berlin</td></tr>
                    <tr><td>107</td><td>Mumbai</td></tr>
                </tbody>
            </table>
        </div>
    </div>
</div>

</body>
</html>