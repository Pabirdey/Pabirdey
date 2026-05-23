 function SaveCokeUnloading() {

        $("#loaderDiv").show();
        var mainList = [];
        var cokeList = [];
        var nutList = [];    
        var mainRows = document.querySelectorAll("#tblBody tr");
        for (var i = 0; i < mainRows.length; i++) {
            var row = mainRows[i];
            var obj = {
                Date: row.querySelector(".row-date").value,
                Shift: row.querySelector(".row-shift").value,
                Bunker: row.querySelector(".bunker").value,

                C: row.querySelector(".c").value,
                E: row.querySelector(".e").value,
                F: row.querySelector(".f").value,

                Total: row.querySelector(".total").value,
                Position: row.querySelector(".position").value,
                Balance: row.querySelector(".balance").value
            };

            mainList.push(obj);
        }    
        var cokeRows = document.querySelectorAll("#cokeTable tbody tr");
        for (var j = 0; j < cokeRows.length; j++) {
            var row = cokeRows[j];
            var obj = {
                Bunker: row.cells[0].innerText,
                C: row.querySelector(".c").value,
                E: row.querySelector(".e").value,
                F: row.querySelector(".f").value,
                Total: row.querySelector(".total").value
            };

            cokeList.push(obj);
        }

        var nutRows = document.querySelectorAll("#nutTable tbody tr");
        for (var k = 0; k < nutRows.length; k++) {
            var row = nutRows[k];
            var obj = {
                Bunker: row.cells[0].innerText,
                C: row.querySelector(".c").value,
                E: row.querySelector(".e").value,
                F: row.querySelector(".f").value,
                Total: row.querySelector(".total").value
            };

            nutList.push(obj);
        }

        console.log("MAIN:", mainList);
        console.log("COKE:", cokeList);
        console.log("NUT:", nutList); 
        $.ajax({
            url: '/Furnace_High_line/SaveFurnaceCokeUnloading',
            type: 'POST',
            data: JSON.stringify({
                main: mainList,
                coke: cokeList,
                nut: nutList
            }),
            contentType: 'application/json',
            success: function (res) {
                //$("#loaderDiv").hide();
                //alert(res.message);
                SaveFurnaceCokeUnloading_ID();
            },

            error: function (xhr) {
                $("#loaderDiv").hide();
                alert("Error : " + xhr.responseText);
            }
        });
    }
