
        $(document).ready(function () {
            loadFinesData();
        });       
        function loadFinesData() {
            $('#loader').show();
            $.ajax({
                url: '/Ore_Beneficiation/GetFinesData',
                type: 'GET',
                dataType: 'json',
                success: function (res) {                                        
                    if (res && res.error) {
                        showError(res.error);
                    }                    
                    else if (res && res.data) {
                        renderTable(res.data);
                    }
                    else {
                        renderTable(res);
                    }

                    $('#loader').hide();
                },

                error: function () {
                    $('#loader').hide();
                    showError("Error loading data");
                }
            });
        }
