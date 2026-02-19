  <div class="modal fade" id="bindetailsmodal" tabindex="-1">
        <div class="modal-dialog modal-md modal-dialog-centered">
            <div class="modal-content">
                <!-- HEADER -->
                <div class="modal-header">
                    <h5 class="modal-title w-100 text-center" style="font-family:Allan,cursive;">Bin Details Master</h5>
                    <button type="button" class="btn-close btn-close-white" data-bs-dismiss="modal"></button>
                </div>
                <!-- BODY -->
                <div class="modal-body">                    
                    <div>
                        <table id="tblBinDetails" style="font-family:Courier New, Courier, monospace;font-weight:bold;">
                            <thead style="font-family:Courier New, Courier, monospace;">
                                <tr stypeof="border:1px solid;">
                                    <th>iMONITOR TAG ID</th>
                                    <th>iHISTORIAN TAG NAME</th>
                                    <th>WEB COLUMN</th>
                                    <th>TAG TYPE</th>
                                    <th>REQUIRED</th>
                                </tr>
                            </thead>
                            <tbody></tbody>
                        </table>
                    </div>
                    
                </div>
                <!-- FOOTER -->
                <div class="modal-footer justify-content-center">
                    <button class="btn-Modalsave" onclick="checkClay()">Save</button>
                    <button class="btn-Modalexit" data-bs-dismiss="modal">Exit</button>
                </div>
            </div>
        </div>
    </div>

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
