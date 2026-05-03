function createRow(item = {}) {
    return `
    <tr>
        <td>
            <input type="text" class="form-control row-date"
            value="${formatDate(item.TIMESTAMP)}" readonly>
        </td>

        <td>
            <select class="form-control row-shift">
                <option value="A" ${item.SHIFT === 'A' ? 'selected' : ''}>A</option>
                <option value="B" ${item.SHIFT === 'B' ? 'selected' : ''}>B</option>
                <option value="C" ${item.SHIFT === 'C' ? 'selected' : ''}>C</option>
            </select>
        </td>

        <td>
            <select class="form-control bunker">
                <option value="">---Pls. Select---</option>

                <option value="WESTERN" ${item.BUNKER === 'WESTERN' ? 'selected' : ''}>WESTERN</option>
                <option value="MIDDLE" ${item.BUNKER === 'MIDDLE' ? 'selected' : ''}>MIDDLE</option>
                <option value="EASTERN" ${item.BUNKER === 'EASTERN' ? 'selected' : ''}>EASTERN</option>
                <option value="H/S NC" ${item.BUNKER === 'H/S NC' ? 'selected' : ''}>H/S NC</option>
                <option value="NC BF KO" ${item.BUNKER === 'NC BF KO' ? 'selected' : ''}>NC BF KO</option>
                <option value="ST.COKE-HALDIA" ${item.BUNKER === 'ST.COKE-HALDIA' ? 'selected' : ''}>ST.COKE-HALDIA</option>
                <option value="ST.COKE-IMPORTED" ${item.BUNKER === 'ST.COKE-IMPORTED' ? 'selected' : ''}>ST.COKE-IMPORTED</option>
                <option value="ST.COKE-OWN" ${item.BUNKER === 'ST.COKE-OWN' ? 'selected' : ''}>ST.COKE-OWN</option>
                <option value="ST.COKE-TOTAL" ${item.BUNKER === 'ST.COKE-TOTAL' ? 'selected' : ''}>ST.COKE-TOTAL</option>
                <option value="B/H HIGH ASH" ${item.BUNKER === 'B/H HIGH ASH' ? 'selected' : ''}>B/H HIGH ASH</option>
                <option value="B/H LOW ASH" ${item.BUNKER === 'B/H LOW ASH' ? 'selected' : ''}>B/H LOW ASH</option>
                <option value="B/H COKE-TOTAL" ${item.BUNKER === 'B/H COKE-TOTAL' ? 'selected' : ''}>B/H COKE-TOTAL</option>
                <option value="ROUGH BREEZE" ${item.BUNKER === 'ROUGH BREEZE' ? 'selected' : ''}>ROUGH BREEZE</option>
                <option value="PLS_25MM_NC" ${item.BUNKER === 'PLS_25MM_NC' ? 'selected' : ''}>PLS_25MM_NC</option>
            </select>
        </td>

        <td><input type="text" class="form-control c" value="${item.C || ''}"></td>
        <td><input type="text" class="form-control e" value="${item.E || ''}"></td>
        <td><input type="text" class="form-control f" value="${item.F || ''}"></td>

        <td><input type="text" class="form-control total" value="${item.TOTAL || ''}" readonly></td>

        <td><input type="text" class="form-control position" value="${item.BUNKER_POSITION || ''}"></td>
        <td><input type="text" class="form-control balance" value="${item.BALANCE || ''}"></td>
    </tr>`;
}
