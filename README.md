 function Get_CP_Fugitivity_Voilin_Chart(pOvenNo, pDate) {
            debugger;
            var modal = $('#FugitiveModal');
            modal.modal('show');
            modal.find('.modal-title').text("Oven No " + pOvenNo);
            var pBatteryNo = $('#battery_no').val();
            var pPlantName = $('#Area').val();
            Plotly.purge('modalPushCurrentChart1');
            $.post('@Url.Action("Get_cp_fugitive_Voilin_Chart")', {
                pTimestamp: pDate,
                pOvenNo: pOvenNo,
                pBatteryNo: pBatteryNo,
                pPlantName: Area
            })
           .done(function (data) {
               if (typeof data === "string") {
                   try {
                       data = JSON.parse(data);
                   } catch (e) {
                       alert("Data parse error: " + e.message);
                       console.error(data);
                       return;
                   }
              }

       let pushForces = data.map(row => parseFloat(row.PUSH_FORCE));

       let trace = {
           type: 'violin',
           y: pushForces,
           box: { visible: true },
           line: { color: 'orange' },
           meanline: { visible: true },
           name: 'Fugitive',
       };

       let layout = {
           title: 'Violin Chart - Fugitive',
           yaxis: { title: 'Fugitive' }
       };

       Plotly.newPlot('modalPushCurrentChart1', [trace], layout);
   })
   .fail(function (xhr, status, error) {
       alert("AJAX Error: " + error);
       console.error(xhr.responseText);
   });
        }
