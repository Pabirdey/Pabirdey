<style>
        body {
            font-family: Arial, sans-serif;
        }

        .Main-Heading {
            text-align: center;
            font-size: 40px;
            margin: 20px 0;
        }

        .form-section {
            padding: 15px;
            border: 1px solid #ccc;
            border-radius: 10px;
            margin-bottom: 20px;
        }

        .section-title {
            font-weight: bold;
            background: #EEB86D;
            padding: 5px 10px;
            border-radius: 5px;
            margin-bottom: 10px;
        }

        .table th, .table td {
            text-align: center;
            vertical-align: middle;
        }

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
    </style>
