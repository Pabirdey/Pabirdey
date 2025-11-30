<script>
$(document).ready(function () {

    // When furnace dropdown changes
    $("select").change(function () {

        var furnace = $(this).val();
        loadMaterials(furnace);

    });

    // Load default furnace (first dropdown value)
    loadMaterials($("select").val());
});


// Function to load materials based on furnace
function loadMaterials(furnaceName) {

    $.ajax({
        url: '/Home/GetMaterialsByFurnace',
        type: 'GET',
        data: { furnace: furnaceName },
        success: function (data) {

            var tbody = $("#materialTable tbody");
            tbody.empty(); // Clear previous rows

            for (var i = 0; i < data.length; i++) {

                var row = "<tr>" +
                    "<td>" + data[i] + "</td>" +
                    "<td><input type='text' class='form-control medium-textbox' id='ton_" + i + "'></td>" +
                    "<td><input type='text' class='form-control medium-textbox' id='kg_" + i + "'></td>" +
                    "</tr>";

                tbody.append(row);
            }
        }
    });
}
</script>
