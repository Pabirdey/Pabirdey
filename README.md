function saveData() {
    let furnace = document.getElementById("txtFurnace").value;
    let selectedDate = document.getElementById("txtDate").value;

    if (!furnace || !selectedDate) {
        alert("Please enter Furnace and Date");
        return;
    }

    let rows = [];
    let tableRows = document.querySelectorAll("#tblData tbody tr");

    tableRows.forEach(function(row) {
        rows.push({
            furnace: furnace,
            tagid: row.querySelector(".tagid").textContent.trim(),
            material: row.querySelector(".material").textContent.trim(),
            date: selectedDate,
            valueTon: row.querySelector(".ton").value,
            valueKg: row.querySelector(".kg").value
        });
    });

    // सभी पंक्तियों को एक साथ भेजना
    fetch("/Home/SaveRawMaterialBatch", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(rows)
    })
    .then(response => response.json())
    .then(data => {
        if (data.success) {
            alert("Data saved successfully!");
        } else {
            alert("Error: " + data.message);
        }
    })
    .catch(error => {
        console.error("Error:", error);
        alert("Error sending data");
    });
}