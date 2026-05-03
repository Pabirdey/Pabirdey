function createRow(item = {}) {
    return `
    <tr>
        <td>
            <input type="text" class="form-control row-date" style="width:100px;" 
            value="${item.TIMESTAMP ? formatDate(item.TIMESTAMP) : ''}" readonly>
        </td>

        <td>
            <select class="form-control row-shift" style="height:30px;width:50px;">
                <option ${item.SHIFT=='A'?'selected':''}>A</option>
                <option ${item.SHIFT=='B'?'selected':''}>B</option>
                <option ${item.SHIFT=='C'?'selected':''}>C</option>
            </select>
        </td>

        <td>
            <select class="form-control bunker text-start ps-01" style="height:30px;width:200px;">
                <option value="">---Pls. Select---</option>
                <option ${item.BUNKER=='WESTERN'?'selected':''}>WESTERN</option>
                <option ${item.BUNKER=='MIDDLE'?'selected':''}>MIDDLE</option>
                <option ${item.BUNKER=='EASTERN'?'selected':''}>EASTERN</option>
                <option ${item.BUNKER=='H/S NC'?'selected':''}>H/S NC</option>
                <option ${item.BUNKER=='NC BF KO'?'selected':''}>NC BF KO</option>
                <option ${item.BUNKER=='ST.COKE-HALDIA'?'selected':''}>ST.COKE-HALDIA</option>
                <option ${item.BUNKER=='ST.COKE-IMPORTED'?'selected':''}>ST.COKE-IMPORTED</option>
                <option ${item.BUNKER=='ST.COKE-OWN'?'selected':''}>ST.COKE-OWN</option>
                <option ${item.BUNKER=='ST.COKE-TOTAL'?'selected':''}>ST.COKE-TOTAL</option>
                <option ${item.BUNKER=='B/H HIGH ASH'?'selected':''}>B/H HIGH ASH</option>
                <option ${item.BUNKER=='B/H LOW ASH'?'selected':''}>B/H LOW ASH</option>
                <option ${item.BUNKER=='B/H COKE-TOTAL'?'selected':''}>B/H COKE-TOTAL</option>
                <option ${item.BUNKER=='ROUGH BREEZE'?'selected':''}>ROUGH BREEZE</option>
                <option ${item.BUNKER=='PLS_25MM_NC'?'selected':''}>PLS_25MM_NC</option>
            </select>
        </td>

        <td><input type="text" class="form-control val c" value="${item.C || ''}"></td>
        <td><input type="text" class="form-control val e" value="${item.E || ''}"></td>
        <td><input type="text" class="form-control val f" value="${item.F || ''}"></td>

        <td><input type="text" class="form-control total" value="${item.TOTAL || ''}" readonly></td>
        <td><input type="text" class="form-control position" value="${item.BUNKER_POSITION || ''}"></td>
        <td><input type="text" class="form-control balance" value="${item.BALANCE || ''}"></td>
    </tr>`;
}
