 var nutRows = document.querySelectorAll("#nutTable tbody tr");
        for (var k = 0; k < nutRows.length; k++) {
            var row = nutRows[k];
            var obj = {
                Date: row.querySelector(".row-date").value,
                Bunker: row.cells[0].innerText,
                C: row.querySelector(".c").value,
                E: row.querySelector(".e").value,
                F: row.querySelector(".f").value,
                Total: row.querySelector(".total").value
            };

            nutList.push(obj);
        }
