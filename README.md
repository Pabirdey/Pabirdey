<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Cast House Details</title>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
  <style>
    .section-title {
      background: #d1e7dd;
      padding: 5px;
      font-weight: bold;
      border: 1px solid #bcd0c7;
      margin-bottom: 10px;
    }
    .table-bordered td, .table-bordered th {
      vertical-align: middle;
      font-size: 13px;
      padding: 4px;
    }
    .highlight-yellow { background-color: #ffffcc; }
    .highlight-blue { background-color: #e7f3fe; }
  </style>
</head>
<body class="p-4">

  <div class="container-fluid">
    <h4 class="text-center mb-4">Cast House Details</h4>

    <!-- Date and Shift Inputs -->
    <div class="row mb-3">
      <div class="col-md-2">
        <label class="form-label fw-bold">Date</label>
        <input type="date" class="form-control">
      </div>
      <div class="col-md-2">
        <label class="form-label fw-bold">Furnace</label>
        <select class="form-select">
          <option>MVL</option>
          <option>FUR_NAME</option>
        </select>
      </div>
      <div class="col-md-2">
        <label class="form-label fw-bold">Shift</label>
        <select class="form-select">
          <option>SHIFT</option>
        </select>
      </div>
    </div>

    <!-- Cast Hole Details Section -->
    <div class="section-title">Cast Hole Details</div>
    <div class="table-responsive mb-4">
      <table class="table table-bordered">
        <thead class="table-light">
          <tr>
            <th>Cast</th>
            <th>Trough Cleaned</th>
            <th>Clay Condition</th>
            <th>Cast Duration</th>
            <th>Cast Speed</th>
            <th>Ready Time</th>
            <th>Tap Hole Behavior</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td class="highlight-yellow">CAST-1</td>
            <td class="highlight-blue">YES</td>
            <td>GOOD</td>
            <td>12 MIN</td>
            <td>MEDIUM</td>
            <td>08:00</td>
            <td>TAPHOLE OK</td>
          </tr>
          <tr>
            <td class="highlight-yellow">CAST-2</td>
            <td class="highlight-blue">NO</td>
            <td>AVERAGE</td>
            <td>10 MIN</td>
            <td>SLOW</td>
            <td>08:30</td>
            <td>TAPHOLE LOW</td>
          </tr>
        </tbody>
      </table>
    </div>

    <!-- Hot Metal Details Section -->
    <div class="section-title">Hot Metal Details</div>
    <div class="table-responsive mb-4">
      <table class="table table-bordered">
        <thead class="table-light">
          <tr>
            <th>HMT Before Slag</th>
            <th>HMT After Slag</th>
            <th>Final Weight</th>
            <th>HM Weight</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>BEFORE</td>
            <td>AFTER</td>
            <td>IS</td>
            <td class="highlight-blue">HM_WEIGHT</td>
          </tr>
          <tr>
            <td>BEFORE</td>
            <td>AFTER</td>
            <td>IS</td>
            <td class="highlight-blue">HM_WEIGHT</td>
          </tr>
        </tbody>
      </table>
    </div>

    <!-- Slag Details Section -->
    <div class="section-title">Slag Details</div>
    <div class="table-responsive">
      <table class="table table-bordered">
        <thead class="table-light">
          <tr>
            <th>Slag Start</th>
            <th>Slag Time</th>
            <th>Retention Time</th>
            <th>No of Slag Ladle</th>
            <th>No of Cinder Granulation</th>
            <th>Granulation Preference</th>
            <th>Slag Total</th>
            <th>Slag Rate</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>START</td>
            <td>F_TIME</td>
            <td>RETENT</td>
            <td>AG_LADLE</td>
            <td>GRANULATOR</td>
            <td>HIGH</td>
            <td>SLAG_TOTAL</td>
            <td>SLAG_RATE</td>
          </tr>
          <tr>
            <td>START</td>
            <td>F_TIME</td>
            <td>RETENT</td>
            <td>AG_LADLE</td>
            <td>GRANULATOR</td>
            <td>HIGH</td>
            <td>SLAG_TOTAL</td>
            <td>SLAG_RATE</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>

</body>
</html>