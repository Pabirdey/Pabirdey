<script>
function loadUsers() {
 $.ajax({
     url: '/Furnace_High_line/GetUsers',
     type: 'GET',
        success: function (data) {
        var dl = document.getElementById("UserList"); 
        dl.innerHTML = ""; 
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
function signoff() {
    var obj = {
        NAME: $("#txtUser").val(),
        SO_DATE: $("#currDate-value").val(),
        SO_SHIFT: $("#ddlshift").val(),
        SO_CHECK: $("#signoff").is(":checked") ? 1 : 0
    };

    $.ajax({
        url: '/Furnace_High_line/SaveSignOff',
        type: 'POST',
        data: obj,
        success: function (res) {                       
            if (obj.SO_CHECK == 1) {
                $("#CokeUnloading").prop("disabled", true);                
            }
            else {
                $("#CokeUnloading").prop("disabled", false);                
            }
        },

        error: function () {
            alert("Error");
        }
    });
}
</script>
 <input type="text" class="form-control custom-input" list="UserList" id="txtUser" placeholder="Select Users">
                                        <datalist id="UserList">                                           
                                        </datalist>
