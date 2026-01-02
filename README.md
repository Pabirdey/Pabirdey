 tableBody += `<td>
                                <input list="MG_CLAY_USED" class ="form-control" placeholder="Select or Type">
                                <datalist id="MG_CLAY_USED">
                                 <option ${!parsedData[i].MG_CLAY_USED ? 'selected': ''} value=""></option>
                                         ${[
                                        'LRH', 'UBQ', 'SARVESH', 'CALDYRS', 'HARIMA(S)', 'HARIMA(D)', 'CORUS', 'TRB', 'VISUVIUS',
                                        'HARIMA-TWH4', 'HARIMA-CPH4', 'HARIMA(D)-TWH5',
                                        'HARIMA(D)-TWH5K', 'HARIMA(D)-TWH5-T'
                                 ].map(option =>
                                `<option ${parsedData[i].MG_CLAY_USED === option ? 'selected': ''}>${option}</option>`).join("")}
                                </datalist>       
