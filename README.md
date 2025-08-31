<div class="col-md-2" id="pswBlock3">
    <label class="form-label">Blend-I</label>
    <select id="PSW_BL1" name="PSW_BL1" onchange="CheckPSW1()" class="form-control">
        <option value="">Select</option>
        <option value="1">1</option>
        <option value="2">2</option>
        <!-- Add other values -->
    </select>
</div>

<div class="col-md-2" id="pswBlock1">
    <label class="form-label">PSW1</label>
    <input class="form-control" type="text" value="@Model.PSW1" name="PSW1" id="PSW1" onblur="SolidWasteSum()" autocomplete="off">
</div>

<script>
function CheckPSW1() {
    var psw1Value = document.getElementById("PSW1").value.trim();
    var dropdown = document.getElementById("PSW_BL1");

    if (psw1Value === "") {
        alert("PSW1 is blank. Please enter a value.");
        dropdown.value = ""; // Reset dropdown to default
    }
}
</script>
