<td>
    <div class="input-wrapper">
        <input type="text"
               class="form-control form-control-lg"
               id="clayInput_${i}"
               name="MG_CLAY_USED"
               value="${parsedData[i].MG_CLAY_USED || ''}">

        <div class="arrow-btn" onclick="toggleList(${i})">▼</div>

        <div class="list-box" id="list_${i}">
            <div onclick="selectItem(this, ${i})">ACE</div>
            <div onclick="selectItem(this, ${i})">BRL</div>
            <div onclick="selectItem(this, ${i})">LRH</div>
            <div onclick="selectItem(this, ${i})">UBQ</div>
            <div onclick="selectItem(this, ${i})">SARVESH</div>
            <div onclick="selectItem(this, ${i})">OTHERS</div>
        </div>
    </div>
</td>

<script>
let activeRowIndex = null;

/* OPEN / CLOSE LIST */
function toggleList(index) {
    event.stopPropagation();   // 🔥 IMPORTANT

    // close other lists
    document.querySelectorAll('.list-box').forEach(l => l.style.display = 'none');

    const list = document.getElementById("list_" + index);
    list.style.display = (list.style.display === "block") ? "none" : "block";
}

/* SELECT ITEM */
function selectItem(el, index) {
    document.getElementById("clayInput_" + index).value = el.innerText;
    document.getElementById("list_" + index).style.display = "none";

    if (el.innerText === "OTHERS") {
        activeRowIndex = index;
        // open modal if required
        // bootstrap.Modal.getOrCreateInstance(document.getElementById("clayModal")).show();
    }
}

/* CLOSE LIST WHEN CLICK OUTSIDE */
document.addEventListener("click", function () {
    document.querySelectorAll('.list-box').forEach(l => l.style.display = 'none');
});
</script>


<style>
.input-wrapper {
    position: relative;
}

.arrow-btn {
    position: absolute;
    right: 5px;
    top: 6px;
    cursor: pointer;
    user-select: none;
}

.list-box {
    display: none;
    position: absolute;
    background: white;
    border: 1px solid #ccc;
    width: 100%;
    max-height: 200px;
    overflow-y: auto;
    z-index: 9999;
}

.list-box div {
    padding: 6px;
    cursor: pointer;
}

.list-box div:hover {
    background: #f0f0f0;
}
</style>