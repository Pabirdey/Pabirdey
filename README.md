<select name="CAST_CLAY_COND" class ='form-select form-select-lg'>
                                <option ${data.CAST_CLAY_COND === 'WET' ? 'selected': ''}>WET</option>
                                <option ${data.CAST_CLAY_COND === 'DRY' ? 'selected' : ''}>DRY</option>
                                <option ${data.CAST_CLAY_COND === 'EXCESS WET' ? 'selected' : ''}>EXCESS WET</option>
                                <option ${data.CAST_CLAY_COND === 'BLEEDING' ? 'selected' : ''}>BLEEDING</option>
