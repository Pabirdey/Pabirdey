 function RowHighlight_Tap_Hole() {
            debugger;
            const inputs = document.querySelectorAll('#TAP_Hot_Metal_Details input');
            inputs.forEach(input=> {
                input.addEventListener('click', function () {
                    document.querySelectorAll('#TAP_Hot_Metal_Details tr').forEach(row=> {
                        row.classList.remove('highlight');
                    });
                    const row = this.closest('tr');
                    if (row) {
                        row.classList.add('highlight');
                    }
                });
            });
            }
