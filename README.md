<td>
    ${
        item.TLC_FUR_FACE == 2
        ? '<span class="green-dot"></span>'
        : '<input type="text" class="table-input" value="' + (item.TLC_FUR_FACE || '') + '" readonly>'
    }
</td>

.green-dot {
    display: inline-block;
    width: 15px;
    height: 15px;
    background-color: green;
    border-radius: 50%;
}
