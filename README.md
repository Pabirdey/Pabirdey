 success: function (res) {

            $("#loaderDiv").hide();

            alert(res.message);
        },

        error: function (xhr) {

            $("#loaderDiv").hide();

            alert("Error : " + xhr.responseText);
        }
    });
}
