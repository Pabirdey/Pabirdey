                                      <select name="DRILL_TYPE" class="form-select form-select-lg">
                                      <option value="" ${!parsedData[i].DRILL_TYPE ? 'selected' : ''}>NULL</option>
                                      <option value="LANCING" ${parsedData[i].DRILL_TYPE === 'LANCING' ? 'selected' : ''}>LANCING</option>
                                      <option value="DANGO DRILL" ${parsedData[i].DRILL_TYPE === 'DANGO DRILL' ? 'selected' : ''}>DANGO DRILL</option>
                                      <option value="SELF" ${parsedData[i].DRILL_TYPE === 'SELF' ? 'selected' : ''}>SELF</option>
                                    </select>
