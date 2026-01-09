tableBody += `
<td>
    <div class="input-wrapper">
        <input type="text"
               class="form-control form-control-lg clay-input"
               id="clayInput_${i}"
               name="MG_CLAY_USED"
               value="${parsedData[i].MG_CLAY_USED || ''}">

        <div class="arrow-btn"
             onclick="toggleList(${i})">▼</div>
    </div>

    <div class="list-box" id="list_${i}">
        <div onclick="selectItem(this, ${i})">ACE</div>
        <div onclick="selectItem(this, ${i})">BRL</div>
        <div onclick="selectItem(this, ${i})">LRH</div>
        <div onclick="selectItem(this, ${i})">UBQ</div>
        <div onclick="selectItem(this, ${i})">SARVESH</div>
        <div onclick="selectItem(this, ${i})">CALDYRS</div>
        <div onclick="selectItem(this, ${i})">VISUVIUS</div>
        <div onclick="selectItem(this, ${i})">OTHERS</div>
    </div>
</td>`;