<script>

    function SaveBFProdData() {

        var modelList = [];

        // ================= C E F =================

        var furnaces1 = ["C", "E", "F"];

        for (var i = 0; i < furnaces1.length; i++) {

            var f = furnaces1[i];

            var model = {

                FURNACE: $("#FURNACE_" + f).val(),

                ACTUAL: Math.round(parseFloat($("#ACTUAL_" + f).val()) || 0),

                REPORTED: Math.round(parseFloat($("#REPORTED_" + f).val()) || 0),

                BALANCE: Math.round(parseFloat($("#BALANCE_" + f).val()) || 0),

                PROD_DATE: lsSelectedFDate
            };

            modelList.push(model);
        }


        // ================= G H I =================

        var furnaces2 = ["G", "H", "I"];

        for (var j = 0; j < furnaces2.length; j++) {

            var f = furnaces2[j];

            var model = {

                FURNACE: $("#TXT_FURNACE_" + f).val(),

                ACTUAL: Math.round(parseFloat($("#TXT_ACTUAL_" + f).val()) || 0),

                REPORTED: Math.round(parseFloat($("#TXT_RPT_" + f).val()) || 0),

                BALANCE: Math.round(parseFloat($("#TXT_BAL_" + f).val()) || 0),

                PROD_DATE: lsSelectedFDate
            };

            modelList.push(model);
        }

        console.log(modelList);


        // ================= FIRST SAVE =================

        $.ajax({

            url: '/HML/SaveBFProdData',

            type: 'POST',

            data: JSON.stringify(modelList),

            contentType: 'application/json; charset=utf-8',

            dataType: 'json',

            success: function (res) {

                if (res.success) {

                    // ================= SECOND SAVE =================

                    SaveDEMOBFProdData(modelList);

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



    // ================= SECOND FUNCTION =================

    function SaveDEMOBFProdData(modelList) {

        $.ajax({

            url: '/HML/SaveDEMOBFProdData',

            type: 'POST',

            data: JSON.stringify(modelList),

            contentType: 'application/json; charset=utf-8',

            dataType: 'json',

            success: function (res) {

                if (res.success) {

                    alert("Both Save Successfully");
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

</script>
