<script>
    let urlBF = '@urlBF';
    var bf = '@ViewBag.bf';

    if (bf !== "") {

        switch (bf) {

            case 'BFCTRL':
                alert("Login From BFCTRL");

                $(".reported_G").prop("readonly", true);
                $(".reported_H").prop("readonly", true);
                $(".reported_I").prop("readonly", true);
                break;

            case 'GBFCTRL':
                alert("Login From GBFCTRL");

                $(".reported_B").prop("readonly", true);
                $(".reported_H").prop("readonly", true);
                $(".reported_I").prop("readonly", true);
                break;

            case 'HBFCTRL':
                alert("Login From HBFCTRL");

                $(".reported_B").prop("readonly", true);
                $(".reported_G").prop("readonly", true);
                $(".reported_I").prop("readonly", true);
                break;

            case 'IBFCTRL':
                alert("Login From IBFCTRL");

                $(".reported_B").prop("readonly", true);
                $(".reported_G").prop("readonly", true);
                $(".reported_H").prop("readonly", true);
                break;

            default:
                console.log("No Match Found");
                break;
        }
    }
</script>
