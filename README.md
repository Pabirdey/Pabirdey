<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0"/>

    <!-- Bootstrap -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet"/>

    <title>Datalist Design</title>

    <style>

        body{
            background:#f2f2f2;
            padding:40px;
        }

        .blue-box{
            background:#0066ff;
            border-radius:35px;
            padding:25px 35px;
            display:flex;
            align-items:center;
            justify-content:space-between;
            max-width:1200px;
            margin:auto;
            box-shadow:0 4px 10px rgba(0,0,0,0.2);
        }

        .left-section{
            width:65%;
        }

        .custom-input{
            height:55px;
            border:3px solid #999;
            border-radius:4px;
            font-size:22px;
            font-family:Arial;
            font-weight:bold;
        }

        .custom-input:focus{
            box-shadow:none;
            border-color:#333;
        }

        .right-section{
            display:flex;
            align-items:center;
            gap:12px;
            color:white;
            font-size:38px;
            font-weight:500;
            font-family:Arial;
        }

        .form-check-input{
            width:28px;
            height:28px;
            cursor:pointer;
        }

        @media(max-width:768px){

            .blue-box{
                flex-direction:column;
                gap:20px;
            }

            .left-section{
                width:100%;
            }

            .right-section{
                font-size:24px;
            }
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

        // Get selected value
        document.getElementById("material").addEventListener("change", function () {

            let value = this.value;

            console.log("Selected :", value);

            // Example
            if(value === "AL203"){
                alert("AL203 Selected");
            }

        });

    </script>

</body>
</html>