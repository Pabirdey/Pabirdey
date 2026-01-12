<script>
    var activeRowIndex = null;

    /* 🔥 MUST be window.function */
    window.toggleList = function (index) {
        var list = document.getElementById("list_" + index);
        if (!list) return;

        list.style.display = (list.style.display === "block") ? "none" : "block";
    };

    window.selectItem = function (event, el, index) {
        event.stopPropagation();

        document.getElementById("clayInput_" + index).value = el.innerText;
        document.getElementById("list_" + index).style.display = "none";

        if (el.innerText === "OTHERS") {
            activeRowIndex = index;
            bootstrap.Modal
                .getOrCreateInstance(document.getElementById("clayModal"))
                .show();
        }
    };

    document.addEventListener("click", function (e) {
        if (!e.target.closest(".input-wrapper")) {
            document.querySelectorAll(".list-box").forEach(x => x.style.display = "none");
        }
    });
</script>

<script>
function Display_Mudgun_Details(lsSelectedFDate, IsSelectedFur) {

    $.ajax({
        url: '@Url.Action("Get_Display_Mudgun_Details", "CastHouse")',
        type: 'GET',
        data: { Fdate: lsSelectedFDate, Fur: IsSelectedFur },
        success: function (result) {

            var parsedData = JSON.parse(result);
            var html = "";

            for (var i = 0; i < parsedData.length; i++) {

                html += `
                <tr>
                    <td>
                        <input class="form-control" value="${parsedData[i].CAST_NO}" readonly>
                    </td>

                    <td>
                        <div class="input-wrapper position-relative">
                            <input type="text"
                                   id="clayInput_${i}"
                                   class="form-control"
                                   value="${parsedData[i].MG_CLAY_USED || ''}">

                            <span class="arrow-btn"
                                  onclick="toggleList(${i})">▼</span>

                            <div class="list-box" id="list_${i}">
                                <div onclick="selectItem(event,this,${i})">ACE</div>
                                <div onclick="selectItem(event,this,${i})">BRL</div>
                                <div onclick="selectItem(event,this,${i})">LRH</div>
                                <div onclick="selectItem(event,this,${i})">OTHERS</div>
                            </div>
                        </div>
                    </td>
                </tr>`;
            }

            $("#Mudgun_Details tbody").html(html);
        }
    });
}
</script>

