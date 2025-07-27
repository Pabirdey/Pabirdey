tableBody += `<td>
  <select class='form-select form-select-md'>
    <option ${!parsedData[i].CAST_CLAY_COND ? 'selected' : ''} value="">-- Select --</option>
    <option ${parsedData[i].CAST_CLAY_COND === 'WET' ? 'selected' : ''}>WET</option>
    <option ${parsedData[i].CAST_CLAY_COND === 'DRY' ? 'selected' : ''}>DRY</option>
    <option ${parsedData[i].CAST_CLAY_COND === 'EXCESS WET' ? 'selected' : ''}>EXCESS WET</option>
    <option ${parsedData[i].CAST_CLAY_COND === 'BLEEDING' ? 'selected' : ''}>BLEEDING</option>
  </select>
</td>`;
