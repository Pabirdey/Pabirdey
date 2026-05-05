<!DOCTYPE html>
<html>
<head>
    <title>Bunker Selection</title>

    <!-- Bootstrap -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">

    <style>
        body {
            background: #f5f7fa;
            padding: 20px;
        }
        .card {
            max-width: 600px;
            margin: auto;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
        }
    </style>
</head>

<body>

<div class="card">

    <h4 class="text-center mb-3">Bunker Selection Screen</h4>

    <!-- Dropdown -->
    <div class="mb-3">
        <label><b>Select Bunker:</b></label>
        <select id="bunker" class="form-control" onchange="handleBunkerChange()">
            <option value="">--Select--</option>
            <option value="ST COKE">ST COKE</option>
            <option value="H/S NC">H/S NC</option>
            <option value="WESTERN">WESTERN</option>
            <option value="MIDDLE">MIDDLE</option>
            <option value="EASTERN">EASTERN</option>
            <option value="NC BF KO">NC BF KO</option>
            <option value="B/H COKE">B/H COKE</option>
            <option value="PLS 25MM NC">PLS 25MM NC</option>
        </select>
    </div>

    <!-- ST COKE -->
    <table id="stcokeTable" class="table table-bordered mt-3" style="display:none;">
        <tr class="table-primary"><th>ST COKE</th></tr>
        <tr><td>ST Coke Row Data</td></tr>
    </table>

    <!-- H/S NC -->
    <table id="hsncTable" class="table table-bordered mt-3" style="display:none;">
        <tr class="table-warning"><th>H/S NC</th></tr>
        <tr><td>H/S NC Row Data</td></tr>
    </table>

    <!-- WESTERN -->
    <table id="westernTable" class="table table-bordered mt-3" style="display:none;">
        <tr class="table-success"><th>WESTERN</th></tr>
        <tr><td>Western Row Data</td></tr>
    </table>

    <!-- MIDDLE -->
    <table id="middleTable" class="table table-bordered mt-3" style="display:none;">
        <tr class="table-info"><th>MIDDLE</th></tr>
        <tr><td>Middle Row Data</td></tr>
    </table>

    <!-- EASTERN -->
    <table id="easternTable" class="table table-bordered mt-3" style="display:none;">
        <tr class="table-danger"><th>EASTERN</th></tr>
        <tr><td>Eastern Row Data</td></tr>
    </table>

    <!-- NC BF KO -->
    <table id="ncbfkoTable" class="table table-bordered mt-3" style="display:none;">
        <tr class="table-secondary"><th>NC BF KO</th></tr>
        <tr><td>NC BF KO Row Data</td></tr>
    </table>

    <!-- B/H COKE -->
    <table id="bhcokeTable" class="table table-bordered mt-3" style="display:none;">
        <tr class="table-dark text-white"><th>B/H COKE</th></tr>
        <tr><td>B/H Coke Row Data</td></tr>
    </table>

    <!-- PLS 25MM NC -->
    <table id="plsTable" class="table table-bordered mt-3" style="display:none;">
        <tr class="table-light"><th>PLS 25MM NC</th></tr>
        <tr><td>PLS 25MM NC Row Data</td></tr>
    </table>

</div>

<script>

function handleBunkerChange() {

    let value = document.getElementById("bunker").value;

    // Hide all tables
    let tables = document.querySelectorAll("table");
    tables.forEach(t => t.style.display = "none");

    // Show based on selection (Oracle logic style)
    if (value === "ST COKE") {
        document.getElementById("stcokeTable").style.display = "table";
    }
    else if (value === "H/S NC") {
        document.getElementById("hsncTable").style.display = "table";
    }
    else if (value === "WESTERN") {
        document.getElementById("westernTable").style.display = "table";
    }
    else if (value === "MIDDLE") {
        document.getElementById("middleTable").style.display = "table";
    }
    else if (value === "EASTERN") {
        document.getElementById("easternTable").style.display = "table";
    }
    else if (value === "NC BF KO") {
        document.getElementById("ncbfkoTable").style.display = "table";
    }
    else if (value === "B/H COKE") {
        document.getElementById("bhcokeTable").style.display = "table";
    }
    else if (value === "PLS 25MM NC") {
        document.getElementById("plsTable").style.display = "table";
    }
}

</script>

</body>
</html>
