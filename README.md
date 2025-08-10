                                                <select name="DRILL_TYPE" class ='form-select form-select-lg'>
                                                <option ${!parsedData[i].DRILL_TYPE ? 'selected': ''} value=""></option>
                                                <option ${parsedData[i].DRILL_TYPE === 'LANCING' ? 'selected': ''}>LANCING</option>
                                                <option ${parsedData[i].DRILL_TYPE === 'DANGO DRILL' ? 'selected': ''}>DANGO DRILL</option>
                                                <option ${parsedData[i].DRILL_TYPE === 'SELF' ? 'selected': ''}>SELF</option>
                                                </select>
