<select name="CAST_TYPE" class="form-select form-select-lg">
    <option value="" ${!data.CAST_TYPE ? 'selected' : ''}>NULL</option>
    <option value="DRY" ${data.CAST_TYPE === 'DRY' ? 'selected' : ''}>DRY</option>
    <option value="NOT DRY" ${data.CAST_TYPE === 'NOT DRY' ? 'selected' : ''}>NOT DRY</option>
</select>
