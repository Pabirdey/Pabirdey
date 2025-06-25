<div id="FugitiveModal" class="modal fade bs-example-modal-lg" tabindex="-1" role="dialog" aria-labelledby="myLargeModalLabel" aria-hidden="true" data-backdrop="static" data-focus="true">
    <div class="modal-dialog modal-dialog" style="width:98%;">
        <div class="modal-content">
            <div class="modal-header">
                <div class="panel margin-bottom-0">
                    <div class="panel-heading no-border">
                        <h5 class="over-title modal-title" id="myModalLabel"></h5>
                        <div class="container-fluid">
                            <div class="rows">
                                <div class="col-md-1">
                                    <div class="form-group">
                                        <a id="oven_condition" class="btn btn-primary" href="#">Oven Condition</a>
                                    </div>
                                </div>
                                <div class="col-md-2" style="margin-left:10px">
                                    <div class="form-group">
                                        <label>Change Oven: </label>
                                        <select class="modal_oven underline"></select>
                                    </div>
                                </div>
                                <div class="col-md-2" style="margin-left:10px">
                                    <div class="form-group">
                                        <label>Change Date: </label>
                                        <a class="modal-drpickr btn btn-o btn-primary">
                                            <i class="fa fa-calendar"></i> <label class="value"></label>
                                        </a>
                                    </div>
                                </div>                               
                            </div>
                        </div>
                       
                    </div>
                </div>
                <div id="modalPushCurrentChart1" class="full-width block" style="height:600px;float:left"></div>
                <br />              
            </div>
        </div>
    </div>
</div>


 $('#FugitiveModal').on('shown.bs.modal', function (e) {
                debugger;
                var modal = $('#FugitiveModal');
                var pOvenNo = $('#pOvenNo').val();
                var pDate = $('#pDate').val();
                var pBatteryNo = $('#pBatteryNo').val();
                var pPlantName = $('#pPlantName').val();
                modal.find('.modal_oven').val(pOvenNo);
                modal.find('.modal_oven').val(pBatteryNo);
                modal.find('.modal_oven').val(pPlantName);
                modal.find('.modal-drpickr .value').html(pDate);
                modal.find('.modal-drpickr').datepicker({
                    format: "dd/mm/yyyy",
                    autoclose: true,
                    todayHighlight: true
                });
                modal.find('.modal-drpickr').datepicker('update', pDate);
                modal.find('.modal-drpickr').on('changeDate', function () {
                    var getFormattedDate = modal.find('.modal-drpickr').datepicker('getFormattedDate');
                    modal.find('.modal-drpickr .value').html(getFormattedDate);
                    Get_Fugitive_Violin_Chart(pOvenNo, getFormattedDate);
                });
                Get_Fugitive_Violin_Chart(pOvenNo, pDate, pBatteryNo, pPlantName);
            });

             $('#FugitiveModal .modal_oven').change(function () {
                var pOvenNo = $(this).val();
                var pDate = $('#FugitiveModal .modal-drpickr').datepicker('getFormattedDate');
                Get_Fugitive_Violin_Chart(pOvenNo, pDate);
            });

            
        function Get_Fugitive_Violin_Chart(pOvenNo, pDate, pBatteryNo, pPlantName) {
    debugger;    
    $('#FugitiveModal').modal('show'); 
    $('.modal-title').text("Oven No " + pOvenNo);    
    Plotly.purge('modalPushCurrentChart1');    
    $.ajax({
        url: '@Url.Action("Get_Fugitive_Violin_Chart")', 
        type: 'POST',
        data: {
            pTimestamp: pDate,
            pOvenNo: pOvenNo,
            pBatteryNo: pBatteryNo,
            pPlantName: pPlantName
        },
        success: function (jData) {           

            var values = jData.map(item => item.PUSH_FORCE);
            var labels = jData.map(item => item.DATETIME);

            var dataPlot = [{
                type: 'violin',
                y: values,
                x: labels,
                box: { visible: true },
                line: { color: 'blue' },
                meanline: { visible: true },
                points: 'all',
                jitter: 0.5,
                scalemode: 'count',
                name: 'Push Force'
            }];

            var layout = {
                title: "Fugitive Violin Chart",
                yaxis: { zeroline: false, title: "Push Force" },
                xaxis: { title: "Date/Time", type: 'category' }, 
                margin: { t: 50 }
            };

            Plotly.newPlot('modalPushCurrentChart1', dataPlot, layout);
        }
        
    });
}
[HttpPost]
        public JsonResult Get_Fugitive_Violin_Chart(string pTimestamp, string pOvenNo, string pBatteryNo, string pPlantName)
        {
                            string sql = string.Empty;
                DataTable dt = new DataTable();
                Dictionary<string, object> param = new Dictionary<string, object>();

                if (pPlantName == "B10")
                {
                    if (pBatteryNo == "10")
                    {
                        sql = "SELECT O.ID_OVEN AS OVEN_NO, TRUNC(O.ST_TIME) AS DATETIME, ROUND(O.DURATION,2) AS PUSH_FORCE " +
                              "FROM imtg.t_cp_fugitive_emission O " +
                              "WHERE TRUNC(O.ST_TIME) > (TO_DATE(:pTimestamp, 'dd/mm/yyyy') - 30) " +
                              "AND TRUNC(O.ST_TIME) <= TO_DATE(:pTimestamp, 'dd/mm/yyyy') " +
                              "AND O.ID_BATTERY = :pBatteryNo AND ID_OVEN = :pOvenNo ORDER BY O.ST_TIME";
                    }
                    else if (pBatteryNo == "11")
                    {
                        sql = "SELECT O.ID_OVEN AS OVEN_NO, TRUNC(O.ST_TIME) AS DATETIME, ROUND(O.DURATION,2) AS PUSH_FORCE " +
                              "FROM imtg.t_cp_fugitive_emission O " +
                              "WHERE TRUNC(O.ST_TIME) > (TO_DATE(:pTimestamp, 'dd/mm/yyyy') - 30) " +
                              "AND TRUNC(O.ST_TIME) <= TO_DATE(:pTimestamp, 'dd/mm/yyyy') " +
                              "AND O.ID_BATTERY = :pBatteryNo AND ID_OVEN = :pOvenNo ORDER BY O.ST_TIME";
                    }
                }

                param.Add("pTimestamp", pTimestamp);
                param.Add("pOvenNo", pOvenNo);
                param.Add("pBatteryNo", pBatteryNo);

                dt = DAL.GetRecords(sql, param);
                return Json(dt, JsonRequestBehavior.AllowGet);
                        
            
        }
        
