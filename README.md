<script>
    $(document).ready(function () {
        loadFinesData();
    });

    function loadFinesData() {

        $('#loader').show();   // ✅ FIX

        $.ajax({
            url: '/Home/GetFinesData',
            type: 'GET',
            dataType: 'json',
            success: function (res) {

                // ✅ Handle if API returns error object
                if (res.error) {
                    $('#finesTable tbody').html(
                        "<tr><td colspan='5' class='text-danger'>" + res.error + "</td></tr>"
                    );
                } else {
                    renderTable(res);
                    showRowCount(res);   // ✅ Added again
                }

                $('#loader').hide();
            },
            error: function () {
                $('#loader').hide();
                $('#finesTable tbody').html(
                    "<tr><td colspan='5' class='text-danger'>Error loading data</td></tr>"
                );
            }
        });
    }

    function renderTable(data) {
        var html = '';

        if (!data || data.length === 0) {
            html = "<tr><td colspan='5'>No data found</td></tr>";
        } else {
            $.each(data, function (i, item) {
                html += '<tr>';

                html += '<td>' + (item.ELEMENT ?? '-') + '</td>';
                html += '<td>' + (item.RETURN_FINES ?? '-') + '</td>';
                html += '<td>' + (item.WET_FINES ?? '-') + '</td>';
                html += '<td>' + (item.DRY_FINES ?? '-') + '</td>';
                html += '<td>' + (item.DRY_FINES_500TPH ?? '-') + '</td>';

                html += '</tr>';
            });
        }

        $('#finesTable tbody').html(html);
    }

    function showRowCount(data) {
        var count = (data && data.length) ? data.length : 0;
        $('#rowCount').text("Total Rows: " + count);
    }
</script>
