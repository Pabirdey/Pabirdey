 <select name="COLOR_FUME_DRILLING" class ='form-select form-select-lg'>
                                                <option ${!parsedData[i].COLOR_FUME_DRILLING ? 'selected': ''} value=""></option>
                                                <option ${parsedData[i].COLOR_FUME_DRILLING === 'BROWN' ? 'selected': ''}>BROWN</option>
                                                <option ${parsedData[i].COLOR_FUME_DRILLING === 'WHITE' ? 'selected': ''}>WHITE</option>
                                                <option ${parsedData[i].COLOR_FUME_DRILLING === 'OTHERS' ? 'selected': ''}>OTHERS</option>
                                                </select>
