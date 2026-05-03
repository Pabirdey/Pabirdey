 <script>
        function createRow() {
            return `
    <tr>
        <td><input type="date" class="form-control row-date"></td>

        <td>
            <select class="form-control row-shift" style="height:30px;width:50px;">
                <option>A</option>
                <option>B</option>
                <option>C</option>
            </select>
        </td>

        
        <td>
            <select class ="form-control text-start ps-01" style="height:30px;width:220px;">
                <option value="">---Pls. Select---</option>
                <option value="WESTERN">WESTERN</option>
                <option value="MIDDLE">MIDDLE</option>
                <option value="EASTERN">EASTERN</option>
                <option value="H/S NC">H/S NC</option>
                <option value="NC BF KO">NC BF KO</option>
                <option value="ST.COKE-HALDIA">ST.COKE-HALDIA</option>
                <option value="ST.COKE-IMPORTED">ST.COKE-IMPORTED</option>
                <option value="ST.COKE-OWN">ST.COKE-OWN</option>
                <option value="ST.COKE-TOTAL">ST.COKE-TOTAL</option>
                <option value="B/H HIGH ASH">B/H HIGH ASH</option>
                <option value="B/H LOW ASH">B/H LOW ASH</option>
                <option value="B/H COKE-TOTAL">B/H COKE-TOTAL</option>
                <option value="ROUGH BREEZE">ROUGH BREEZE</option>
                <option value="PLS_25MM_NC">PLS_25MM_NC</option>
            </select>
        </td>

        <td><input class="form-control"></td>
        <td><input class="form-control"></td>
        <td><input class="form-control"></td>
        <td><input class="form-control total" readonly></td>
        <td><input class="form-control"></td>
        <td><input class="form-control"></td>
    </tr>`;
        }

        // generate rows
        for (let i = 0; i < 8; i++) {
            document.getElementById("tblBody").innerHTML += createRow();
        }

    </script>
