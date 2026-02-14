@section css {
    <link rel="stylesheet" href="@Url.Content("~/bower_components/bootstrap/dist/css/bootstrap.min.css")">
    <link rel="stylesheet" href="@Url.Content("~/bower_components/bootstrap-datepicker/dist/css/bootstrap-datepicker3.standalone.min.css")">

    <style>
        body {
            background-color: #eef2f7;
        }

        .Main {
            background-color: #ffffff;
            padding: 25px;
            border-radius: 12px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.08);
        }

        .page-title {
            font-weight: 700;
            color: #1f2d3d;
            letter-spacing: 1px;
        }

        fieldset {
            border: 1px solid #dcdcdc;
            padding: 15px;
            border-radius: 8px;
            background: #fafafa;
        }

        legend {
            font-size: 14px;
            font-weight: 600;
            padding: 0 10px;
        }

        /* FLEX LAYOUT */
        .Consumption {
            display: flex;
            gap: 25px;
            margin-top: 25px;
        }

        /* LEFT TABLE */
        #materialTableContainer {
            flex: 2;
            min-width: 550px;
            max-height: 400px;
            overflow-y: auto;
            border-radius: 8px;
        }

        #materialTable {
            width: 100%;
        }

        /* RIGHT TABLE */
        #types {
            flex: 1;
            min-width: 280px;
        }

        /* HEADER STICKY */
        #materialTable thead th {
            position: sticky;
            top: 0;
            background: linear-gradient(90deg, #1f4e79, #2c3e50);
            color: white;
            text-align: center;
            z-index: 2;
        }

        #types th {
            background: linear-gradient(90deg, #34495e, #2c3e50);
            color: white;
            text-align: center;
        }

        #materialTable td {
            font-family: Courier New, monospace;
            font-weight: bold;
            font-size: 14px;
        }

        .medium-textbox {
            width: 110px;
            text-align: right;
            font-weight: bold;
        }

        .btn-custom {
            padding: 10px 40px;
            font-size: 15px;
            border-radius: 8px;
        }

        #materialTable tbody tr:hover {
            background-color: #f1f7ff;
        }

        /* LOADER */
        #loader {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(255,255,255,0.7);
            z-index: 9999;
            text-align: center;
            padding-top: 300px;
            font-size: 20px;
            font-weight: bold;
        }

        /* RESPONSIVE */
        @media (max-width: 992px) {
            .Consumption {
                flex-direction: column;
            }

            #materialTableContainer,
            #types {
                width: 100%;
                min-width: 100%;
            }
        }
    </style>
}
