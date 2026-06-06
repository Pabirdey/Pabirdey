$.ajax({
    url: '/Granshot/Get_Granshot_Details',
    type: 'GET',
    data: {
        pdate: pdate,
        pshift: shift
    },
    success: function (result) {

        console.log("Success");
        console.log(result);

        BindTable(result);
    },
    error: function (xhr, status, error) {

        console.log("Error");
        console.log(xhr.responseText);
        console.log(error);
    }
});
