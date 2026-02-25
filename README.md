<style>
        .datepicker-days thead th {
            color: #000 !important;
            background-color: #f8f9fa !important;
            font-weight: bold;
        }

        .datepicker {
            z-index: 1055 !important;
        }

        body {
            background-color: #f4f6f9;
        }

        .Main {
            background-color: #ffffff;
            padding: 20px;
            border-radius: 10px;
        }

        .Main-Heading {
            font-family: Allan, cursive;
            font-weight: bold;
            font-size: 6vh;
            text-align: center;
            padding: 20px;
            color: rgb(57,57,57);
            margin: 20px 0;
        }

        .Consumption {
            display: flex;
            gap: 10px;
            align-items: flex-start;
            flex-wrap: wrap;
            margin-top: 20px;
        }

        #materialTable {
            flex: 0 0 550px;
            max-width: 550px;
            background: white;
            font-family: Courier New !important;
        }

        #types {
            flex: 0 0 310px;
            max-width: 310px;
            background: white;
            border: 1px solid;
        }

        #materialTable th {
            background: #8d15aa;
            color: white;
            text-align: center;
        }

        #materialTable td {
            border: 1px solid #000;
            font-weight: bold;
        }

        #types th {
            background: #8d15aa;
            color: white;
            text-align: center;
        }

        #types .btn {
            min-width: 90px;
            font-weight: bold;
            font-family: Courier New;
        }

        .medium-textbox {
            width: 100px;
            text-align: right;
            font-weight: bold;
        }
       .modal-content {
    border-radius: 25px;
    border: none;
}

.modal-header {
    background: #0d6efd;
    color: #fff;
    border-radius: 25px 25px 0 0;
}

.btn-Modalsave {
    background: #198754;
    color: white;
    padding: 8px 30px;
    border-radius: 20px;
}

.btn-Modalexit {
    background: #dc3545;
    color: white;
    padding: 8px 30px;
    border-radius: 20px;
}


.custom-modal {
    margin-top: 10px !important;
    max-width: 55% !important;
}
#BinDetailsmodal .modal-body {
    max-height: 70vh; 
    overflow-y: auto;
}

#tblBinDetails thead th {
    position: sticky;
    top: 0;
    background-color: #fff; 
    z-index: 10;    
}
.table-container {
    max-height: 60vh;
    overflow: auto;          
}

    </style>
     <div class="modal fade" id="BinDetailsmodal" tabindex="-1" data-bs-backdrop="static" data-bs-keyboard="false">
        <div class="modal-dialog modal-xl custom-modal">
            <div class="modal-content">
                <div class="modal-header">
                    <h3 class="modal-title w-100 text-center" style="font-family:Allan,cursive;">Bin Details Master</h3>                                        
                </div>      
                <div class="d-flex align-items-center ms-3 mt-2">
                    <label for="ddlFurnaceModal" style="font-family:Allan,cursive; font-weight:bold; margin-right:10px;">
                        Furname :-
                    </label>
                    <select id="ddlFurnaceModal" class="form-select w-auto">
                        <option value="C">C</option>
                        <option value="E">E</option>
                        <option value="F">F</option>
                    </select>
                </div>      
                <div class="modal-body">
                    <div class="table-container">
                        <table id="tblBinDetails" class="table table-bordered" style="font-family:Courier New; font-weight:bold;">
                            <thead>
                                <tr>
                                    <th style="width:40px;">FUR NAME</th>
                                    <th style="width:40px;">iMONITOR TAG ID</th>
                                    <th style="width:70px;">iHISTORIAN TAG NAME</th>
                                    <th style="width:40px;">WEB COLUMN</th>
                                    <th style="width:40px;">TAG TYPE</th>
                                    <th style="width:40px;">REQUIRED</th>
                                </tr>
                            </thead>
                            <tbody></tbody>
                        </table>
                    </div>
                </div>
                <div class="modal-footer justify-content-center">
                    <button class="btn-Modalsave" onclick="btnSaveBinRequired()">Save</button>
                    <button class="btn-Modalexit" data-bs-dismiss="modal">Exit</button>
                </div>

            </div>
        </div>
    </div>
