@{
    ViewBag.Title = "Cast House Details";
    Layout = null;
}

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Cast House Details</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap-datepicker@1.10.0/dist/css/bootstrap-datepicker.min.css" rel="stylesheet">
    <style>
        body { font-family: Arial, sans-serif; }
        .Main-Heading { text-align: center; font-size: 40px; margin: 20px 0; }
        .form-section { padding: 15px; border: 1px solid #ccc; border-radius: 10px; margin-bottom: 20px; }
        .section-title { font-weight: bold; background: #EEB86D; padding: 5px 10px; border-radius: 5px; margin-bottom: 10px; }
        .table th, .table td { text-align: center; vertical-align: middle; }
        .input-wrapper { position: relative; display: flex; }
        .arrow-btn { position: absolute; right: 5px; top: 6px; cursor: pointer; background: #f0f0f0; padding: 0 5px; }
        .list-box { display: none; position: absolute; background: white; border: 1px solid #ccc; width: 100%; max-height: 150px; overflow-y: auto; z-index: 9999; }
        .list-box div { padding: 5px; cursor: pointer; }
        .list-box div:hover { background: #eee; }
    </style>
</head>
<body>

<div class="container">
    <div class="Main-Heading">Cast House Details</div>

    <div class="mb-3">
        <label for="tbFDatePick" class="form-label">Date:</label>
        <input type="text" id="tbFDatePick" class="form-control d-inline-block" style="width:150px;">
        <label for="lstFur" class="form-label ms-3">Furnace:</label>
        <select id="lstFur" class="form-select d-inline-block" style="width:100px;">
            <option value="C">C</option>
            <option value="E">E</option>
            <option value="F">F</option>
            <option value="G">G</option>
            <option value="H">H</option>
            <option value="I">I</option>
        </select>
    </div>

    <!-- Mudgun Details -->
    <div class="form-section">
        <div class="section-title">Mudgun Details</div>
        <div class="table-responsive">
            <table class="table table-bordered table-sm" id="Mudgun_Details">
                <thead>
                    <tr>
                        <th>Cast No</th>
                        <th>Closure Mode</th>
                        <th>Clay Qty</th>
                        <th>MG Clay Type</th>
                        <th>Lot No</th>
                        <th>No. of Bags</th>
                    </tr>
                </thead>
                <tbody></tbody>
            </table>
        </div>
    </div>
</div>

<!-- Modal for Other MG Clay -->
<div class="modal fade" id="mgClayOtherModal" tabindex="-1">
  <div class="modal-dialog modal-dialog-centered">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title">Other MG Clay Type</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
      </div>
      <div class="modal-body">
        <input type="hidden" id="hdnRowIndex">
        <input type="text" id="txtOtherMGClay" class="form-control" placeholder="Enter MG Clay Type">
      </div>
      <div class="modal-footer">
        <button class="btn btn-secondary" data-bs-dismiss="modal">Cancel</button>
        <button class="btn btn-primary" onclick="saveOtherMGClay()">Save</button>
      </div>
    </div>
  </div>
</div>

<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/bootstrap-datepicker@1.10.0/dist/js/bootstrap-datepicker.min.js"></script>

<script>
let lsSelectedFDate;
let IsSelectedFur;

$(document).ready(function() {
    // Initialize datepicker with today's date
    let today = new Date();
    lsSelectedFDate = ("0" + today.getDate()).slice(-2) + "/" + ("0"+(today.getMonth()+1)).slice(-2) + "/" + today.getFullYear();

    $('#tbFDatePick').datepicker({
        format: "dd/mm/yyyy",
        autoclose: true,
        todayHighlight: true
    }).val(lsSelectedFDate);

    IsSelectedFur = $('#lstFur').val();
    Display_Mudgun_Details(lsSelectedFDate, IsSelectedFur);

    $('#lstFur').change(function(){
        IsSelectedFur = $(this).val();
        Display_Mudgun_Details(lsSelectedFDate, IsSelectedFur);
    });

    $('#tbFDatePick').on('changeDate', function(){
        lsSelectedFDate = $(this).val();
        Display_Mudgun_Details(lsSelectedFDate, IsSelectedFur);
    });
});

// AJAX call to controller
function Display_Mudgun_Details(date, furnace){
    $.ajax({
        url: '@Url.Action("Get_Display_Mudgun_Details","CastHouse")',
        type: 'GET',
        data: { Fdate: date, Fur: furnace },
        success: function(result){
            let parsedData = JSON.parse(result);
            let tableBody = "";
            for(let i=0;i<parsedData.length;i++){
                tableBody += "<tr>";
                tableBody += `<td>${parsedData[i].CAST_NO}</td>`;
                tableBody += `<td>
                                <select class="form-select form-select-sm">
                                    <option value="" ${parsedData[i].CLOSURE_MODE==""?'selected':''}></option>
                                    <option value="MUDGUN" ${parsedData[i].CLOSURE_MODE=="MUDGUN"?'selected':''}>MUDGUN</option>
                                    <option value="NULL" ${parsedData[i].CLOSURE_MODE=="NULL"?'selected':''}>NULL</option>
                                </select>
                              </td>`;
                tableBody += `<td><input class="form-control form-control-sm" value="${parsedData[i].CLAY_QUANTITY}"></td>`;
                tableBody += `<td>
                                <div class="input-wrapper">
                                    <input type="text" class="form-control form-control-sm" id="clayInput_${i}" value="${parsedData[i].MG_CLAY}" readonly>
                                    <div class="arrow-btn" onclick="toggleList(${i})">▼</div>
                                    <div class="list-box" id="list_${i}">
                                        <div onclick="selectItem(this, ${i})">ACE</div>
                                        <div onclick="selectItem(this, ${i})">BRL</div>
                                        <div onclick="selectItem(this, ${i})">LRH</div>
                                        <div onclick="selectItem(this, ${i})">UBQ</div>
                                        <div onclick="selectItem(this, ${i})">OTHERS</div>
                                    </div>
                                </div>
                              </td>`;
                tableBody += `<td>${parsedData[i].LOT_NO}</td>`;
                tableBody += `<td>${parsedData[i].NO_OF_BAGS}</td>`;
                tableBody += "</tr>";
            }
            $('#Mudgun_Details tbody').html(tableBody);
        }
    });
}

// Dropdown list functions
function toggleList(i){
    $(".list-box").hide();
    $("#list_"+i).toggle();
}
function selectItem(el, i){
    let val = el.innerText.trim();
    if(val === "OTHERS"){
        $("#hdnRowIndex").val(i);
        $("#txtOtherMGClay").val('');
        let modalEl = document.getElementById("mgClayOtherModal");
        let modal = new bootstrap.Modal(modalEl);
        modal.show();
        return;
    }
    $("#clayInput_"+i).val(val);
    $("#list_"+i).hide();
}
function saveOtherMGClay(){
    let i = $("#hdnRowIndex").val();
    let val = $("#txtOtherMGClay").val().trim();
    if(!val){ alert("Enter value"); return; }
    $("#clayInput_"+i).val(val);
    let modalEl = document.getElementById("mgClayOtherModal");
    let modal = bootstrap.Modal.getInstance(modalEl);
    if(modal) modal.hide();
}
</script>

</body>
</html>
