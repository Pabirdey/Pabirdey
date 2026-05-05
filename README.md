public class SaveModel
{
    public List<MainData> main { get; set; }
    public List<TonnageData> coke { get; set; }
    public List<TonnageData> nut { get; set; }
}
public class MainData
{
    public string Date { get; set; }      // dd/MM/yyyy
    public string Shift { get; set; }
    public string Bunker { get; set; }

    public string C { get; set; }
    public string E { get; set; }
    public string F { get; set; }

    public string Total { get; set; }

    public string Position { get; set; }
    public string Balance { get; set; }
}
public class TonnageData
{
    public string Bunker { get; set; }

    public string C { get; set; }
    public string E { get; set; }
    public string F { get; set; }

    public string Total { get; set; }
}
function saveData() {

    var mainList = [];
    var cokeList = [];
    var nutList = [];

    // 🔷 MAIN TABLE (Coke Unloading)
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

    // 🔷 TONNAGE OF COKE
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

    // 🔷 TONNAGE OF NUT COKE
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

    // 🔥 AJAX CALL
    $.ajax({
        url: '/YourController/SaveData',
        type: 'POST',
        data: JSON.stringify({
            main: mainList,
            coke: cokeList,
            nut: nutList
        }),
        contentType: 'application/json',
        success: function () {
            alert("Data Saved Successfully");
        },
        error: function () {
            alert("Error Saving Data");
        }
    });
}