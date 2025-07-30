 $('#lstFur').change(function () {
                IsSelectedFur = $('#lstFur option:selected').val();
                Display_Tap_Hole_Details(lsSelectedFDate, IsSelectedFur);
                Display_Driling_Details(lsSelectedFDate, IsSelectedFur);
                Display_Mudgun_Details(lsSelectedFDate, IsSelectedFur);
                Display_Other_Details(lsSelectedFDate, IsSelectedFur);
            });
