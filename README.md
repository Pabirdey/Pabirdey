<td>
    ${
        item.TLC_FUR_FACE == 2
        ? '<span class="green-dot"></span>'
        : item.TLC_FUR_FACE == 1
            ? '<span class="red-dot"></span>'
            : '<input type="text" class="table-input" value="' + (item.TLC_FUR_FACE || '') + '" readonly>'
    }
</td>
