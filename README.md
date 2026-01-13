let currentIndex = null;

function toggleList(i) {
    document.getElementById("list_" + i).classList.toggle("show");
}

function selectItem(el, i) {
    let value = el.innerText;
    let input = document.getElementById("clayInput_" + i);

    input.value = value;
    document.getElementById("list_" + i).classList.remove("show");

    // ⭐ THIS IS THE FIX
    if (value === "OTHERS") {
        currentIndex = i;
        document.getElementById("otherClayValue").value = "";
        let modal = new bootstrap.Modal(document.getElementById("othersModal"));
        modal.show();
    }
}

tableBody += `
<td>
  <div class="input-wrapper">
    <input type="text"
           class="form-control form-control-lg"
           id="clayInput_${i}"
           name="MG_CLAY_USED">

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
</td>`;