<style>
        .table-input {
            font-size: 1rem;
            padding: 2px 4px;
            border: 2px solid;
        }

        .my-swal-popup {
            font-family: 'Arial', sans-serif;
        }

        .my-swal-title {
            font-family: 'Georgia', serif;
            font-size: 22px;
        }

        .my-swal-text {
            font-family: 'Verdana', sans-serif;
            font-size: 18px;
        }

        .form-section {
            background: #ffffff;
            padding: 20px;
            border-radius: 20px;
            box-shadow: 0 10px 20px rgba(0,0,0,0.1);
            margin-bottom: 25px;
            overflow: visible;
            font-family: Courier New, Courier, monospace;
        }

        .section-title {
            background: #EEB86D;
            color: black;
            padding: 5px 10px;
            margin-bottom: 10px;
            font-weight: bold;
            border-radius: 10px;
            text-align: left;
            font-family: Courier New, Courier, monospace;
            font-size: 18px;
        }

        .form-control-lg {
            font-size: 1.5rem;
            font-family: Courier New, Courier, monospace;
            color: black;
        }

        th {
            font-family: Courier New, Courier, monospace;
            font-size: 14px;
            font-weight: bold;
            border: 1px solid;
            color: white;
        }

        .scrollable-table {
            overflow-y: auto;
        }

        .table thead th {
            position: sticky;
            top: 0;
            z-index: 2;
            border: 5px solid;
        }

        .Long_Heading_Medium {
            min-width: 100px;
            border: 1px solid black;
        }

        .Heading_Tiny {
            width: 20px;
            white-space: nowrap;
        }

        .Long_Heading {
            min-width: 130px;
        }

        .section_Exception-title {
            background: #EEB86D;
            color: black;
            padding: 5px 10px;
            margin-bottom: 10px;
            font-weight: bold;
            border-radius: 10px;
            text-align: left;
            font-family: Courier New, Courier, monospace;
            font-size: 15px;
            width: 15vh;
        }

        .Heading_Small {
            width: 10px;
            white-space: nowrap;
        }

        .section-Drill-title {
            background: #EEB86D;
            color: black;
            padding: 5px 10px;
            margin-bottom: 10px;
            font-weight: bold;
            border-radius: 4px;
            text-align: left;
            font-family: Courier New, Courier, monospace;
            font-size: 20px;
        }

        .form-group {
            border-radius: 25px;
            border: 4px solid #73AD21;
            padding: 10px;
            margin: 10px;
            width: 500px;
        }

        #Driling_Slag_Details tr.highlight td {
            background-color: yellow !important;
        }

        #TAP_Hot_Metal_Details tr.highlight td {
            background-color: yellow !important;
        }

        #Mudgun_Details tr.highlight td {
            background-color: yellow !important;
        }

        #Other_Details tr.highlight td {
            background-color: yellow !important;
        }

        .btnSaveCastHouse {
            background: linear-gradient(to bottom right, #EF4765, #FF9A5A);
            border: 0;
            border-radius: 10px;
            color: #FFFFFF;
            cursor: pointer;
            display: inline-block;
            font-family: Courier New, Courier, monospace;
            font-size: 15px;
            font-weight: bold;
            line-height: 2.5;
            outline: transparent;
            padding: 0 1rem;
            text-align: center;
            text-decoration: none;
            transition: box-shadow .2s ease-in-out;
            user-select: none;
            -webkit-user-select: none;
            touch-action: manipulation;
            white-space: nowrap;
            width: 12vh;
            margin-left: 30px;
            margin-top: 100px;
        }

            .btnSaveCastHouse:not([disabled]):focus {
                box-shadow: 0 0 .25rem rgba(0, 0, 0, 0.5), -.125rem -.125rem 1rem rgba(239, 71, 101, 0.5), .125rem .125rem 1rem rgba(255, 154, 90, 0.5);
            }

            .btnSaveCastHouse:not([disabled]):hover {
                box-shadow: 0 0 .25rem rgba(0, 0, 0, 0.5), -.125rem -.125rem 1rem rgba(239, 71, 101, 0.5), .125rem .125rem 1rem rgba(255, 154, 90, 0.5);
            }

        .btnHMLogistics {
            margin: 10px;
            padding: 15px 30px;
            text-align: center;
            text-transform: uppercase;
            transition: 0.5s;
            background-size: 200% auto;
            color: white;
            border-radius: 10px;
            display: block;
            border: 0px;
            font-weight: bold;
            box-shadow: 0px 0px 14px -7px #f09819;
            background-image: linear-gradient(45deg, #FF512F 0%, #F09819 51%, #FF512F 100%);
            cursor: pointer;
            user-select: none;
            -webkit-user-select: none;
            touch-action: manipulation;
        }

            .btnHMLogistics:hover {
                background-position: right center;
                color: #fff;
                text-decoration: none;
            }

            .btnHMLogistics:active {
                transform: scale(0.95);
            }

        select {
            appearance: auto !important;
            -webkit-a ppearance: auto !important;
            -moz-appearance: auto !important;
        }


        .Main-Heading {
            font-family: Allan,cursive;
            font-weight: bold;
            font-size: 6vh;
            text-align: center;
            padding: 20px;
            color: rgb(57,57,57);
            text-shadow: rgba(13, 0, 77, 0.08) 0px 2px 4px, rgba(13, 0, 77, 0.08) 0px 3px 6px, rgba(13, 0, 77, 0.08) 0px 8px 16px;
            border-radius: 10px;
        }

        #backgrcol_Tap_hole {
            color: white;
            font-weight: bold;
            padding: 8px;
        }

        fieldset {
            border: 2px solid #ccc !important;
            padding: 10px 12px 12px 12px;
        }

        legend {
            font-size: 24px;
            font-weight: 800;
            padding: 0 8px;
        }

        .input-wrapper {
            display: flex;
            border: 1px solid #999;
        }

            .input-wrapper input {
                border: none;
                outline: none;
            }

        .arrow-btn {
            width: 30px;
            text-align: center;
            cursor: pointer;
            background: #f0f0f0;
        }

        .list-box {
            border: 1px solid #999;
            display: none;
            background: #fff;
            position: absolute;
            z-index: 999;
        }

            .list-box div {
                padding: 5px;
                cursor: pointer;
            }

                .list-box div:hover {
                    background: #e6e6e6;
                }
                .input-wrapper {
    position: relative;
}

.arrow-btn {
    position: absolute;
    right: 5px;
    top: 6px;
    cursor: pointer;
    user-select: none;
}

.list-box {
    display: none;
    position: absolute;
    background: white;
    border: 1px solid #ccc;
    width: 100%;
    max-height: 200px;
    overflow-y: auto;
    z-index: 9999;
}

.list-box div {
    padding: 6px;
    cursor: pointer;
}

.list-box div:hover {
    background: #f0f0f0;
}
    </style>
      <style>
        /* ===== Headings ===== */
        .Main-Heading {
            font-family: Allan, cursive;
            font-weight: bold;
            font-size: 6vh;
            text-align: center;
            padding: 20px;
            color: rgb(57,57,57);
            text-shadow: rgba(13, 0, 77, 0.08) 0px 2px 4px, rgba(13, 0, 77, 0.08) 0px 3px 6px, rgba(13, 0, 77, 0.08) 0px 8px 16px;
            border-radius: 10px;
            margin: 20px 0;
        }

        /* ===== Sections ===== */
        .form-section {
            background: #ffffff;
            padding: 20px;
            border-radius: 20px;
            box-shadow: 0 10px 20px rgba(0,0,0,0.1);
            margin-bottom: 25px;
            overflow: visible;
            border: 1px solid #ccc;
            font-family: Courier New, Courier, monospace;
        }

        .section-title,
        .section_Exception-title,
        .section-Drill-title {
            background: #EEB86D;
            color: black;
            padding: 5px 10px;
            font-weight: bold;
            border-radius: 10px;
            margin-bottom: 10px;
            font-family: Courier New, Courier, monospace;
        }

        .section-title {
            font-size: 18px;
        }

        .section_Exception-title {
            font-size: 15px;
            width: 15vh;
        }

        .section-Drill-title {
            font-size: 20px;
            border-radius: 4px;
        }

        /* ===== Forms ===== */
        .form-control-lg {
            font-size: 1.5rem;
            font-family: Courier New, Courier, monospace;
            color: black;
        }

        .form-group {
            border-radius: 25px;
            border: 4px solid #73AD21;
            padding: 10px;
            margin: 10px;
            width: 500px;
        }

        /* ===== Tables ===== */
        th {
            font-family: Courier New, Courier, monospace;
            font-size: 14px;
            font-weight: bold;
            border: 1px solid;
            color: white;
        }

        .table th,
        .table td {
            text-align: center;
            vertical-align: middle;
        }

        .scrollable-table {
            overflow-y: auto;
        }

        .table thead th {
            position: sticky;
            top: 0;
            z-index: 2;
            border: 1px solid;
        }

        /* ===== Column Widths ===== */
        .Long_Heading {
            min-width: 130px;
        }

        .Long_Heading_Medium {
            min-width: 100px;
        }

        .Heading_Tiny {
            width: 20px;
            white-space: nowrap;
        }

        .Heading_Small {
            width: 10px;
            white-space: nowrap;
        }

        /* ===== Inputs ===== */
        .table-input {
            font-size: 1rem;
            padding: 2px 4px;
            border: 2px solid;
        }

        .highlight {
            background-color: #ffe08a !important;
        }

        /* ===== Buttons ===== */
        .btnSaveCastHouse {
            background: linear-gradient(to bottom right, #EF4765, #FF9A5A);
            border: 0;
            border-radius: 10px;
            color: #FFFFFF;
            cursor: pointer;
            font-family: Courier New, Courier, monospace;
            font-size: 15px;
            font-weight: bold;
            line-height: 2.5;
            padding: 0 1rem;
            width: 12vh;
            margin-left: 30px;
            margin-top: 100px;
            transition: box-shadow .2s ease-in-out;
        }

            .btnSaveCastHouse:hover,
            .btnSaveCastHouse:focus {
                box-shadow: 0 0 .25rem rgba(0,0,0,.5), -.125rem -.125rem 1rem rgba(239,71,101,.5), .125rem .125rem 1rem rgba(255,154,90,.5);
            }

        .btnHMLogistics {
            margin: 10px;
            padding: 15px 30px;
            font-weight: bold;
            color: white;
            border-radius: 10px;
            border: 0;
            background-image: linear-gradient(45deg, #FF512F 0%, #F09819 51%, #FF512F 100%);
            background-size: 200% auto;
            cursor: pointer;
            transition: 0.5s;
            box-shadow: 0px 0px 14px -7px #f09819;
        }

            .btnHMLogistics:hover {
                background-position: right center;
            }

            .btnHMLogistics:active {
                transform: scale(0.95);
            }

        /* ===== SweetAlert ===== */
        .my-swal-popup {
            font-family: Arial, sans-serif;
        }

        .my-swal-title {
            font-family: Georgia, serif;
            font-size: 22px;
        }

        .my-swal-text {
            font-family: Verdana, sans-serif;
            font-size: 18px;
        }

        /* ===== Mudgun Clay Dropdown ===== */
        .mgClayWrapper {
            position: relative;
            display: flex;
            align-items: center;
        }

            .mgClayWrapper .mgClayInput {
                width: 100%;
            }

            .mgClayWrapper button {
                margin-left: 5px;
            }

        .mgClayList {
            display: none;
            position: absolute;
            background: white;
            border: 1px solid #ccc;
            z-index: 1000;
            top: 30px;
            left: 0;
            width: 150px;
            max-height: 150px;
            overflow-y: auto;
        }

            .mgClayList div {
                padding: 5px;
                cursor: pointer;
            }

                .mgClayList div:hover {
                    background: #eee;
                }

        /* ===== Misc ===== */
        #backgrcol_Tap_hole {
            color: white;
            font-weight: bold;
            padding: 8px;
        }
         fieldset {
            border: 2px solid #ccc !important;
            padding: 10px 12px 12px 12px;
        }

        legend {
            font-size: 24px;
            font-weight: 800;
            padding: 0 8px;
        }

    </style>
