tableBody += `
<td class="d-flex gap-0">
    <input name="LOT_NO" style="width:120px;" value="${parsedData[i].LOT_NO}" />
    <button type="button"
            class="btn btn-primary btn-sm getLot"
            data-castno="${parsedData[i].LOT_NO}">
        ::
    </button>
</td>`;

tableBody += `
<td>
    <input name="NO_OF_BAGS"
           class="form-control form-control-lg"
           value="${parsedData[i].NO_OF_BAGS}" />
</td>`;

tableBody += `
<td>
    <input name="MUDGUN_HOLD_TIME"
           class="form-control form-control-lg"
           value="${parsedData[i].MUDGUN_HOLD_TIME}" />
</td>`;

tableBody += `
<td>
    <select name="MUDGUN_NOZZLE" class="form-select form-select-lg">
        <option value="" ${!parsedData[i].MUDGUN_NOZZLE ? 'selected' : ''}></option>
        <option value="REPLACEMENT"
            ${parsedData[i].MUDGUN_NOZZLE === 'REPLACEMENT' ? 'selected' : ''}>
            REPLACEMENT
        </option>
        <option value="WEILD"
            ${parsedData[i].MUDGUN_NOZZLE === 'WEILD' ? 'selected' : ''}>
            WEILD
        </option>
    </select>
</td>`;
