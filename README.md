<td>
    <input type="text"
           class="table-input ${
               item.TLC_NO >= 1 && item.TLC_NO <= 16
                   ? 'blue-bg'
                   : item.TLC_NO >= 17 && item.TLC_NO <= 27
                       ? 'green-bg'
                       : ''
           }"
           value="${item.TLC_NO || ''}"
           readonly>
</td>
