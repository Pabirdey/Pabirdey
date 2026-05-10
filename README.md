function loadUsers() {

        $.ajax({

            url: '/Furnace_High_line/GetUsers',

            type: 'GET',

            success: function (data) {

                console.log(data);

                var dl =
                    document.getElementById("UserList");

                dl.innerHTML = "";

                for (var i = 0; i < data.length; i++) {

                    var option =
                        document.createElement("option");

                    option.value =
                        data[i].USER_NAME;

                    dl.appendChild(option);

                }

            },

            error: function (xhr) {

                console.log(xhr);

                alert("Data Load Error");

            }

        });

    }
<input type="text"
       class="form-control custom-input"
       list="UserList"
       id="txtUser"
       placeholder="Select Users">

<datalist id="UserList">
</datalist>
