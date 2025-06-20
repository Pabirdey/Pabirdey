<!DOCTYPE html>
<html>
<head>
  <title>Copy Textbox Value</title>
</head>
<body>

<!-- First textbox (source) -->
<input type="text" id="source" placeholder="Enter something" oninput="copyValue()" />

<!-- Second textbox (destination) -->
<input type="text" id="destination" placeholder="Value copied here" />

<script>
function copyValue() {
  // Get value from source textbox
  var sourceValue = document.getElementById("source").value;

  // Set the value to destination textbox
  document.getElementById("destination").value = sourceValue;
}
</script>

</body>
</html>