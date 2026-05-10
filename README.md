 onkeyup="calculateTotal(this)">

 function calculateTotal(ele) {

        var row = ele.closest("tr");

        var c =
            parseFloat(
                row.querySelector(".c").value
            ) || 0;

        var e =
            parseFloat(
                row.querySelector(".e").value
            ) || 0;

        var f =
            parseFloat(
                row.querySelector(".f").value
            ) || 0;

        var total = c + e + f;

        row.querySelector(".total").value =
            total.toFixed(2);

    }
