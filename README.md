<!DOCTYPE html>
<html>
<head>
<title>Datalist Change Item Anytime</title>

<style>
input{
    width:250px;
    padding:6px;
    font-size:16px;
}
</style>

</head>
<body>

<h3>Click input anytime to open list & change value</h3>

<input list="MG_CLAY_USED" id="clayInput" placeholder="Select or Type">

<datalist id="MG_CLAY_USED">
  <option value="LRH">
  <option value="UBQ">
  <option value="SARVESH">
  <option value="HARIMA(S)">
  <option value="HARIMA(D)">
  <option value="CORUS">
</datalist>

<script>
const input = document.getElementById("clayInput");

input.addEventListener("click", function () {

    // Save current value
    const currentValue = this.value;

    // Chrome / Edge support
    if (this.showPicker) {
        this.showPicker();
    }
    else {
        // Old browser trick
        this.blur();
        this.focus();
    }

    // Restore value (so it does not clear)
    this.value = currentValue;
});

// Also open when focus by TAB
input.addEventListener("focus", function () {
    if (this.showPicker) this.showPicker();
});
</script>

</body>
</html>