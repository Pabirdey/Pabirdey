<!DOCTYPE html>
<html>
<body>

<input type="text"
       list="itemList"
       oninput="selectItem(this,0)"
       placeholder="Select item">

<datalist id="itemList">
    <option value="CLAY">
    <option value="SAND">
    <option value="OTHERS">
</datalist>

<script>
function selectItem(ctrl, index) {
    if (ctrl.value === "OTHERS") {
        alert("Show extra textbox");
    }
    console.log("Value:", ctrl.value, "Index:", index);
}
</script>

</body>
</html>