<div class="blue-box">

    <!-- Datalist -->
    <div class="left-section">

        <input type="text"
               class="form-control custom-input"
               list="materialList"
               id="material"
               placeholder="Select Users">

        <datalist id="materialList">
        </datalist>

    </div>

    <!-- Checkbox -->
    <div class="right-section">

        <input class="form-check-input"
               type="checkbox"
               id="signoff">

        <label for="signoff">
            Sign OFF
        </label>

    </div>

</div>

<script>

    $(document).ready(function () {

        loadUsers();

    });

    // Load Oracle Data
    function loadUsers() {

        $.ajax({

            url: '/Home/GetUsers',
            type: 'GET',

            success: function (data) {

                var dl = document.getElementById("materialList");

                // Clear old option
                dl.innerHTML = "";

                // Using length function
                for (var i = 0; i < data.length; i++) {

                    var option = document.createElement("option");

                    option.value = data[i].USER_NAME;

                    dl.appendChild(option);

                }

            },

            error: function () {

                alert("Data Load Error");

            }

        });

    }

</script>
