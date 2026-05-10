<td>
    <input type="text"
           class="form-control c"
           value="${item.C || ''}"
           onkeyup="calculateTotal(this)">
</td>

<td>
    <input type="text"
           class="form-control e"
           value="${item.E || ''}"
           onkeyup="calculateTotal(this)">
</td>

<td>
    <input type="text"
           class="form-control f"
           value="${item.F || ''}"
           onkeyup="calculateTotal(this)">
</td>

<td>
    <input type="text"
           class="form-control total"
           value="${item.TOTAL || ''}"
           readonly>
</td>
