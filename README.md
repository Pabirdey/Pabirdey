$(document).on("click", "#Driling_Slag_Details *", "#TAP_Hot_Metal_Details *", function () {
                debugger;
                let row = $(this).closest("tr"); // Get the parent row
                if (!row.length) return;
                let castNo = row.attr("data-castno");
                if (!castNo) return;
                castNo = castNo.trim();
                // Remove previous highlight
                $("#Driling_Slag_Details tr").removeClass("highlight");
                $("#TAP_Hot_Metal_Details tr").removeClass("highlight");
                // Highlight the row
                row.addClass("highlight");
            });
