<script>
    // Change this to your actual table's ID
    const inputs = document.querySelectorAll('#tapHoleTable input');

    inputs.forEach(input => {
        input.addEventListener('click', function () {
            // Remove highlight from all rows
            document.querySelectorAll('#tapHoleTable tr').forEach(row => {
                row.classList.remove('highlight');
            });

            // Highlight the clicked row
            const row = this.closest('tr');
            if (row) {
                row.classList.add('highlight');
            }
        });
    });
</script>