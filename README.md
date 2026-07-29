 $.ajax({
                url: '/BF_Production/SaveBFProdData',
                type: 'POST',
                data: JSON.stringify(modelList),
                contentType: 'application/json; charset=utf-8',
                success: function (res) {
                    if (res.success) {
                        SaveDEMOBFProdData(modelList);
                    } else {
                        alert(res.message);
                    }
                },
                error: function () {
                    alert("Server Error");
                }
            });
             function SaveDEMOBFProdData(modelList) {
        $.ajax({
            url: '/BF_Production/SaveDEMOBFProdData',
            type: 'POST',
            data: JSON.stringify(modelList),
            contentType: 'application/json; charset=utf-8',
            dataType: 'json',
            success: function (res) {
                if (res.success) {
                    //alert("BF Prod Save Data Successfully");
                    Save_A_FBF_LadleData(modelList);                    
                }
                else {
                    alert(res.message);
                }
            },

            error: function (xhr) {
                alert("Server Error");
                console.log(xhr.responseText);
            }
        });
    }
    function Save_GBF_LadleData(modelList) {
        $.ajax({
            url: '/BF_Production/Save_GBF_LadleData',
            type: 'POST',
            data: JSON.stringify(modelList),
            contentType: 'application/json; charset=utf-8',
            dataType: 'json',
            success: function (res) {
                if (res.success) {
                    alert("BF Prod Save Data Successfully");
                }
                else {
                    alert(res.message);
                }
            },

            error: function (xhr) {
                alert("Server Error");
                console.log(xhr.responseText);
            }
        });
    }
    function Save_A_FBF_LadleData(modelList) {
        $.ajax({
            url: '/BF_Production/Save_A_F_BF_LadleData',
            type: 'POST',
            data: JSON.stringify(modelList),
            contentType: 'application/json; charset=utf-8',
            dataType: 'json',
            success: function (res) {
                if (res.success) {
                    //alert("BF Prod Save Data Successfully");
                    Save_GBF_LadleData(modelList);
                }
                else {
                    alert(res.message);
                }
            },

            error: function (xhr) {
                alert("Server Error");
                console.log(xhr.responseText);
            }
        });
    }
