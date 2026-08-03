  function BFProdProcedure() {
        var furnaces = ["C", "D", "E", "F"];
        var completed = 0;
        var message = "";

        furnaces.forEach(function (furnace) {
            $.ajax({
                url: '/BF_Production/BFProdProcedure',
                type: 'POST',
                data: {
                    p_date: lsSelectedFDate,
                    p_furnace: furnace
                },
                success: function (res) {

                    completed++;
                    message = res.message;

                    if (completed === furnaces.length) {
                        alert(message);  
                    }
                },
                error: function (xhr) {
                    alert("Calculation failed.");
                }
            });

        });
    }  function BFProdProcedure() {
        var furnaces = ["C", "D", "E", "F"];
        var completed = 0;
        var message = "";

        furnaces.forEach(function (furnace) {
            $.ajax({
                url: '/BF_Production/BFProdProcedure',
                type: 'POST',
                data: {
                    p_date: lsSelectedFDate,
                    p_furnace: furnace
                },
                success: function (res) {

                    completed++;
                    message = res.message;

                    if (completed === furnaces.length) {
                        alert(message);  
                    }
                },
                error: function (xhr) {
                    alert("Calculation failed.");
                }
            });

        });
    }
    DEMO.PROC_FURNACE_DELAY_ANALYSIS(:ctl_blk.CTL_DATE_TIME_PROD);  	
    Begin
				demo.proc_furnace_derailment(:ctl_blk.CTL_DATE_TIME_PROD);
			Exception
				when others then
				null;
			End;
			
