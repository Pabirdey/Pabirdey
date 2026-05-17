   <script>
        $(".reported").each(function () {
            debugger;
            let id = $(this).attr("id");
            debugger;
            originalValues[id] = Number($(this).val()) || 0;
        });
        $("#REPORTED_C").on("blur", function () {
            debugger;
            let id = $(this).attr("id");

            let current = Number($(this).val()) || 0;

            let old = originalValues[id];

            let diff = current - old;

            let baseTD = Number($("#REPORTED_C_TD").val()) || 0;

            let baseBal = Number($("#BALANCE_C").val()) || 0;

            $("#REPORTED_C_TD").val(baseTD + diff);
            $("#BALANCE_C").val(baseBal - diff);

            // update stored value for next edit
            originalValues[id] = current;
        });
    </script>
