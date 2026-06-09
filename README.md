 function BindTable(data) {            
            $("#tblBody").empty();
            var totalRows = 15;
            var dataCount = data.length;
            if (dataCount > 0) {
                $.each(data, function (i, item) {
                    var row = `<tr>
                <td><input type="text" class="table-input" value="${item.CAST_NO || ''}"></td>
                <td>
    <input type="time"
           class ="table-input"
           min="09:00"
           max="17:00"
           value="${item.CAST_ST_TIME || ''}">
</td>

                <td><input type="time" class="table-input" value="${item.CAST_END_TIME || ''}"></td>
                <td><input type="text" class="table-input" value="${item.TRP_NO || ''}"></td>
                <td><input type="time" class="table-input" value="${item.LADLE_FLST_TIME || ''}"></td>
                <td><input type="time" class="table-input" value="${item.LADLE_FLEND_TIME || ''}"></td>
                <td>
                    <select class ="table-input arrivedFrom">
                        <option value=""></option>
                        <option value="C" ${item.ARRIVED_FROM === 'C' ? 'selected': ''}>C</option>
                        <option value="E" ${item.ARRIVED_FROM === 'E' ? 'selected': ''}>E</option>
                        <option value="F" ${item.ARRIVED_FROM === 'F' ? 'selected': ''}>F</option>
                        <option value="C" ${item.ARRIVED_FROM === 'G' ? 'selected': ''}>G</option>
                        <option value="E" ${item.ARRIVED_FROM === 'H' ? 'selected': ''}>H</option>
                        <option value="F" ${item.ARRIVED_FROM === 'I' ? 'selected': ''}>I</option>
                    </select>
               </td>
               console.log(item.ARRIVED_FROM);
                <td><input type="text" class="table-input" value="${item.GROSS_WT || ''}"></td>
                <td><input type="text" class="table-input" value="${item.TARE_WT || ''}"></td>
                <td><input type="text" class="table-input" value="${item.NET_WT || ''}"></td>
                <td><input type="text" class="table-input" value="${item.POURING_RATE || ''}"></td>
                <td><input type="text" class="table-input" value="${item.HMT || ''}"></td>
                <td><input type="text" class="table-input" value="${item.REASON_POURING || ''}"></td>
                <td><input type="text" class="table-input" value="${item.SEQ_NO || ''}"></td>
                <td><button type="button" class="btnDelete">Delete</button></td>
            </tr>`;

                    $("#tblBody").append(row);
                });

                
                for (var i = dataCount; i < totalRows; i++) {

                    var blankRow = `<tr>
                <td><input type="text" class="table-input"></td>
                <td><input type="text" class="table-input"></td>
                <td><input type="text" class="table-input"></td>
                <td><input type="text" class="table-input"></td>
                <td><input type="text" class="table-input"></td>
                <td><input type="text" class="table-input"></td>

                <td>
                    <select class ="table-input arrivedFrom">                    
                        <option value=""></option>
                        <option value="C">C</option>
                        <option value="E">E</option>
                        <option value="F">F</option>
                        <option value="F">G</option>
                        <option value="F">H</option>
                        <option value="F">I</option>
                    </select>
                </td>

                <td><input type="text" class="table-input"></td>
                <td><input type="text" class="table-input"></td>
                <td><input type="text" class="table-input"></td>
                <td><input type="text" class="table-input"></td>
                <td><input type="text" class="table-input"></td>
                <td><input type="text" class="table-input"></td>
                <td><input type="text" class="table-input"></td>
                <td><button type="button" class="btnDelete">Delete</button></td>
            </tr>`;

                    $("#tblBody").append(blankRow);
                }
            }
            else {

               
                for (var i = 0; i < totalRows; i++) {

                    var blankRow = `<tr>
                <td><input type="text" class="table-input"></td>
                <td><input type="text" class="table-input"></td>
                <td><input type="text" class="table-input"></td>
                <td><input type="text" class="table-input"></td>
                <td><input type="text" class="table-input"></td>
                <td><input type="text" class="table-input"></td>

                <td>
                    <select class ="table-input arrivedFrom">                    
                        <option value=""></option>
                        <option value="C">C</option>
                        <option value="E">E</option>
                        <option value="F">F</option>
                        <option value="F">G</option>
                        <option value="F">H</option>
                        <option value="F">I</option>
                    </select>
                </td>

                <td><input type="text" class="table-input"></td>
                <td><input type="text" class="table-input"></td>
                <td><input type="text" class="table-input"></td>
                <td><input type="text" class="table-input"></td>
                <td><input type="text" class="table-input"></td>
                <td><input type="text" class="table-input"></td>
                <td><input type="text" class="table-input"></td>
                <td><button type="button" class="btnDelete">Delete</button></td>
            </tr>`;

                    $("#tblBody").append(blankRow);
                }
            }
        }
