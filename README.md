<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <!-- Bootstrap -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet"/>

    <title>Small Datalist Design</title>

    <style>

        body{
            background:#f2f2f2;
            padding:25px;
        }

        /* Small Box */
        .blue-box{
            background:#0066ff;
            border-radius:14px;
            padding:10px 15px;
            display:flex;
            align-items:center;
            justify-content:space-between;
            width:430px;
            margin:auto;
            box-shadow:0 3px 8px rgba(0,0,0,0.2);
        }

        .left-section{
            width:58%;
        }

        /* Small Input */
        .custom-input{
            height:34px;
            border:2px solid #999;
            border-radius:5px;
            font-size:13px;
            font-family:Arial;
            font-weight:bold;
            padding-left:10px;
        }

        .custom-input:focus{
            box-shadow:none;
            border-color:#222;
        }

        /* Small Right Section */
        .right-section{
            display:flex;
            align-items:center;
            gap:7px;
            color:white;
            font-size:15px;
            font-weight:600;
            font-family:Arial;
        }

        /* Small Checkbox */
        .form-check-input{
            width:17px;
            height:17px;
            cursor:pointer;
            margin-top:0;
        }

    </style>
</head>

<body>

    <div class="blue-box">

        <!-- Datalist Input -->
        <div class="left-section">

            <input type="text"
                   class="form-control custom-input"
                   list="materialList"
                   id="material"
                   placeholder="Select Material">

            <datalist id="materialList">
                <option value="AL203">
                <option value="SIO2">
                <option value="MGO">
                <option value="CAO">
                <option value="FE">
                <option value="RETURN FINES">
                <option value="LAM COKE">
            </datalist>

        </div>

        <!-- Checkbox -->
        <div class="right-section">

            <input class="form-check-input"
                   type="checkbox"
                   id="signoff">

            <label for="signoff">
                Sign OFF
            </label>

        </div>

    </div>

    <script>

        document.getElementById("material")
        .addEventListener("change", function () {

            let value = this.value;

            console.log("Selected :", value);

            if(value === "AL203"){
                alert("AL203 Selected");
            }

        });

    </script>

</body>
</html>
