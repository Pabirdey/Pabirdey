   $(document).on("click", "#Driling_Slag_Details *, #TAP_Hot_Metal_Details *,#Mudgun_Details *,#Other_Details *", function () {
            
            let row = $(this).closest("tr");
            if (!row.length) return;
            let castNo = row.attr("data-castno");
            if (!castNo) return;
            castNo = castNo.trim();
            $("#Driling_Slag_Details tr").removeClass("highlight");
            $("#TAP_Hot_Metal_Details tr").removeClass("highlight");
            $("#Mudgun_Details tr").removeClass("highlight");
            $("#Other_Details tr").removeClass("highlight");

            $('#Driling_Slag_Details tr[data-castno="' + castNo + '"]').addClass("highlight");
            $('#TAP_Hot_Metal_Details tr[data-castno="' + castNo + '"]').addClass("highlight");
            $('#Mudgun_Details tr[data-castno="' + castNo + '"]').addClass("highlight");
            $('#Other_Details tr[data-castno="' + castNo + '"]').addClass("highlight");
        });
