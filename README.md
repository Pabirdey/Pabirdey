tableBody += `<tr data-castno='${parsedData[i].CAST_NO}'>`;

tableBody += `<td>
                <input name="CAST_NO" 
                       class="form-control form-control-lg"
                       value="${parsedData[i].CAST_NO}" 
                       readonly />
              </td>`;