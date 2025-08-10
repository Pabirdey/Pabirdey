<select name="CAST_CLAY_COND" class="form-select form-select-lg">
    <option value="" ${!data.CAST_CLAY_COND ? 'selected' : ''}>NULL</option>
    <option value="WET" ${data.CAST_CLAY_COND === 'WET' ? 'selected' : ''}>WET</option>
    <option value="DRY" ${data.CAST_CLAY_COND === 'DRY' ? 'selected' : ''}>DRY</option>
    <option value="EXCESS WET" ${data.CAST_CLAY_COND === 'EXCESS WET' ? 'selected' : ''}>EXCESS WET</option>
    <option value="BLEEDING" ${data.CAST_CLAY_COND === 'BLEEDING' ? 'selected' : ''}>BLEEDING</option>
</select>
