<script>
function toggleList(i) {
    // Close all other lists using a simple for loop
    var lists = document.getElementsByClassName('list-box');
    for (var j = 0; j < lists.length; j++) {
        lists[j].style.display = 'none';
    }

    // Toggle current list
    var list = document.getElementById('list_' + i);
    list.style.display = (list.style.display === 'block') ? 'none' : 'block';
}

function selectItem(el, i) {
    var val = el.innerText.trim();

    // Close the dropdown
    document.getElementById('list_' + i).style.display = 'none';

    if (val === "OTHERS") {
        // Show modal for other value
        document.getElementById('hdnRowIndex').value = i;
        document.getElementById('txtOtherMGClay').value = '';
        var modalEl = document.getElementById('mgClayOtherModal');
        var modal = new bootstrap.Modal(modalEl);
        modal.show();
        return;
    }

    // Set the selected value
    document.getElementById('clayInput_' + i).value = val;
}

// Close all dropdowns if clicking outside
document.addEventListener('click', function(e) {
    if (!e.target.classList.contains('arrow-btn') && !e.target.closest('.list-box')) {
        var lists = document.getElementsByClassName('list-box');
        for (var j = 0; j < lists.length; j++) {
            lists[j].style.display = 'none';
        }
    }
});
</script>
