var SelectUser=$("#txtUser").val();
        var Signoff=$("#signoff").val();
        if((SelectUser=="" || SelectUser==null) && (Signoff=="" || Signoff==null)){
            alert("Please Select User Name & Check Signoff");
            $("#txtUser").focus();
            return;
        }
