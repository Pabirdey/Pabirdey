@{
    ViewBag.Title = "Fugitive Emission Violin Chart";
    Layout = null; // or set your actual layout
}

<!-- Include Plotly JS -->
<script src="https://cdn.plot.ly/plotly-latest.min.js"></script>
<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>

<!-- Example Inputs -->
<label>Battery No:</label>
<select id="battery_no">
    <option value="10">10</option>
    <option value="11">11</option>
</select>

<label>Oven No:</label>
<input type="text" id="oven_no" />

<label>Date:</label>
<input type="text" id="date" placeholder="dd/mm/yyyy" />

<!-- Hidden or dropdown for Area -->
<input type="hidden" id="plant_area" value="B10" />

<button onclick="Get_Fugitive_Violin_Chart()">Show Violin Chart</button>

<!-- Modal -->
<div class="modal" tabindex="-1" role="dialog" id="FugitiveModal">
    <div class="modal-dialog" style="max-width: 900px;" role="document">
        <div class="modal-content">
            <div class="modal-header">
                <h5 class="modal-title">Fugitive Violin Chart</h5>
                <button type="button" class="close" data-dismiss="modal" onclick="$('#FugitiveModal').hide()">×</button>
            </div>
            <div class="modal-body">
                <div id="modalPushCurrentChart1" style="width: 100%; height: 500px;"></div>
            </div>
        </div>
    </div>
</div>

<!-- Main JavaScript -->
<script type="text/javascript">
    function Get_Fugitive_Violin_Chart() {
        var pOvenNo = $('#oven_no').val();
        var pDate = $('#date').val();
        var pBatteryNo = $('#battery_no').val();
        var Area = $('#plant_area').val(); // Make sure this is defined

        if (!pOvenNo || !pDate) {
            alert("Please enter oven number and date.");
            return;
        }

        $('#FugitiveModal').show();
        $('.modal-title').text("Oven No " + pOvenNo);
        Plotly.purge('modalPushCurrentChart1');

        $.post('@Url.Action("Get_Fugitive_Violin_Chart")', {
            'pTimestamp': pDate,
            'pOvenNo': pOvenNo,
            'pBatteryNo': pBatteryNo,
            'pPlantName': Area
        }, function (jData) {
            if (!jData || jData.length === 0 || jData.success === false) {
                alert("No data or error: " + (jData.message || "Unknown error"));
                return;
            }

            var values = jData.map(item => item.PUSH_FORCE);
            var labels = jData.map(item => item.DATETIME);

            var dataPlot = [{
                type: 'violin',
                y: values,
                x: labels,
                box: { visible: true },
                line: { color: 'blue' },
                meanline: { visible: true }
            }];

            var layout = {
                title: "Fugitive Violin Chart",
                yaxis: { zeroline: false, title: "Push Force" },
                xaxis: { title: "Date" }
            };

            Plotly.newPlot('modalPushCurrentChart1', dataPlot, layout);
        }).fail(function (xhr, status, error) {
            alert("Error occurred: " + xhr.responseText);
        });
    }
</script>

<!-- Optional Bootstrap (if you're using Bootstrap modal) -->
<link href="https://cdn.jsdelivr.net/npm/bootstrap@4.6.2/dist/css/bootstrap.min.css" rel="stylesheet" />
<script src="https://cdn.jsdelivr.net/npm/bootstrap@4.6.2/dist/js/bootstrap.bundle.min.js"></script>