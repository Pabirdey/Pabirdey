<select name="TAPHOLE_BEHAVIOUR" class="form-select form-select-lg">
    <option value="" ${!data.TAPHOLE_BEHAVIOUR ? 'selected' : ''}></option>
    <option value="WIDE" ${data.TAPHOLE_BEHAVIOUR === 'WIDE' ? 'selected' : ''}>WIDE</option>
    <option value="NORMAL" ${data.TAPHOLE_BEHAVIOUR === 'NORMAL' ? 'selected' : ''}>NORMAL</option>
    <option value="WIDE+COKE TROUBLE" ${data.TAPHOLE_BEHAVIOUR === 'WIDE+COKE TROUBLE' ? 'selected' : ''}>WIDE+COKE TROUBLE</option>
    <option value="NORMAL+COKE TROUBLE" ${data.TAPHOLE_BEHAVIOUR === 'NORMAL+COKE TROUBLE' ? 'selected' : ''}>NORMAL+COKE TROUBLE</option>
</select>
