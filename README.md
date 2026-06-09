 <td>
                    <select class ="table-input arrivedFrom">
                        <option value=""></option>
                        <option value="C" ${item.ARRIVED_FROM === 'C' ? 'selected': ''}>C</option>
                        <option value="E" ${item.ARRIVED_FROM === 'E' ? 'selected': ''}>E</option>
                        <option value="F" ${item.ARRIVED_FROM === 'F' ? 'selected': ''}>F</option>
                        <option value="C" ${item.ARRIVED_FROM === 'G' ? 'selected': ''}>G</option>
                        <option value="E" ${item.ARRIVED_FROM === 'H' ? 'selected': ''}>H</option>
                        <option value="F" ${item.ARRIVED_FROM === 'I' ? 'selected': ''}>I</option>
                    </select>
               </td>
                 $(document).on("change", ".arrivedFrom", function () {
        var row = $(this).closest("tr");
        var arrivedFrom = $(this).val();               
        debugger;
        $.ajax({
            url: '/Granshot/CalculateLadle',
            type: 'POST',
            data: {
                txtdate: $("#hiddenDate").val(),
                ddlshift: $("#ddlshift").val(),
                TRP_NO: row.find("td:eq(3) input").val(),
                LADLE_FLST_TIME: row.find("td:eq(4) input").val(),
                LADLE_FLEND_TIME: row.find("td:eq(5) input").val(),
                ARRIVED_FROM: arrivedFrom
            },
            success: function (response) {
                if (response.success) {
                    row.find("td:eq(7) input").val(response.data.GROSS_WT);
                    row.find("td:eq(8) input").val(response.data.TARE_WT);
                    row.find("td:eq(9) input").val(response.data.NET_WT);
                    row.find("td:eq(10) input").val(response.data.POURING_RATE);
                    row.find("td:eq(11) input").val(response.data.HMT);
                }
                else {
                    alert(response.message);
                }
            },
            error: function () {
                alert("Error occurred");
            }
        });

    });
