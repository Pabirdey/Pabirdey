<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Beautiful Table</title>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
  <style>
    body {
      background: linear-gradient(to right, #dbeafe, #f0f9ff);
      font-family: 'Segoe UI', sans-serif;
      padding: 30px;
    }

    .beautiful-table th {
      background: linear-gradient(to right, #6366f1, #60a5fa);
      color: white;
      text-align: center;
    }

    .beautiful-table td {
      background-color: #ffffff;
      text-align: center;
    }

    .beautiful-table tr:hover {
      background-color: #e0f2fe;
      transition: 0.3s;
    }

    .card {
      border-radius: 15px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.1);
    }
  </style>
</head>
<body>

  <div class="card p-4">
    <h4 class="mb-4 text-primary text-center">Employee Data</h4>
    <div class="table-responsive">
      <table class="table beautiful-table table-bordered table-striped">
        <thead>
          <tr>
            <th>#</th>
            <th>Name</th>
            <th>Department</th>
            <th>Status</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>1</td>
            <td>Ravi Kumar</td>
            <td>IT</td>
            <td><span class="badge bg-success">Active</span></td>
          </tr>
          <tr>
            <td>2</td>
            <td>Priya Singh</td>
            <td>HR</td>
            <td><span class="badge bg-warning text-dark">Pending</span></td>
          </tr>
          <tr>
            <td>3</td>
            <td>Amit Verma</td>
            <td>Finance</td>
            <td><span class="badge bg-danger">Blocked</span></td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>

</body>
</html>