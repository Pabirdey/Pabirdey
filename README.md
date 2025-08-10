<select name="COLOR_FUME_DRILLING" class="form-select form-select-lg">
    <option value="" ${!parsedData[i].COLOR_FUME_DRILLING ? 'selected' : ''}></option>
    <option value="BROWN" ${parsedData[i].COLOR_FUME_DRILLING === 'BROWN' ? 'selected' : ''}>BROWN</option>
    <option value="WHITE" ${parsedData[i].COLOR_FUME_DRILLING === 'WHITE' ? 'selected' : ''}>WHITE</option>
    <option value="OTHERS" ${parsedData[i].COLOR_FUME_DRILLING === 'OTHERS' ? 'selected' : ''}>OTHERS</option>
</select>
