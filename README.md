<script>

    // ✅ DATE FORMAT
    function formatDate(dt) {
        if (!dt) return "";

        let d = new Date(dt);
        let day = ("0" + d.getDate()).slice(-2);
        let month = ("0" + (d.getMonth() + 1)).slice(-2);
        let year = d.getFullYear();

        return day + "/" + month + "/" + year;
    }

    // ✅ CREATE ROW
    function createRow(item = {}) {

        return `
        <tr>
            <td><input class="form-control row-date" value="${formatDate(item.TIMESTAMP)}" readonly></td>

            <td>
                <select class="form-control row-shift">
                    <option ${item.SHIFT == 'A' ? 'selected' : ''}>A</option>
                    <option ${item.SHIFT == 'B' ? 'selected' : ''}>B</option>
                    <option ${item.SHIFT == 'C' ? 'selected' : ''}>C</option>
                </select>
            </td>

            <td>
                <select class="form-control bunker">
                    <option ${item.BUNKER=='WESTERN'?'selected':''}>WESTERN</option>
                    <option ${item.BUNKER=='MIDDLE'?'selected':''}>MIDDLE</option>
                    <option ${item.BUNKER=='EASTERN'?'selected':''}>EASTERN</option>
                </select>
            </td>

            <td><input class="form-control c" value="${item.C || ''}"></td>
            <td><input class="form-control e" value="${item.E || ''}"></td>
            <td><input class="form-control f" value="${item.F || ''}"></td>

            <td><input class="form-control total" value="${item.TOTAL || ''}" readonly></td>
            <td><input class="form-control position" value="${item.BUNKER_POSITION || ''}"></td>
            <td><input class="form-control balance" value="${item.BALANCE || ''}"></td>
        </tr>`;
    }

    // ✅ LOAD DATA FROM ORACLE
    function Display_Coke_Unloading() {

        var date = $("#txtDate").val();
        var shift = $("#ddlshift").val();

        $.ajax({
            url: '/Furnace_High_line/Get_Coke_Unloading',
            type: 'GET',
            data: { date: date, shift: shift },

            success: function (res) {

                let tbody = $("#tblBody");
                tbody.empty();

                if (res.success) {

                    if (res.data.length > 0) {

                        res.data.forEach(function (item) {
                            tbody.append(createRow(item));
                        });

                    } else {
                        for (let i = 0; i < 8; i++) {
                            tbody.append(createRow());
                        }
                    }

                } else {
                    alert(res.message);
                }
            },
            error: function () {
                alert("Error loading data");
            }
        });
    }

    // ✅ AUTO TOTAL
    $(document).on("input", ".c, .e, .f", function () {

        let row = $(this).closest("tr");

        let c = parseFloat(row.find(".c").val()) || 0;
        let e = parseFloat(row.find(".e").val()) || 0;
        let f = parseFloat(row.find(".f").val()) || 0;

        row.find(".total").val(c + e + f);
    });

</script>
