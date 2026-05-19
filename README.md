<script>
    function Dis_CBF_TO_IBF_LDActualData(lsSelectedFDate) {

        $.ajax({
            url: '/HML/GetCbfToIbfActalTodate',
            type: 'GET',
            data: { prodDate: lsSelectedFDate },

            success: function (response) {

                if (response.status) {

                    var data = response.data;

                    $("#TXT_CTOG_LD1_TONS").val(Math.round(data.CTOG_LD1_TONS || 0));
                    $("#TXT_CTOG_LD2_TONS").val(Math.round(data.CTOG_LD2_TONS || 0));
                    $("#TXT_CTOG_LD3_TONS").val(Math.round(data.CTOG_LD3_TONS || 0));
                    $("#TXT_CTOG_MRDTP_TONS").val(Math.round(data.CTOG_MRDTP_TONS || 0));

                    $("#TXT_CTOH_LD1_TONS").val(Math.round(data.CTOH_LD1_TONS || 0));
                    $("#TXT_CTOH_LD2_TONS").val(Math.round(data.CTOH_LD2_TONS || 0));
                    $("#TXT_CTOH_LD3_TONS").val(Math.round(data.CTOH_LD3_TONS || 0));
                    $("#TXT_CTOH_MRDTP_TONS").val(Math.round(data.CTOH_MRDTP_TONS || 0));

                    $("#TXT_CTOI_LD1_TONS").val(Math.round(data.CTOI_LD1_TONS || 0));
                    $("#TXT_CTOI_LD2_TONS").val(Math.round(data.CTOI_LD2_TONS || 0));
                    $("#TXT_CTOI_LD3_TONS").val(Math.round(data.CTOI_LD3_TONS || 0));
                    $("#TXT_CTOI_MRDTP_TONS").val(Math.round(data.CTOI_MRDTP_TONS || 0));
                }
                else {

                    alert(response.message);
                }
            },

            error: function (xhr, status, error) {

                alert("Error occurred while loading data");
                console.log(error);
            }
        });
    }
</script>
