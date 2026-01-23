<script>
function toggleList(i) {
    // Close all other lists
    document.querySelectorAll('.list-box').forEach(box => box.style.display = 'none');
    // Toggle this one
    const list = document.getElementById('list_' + i);
    list.style.display = (list.style.display === 'block') ? 'none' : 'block';
}

function selectItem(el, i) {
    const val = el.innerText.trim();
    // Always close the dropdown first
    document.getElementById('list_' + i).style.display = 'none';

    if (val === "OTHERS") {
        // Show modal for other value
        document.getElementById('hdnRowIndex').value = i;
        document.getElementById('txtOtherMGClay').value = '';
        const modal = new bootstrap.Modal(document.getElementById('mgClayOtherModal'));
        modal.show();
        return;
    }

    // Set the selected value
    document.getElementById('clayInput_' + i).value = val;
}

// Optional: close dropdown if clicking outside
document.addEventListener('click', function(e) {
    if (!e.target.classList.contains('arrow-btn') && !e.target.closest('.list-box')) {
        document.querySelectorAll('.list-box').forEach(box => box.style.display = 'none');
    }
});
</script>
