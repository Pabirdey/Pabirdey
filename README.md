<!DOCTYPE html>
<html>
<head>
    <title>Datalist Open on Click</title>
    <style>
        body{
            font-family: Arial;
            padding: 40px;
        }

        input{
            width:250px;
            padding:8px;
            font-size:16px;
        }
    </style>
</head>

<body>

<h2>Datalist Open On Click Example</h2>

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

// When user clicks input → dropdown opens
const input = document.getElementById("clayInput");

input.addEventListener("click", function () {

    // Chrome / Edge / New browsers
    if (this.showPicker) {
        this.showPicker();
        return;
    }

    // Fallback for old browsers
    this.blur();      // remove focus
    this.focus();     // re-focus to trigger list
});

// Also open when user focuses with TAB key
input.addEventListener("focus", function () {
    if (this.showPicker) this.showPicker();
});

</script>

</body>
</html>