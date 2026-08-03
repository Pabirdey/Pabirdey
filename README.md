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
    }
