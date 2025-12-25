<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Raw Material Entry</title>

<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">

<style>
body{
    background:#1e8f3b;
    background:linear-gradient(135deg,#1e8f3b,#0d5e27);
    min-height:100vh;
}

.form-container{
    background:#2e9d44;
    border-radius:15px;
    padding:25px;
    color:white;
    box-shadow:0 0 15px rgba(0,0,0,.4);
}

.section-box{
    background:#3daf4f;
    padding:20px;
    border-radius:10px;
}

table input, select{
    background:#fff8c7 !important;
    border-radius:5px;
}

.label-col{
    color:#fff;
    font-weight:600;
}

.title-text{
    font-size:18px;
    font-weight:700;
}
</style>
</head>

<body>

<div class="container py-4">
    <div class="form-container">

        <!-- Header -->
        <div class="row mb-4">
            <div class="col-md-6">
                <label class="fw-bold">Date:</label>
                <input type="date" class="form-control d-inline-block w-50">
            </div>

            <div class="col-md-6">
                <label class="fw-bold">Furnace:</label>
                <select class="form-select w-25 d-inline-block">
                    <option>F</option>
                    <option>E</option>
                    <option>D</option>
                </select>
            </div>
        </div>

        <!-- Body Box -->
        <div class="section-box">
            <div class="row text-center mb-2">
                <div class="col-md-4 title-text">Materials</div>
                <div class="col-md-4 title-text">Value in Tons</div>
                <div class="col-md-4 title-text">Value in Kgs / Types</div>
            </div>

            <table class="table table-borderless text-white">
                <tbody>

                    <!-- ROW -->
                    <tr>
                        <td class="label-col">COAL</td>
                        <td><input class="form-control" placeholder="Tons"></td>
                        <td class="d-flex gap-2">
                            <input class="form-control" placeholder="Kgs">
                            <select class="form-select">
                                <option>IPC</option>
                                <option>Other</option>
                            </select>
                        </td>
                    </tr>

                    <tr>
                        <td class="label-col">NUT COKE</td>
                        <td><input class="form-control"></td>
                        <td class="d-flex gap-2">
                            <input class="form-control">
                            <select class="form-select">
                                <option>BF Sized</option>
                            </select>
                        </td>
                    </tr>

                    <tr>
                        <td class="label-col">SINTER</td>
                        <td><input class="form-control"></td>
                        <td><input class="form-control"></td>
                    </tr>

                    <tr>
                        <td class="label-col">COKE</td>
                        <td><input class="form-control"></td>
                        <td><input class="form-control"></td>
                    </tr>

                    <tr>
                        <td class="label-col">PELLET</td>
                        <td><input class="form-control"></td>
                        <td><input class="form-control"></td>
                    </tr>

                </tbody>
            </table>

            <!-- Theoretical Production -->
            <div class="mt-3">
                <label class="fw-bold">Theoretical Production</label>
                <input class="form-control w-25" value="4307.16">
            </div>

            <!-- Buttons -->
            <div class="mt-4">
                <button class="btn btn-primary px-4">Save</button>
                <button class="btn btn-dark px-4">Back</button>
            </div>

        </div>
    </div>
</div>

</body>
</html>