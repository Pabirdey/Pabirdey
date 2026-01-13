I can help you improve this code! Here are the issues and fixes:
let currentIndex = null;

function toggleList(i) {
    const list = document.getElementById("list_" + i);
    if (list) {
        list.classList.toggle("show");
    }
}

function selectItem(el, i) {
    const value = el.innerText;
    const input = document.getElementById("clayInput_" + i);
    const list = document.getElementById("list_" + i);

    if (input) {
        input.value = value;
    }
    
    if (list) {
        list.classList.remove("show");
    }

    // Handle "OTHERS" option
    if (value === "OTHERS") {
        currentIndex = i;
        const modalElement = document.getElementById("clayModal");
        
        if (modalElement) {
            // Clear modal input if it exists
            const modalInput = modalElement.querySelector('input[type="text"]');
            if (modalInput) {
                modalInput.value = "";
            }
            
            const modal = new bootstrap.Modal(modalElement);
            modal.show();
        }
    }
}
Key improvements:
Added null checks - Prevents errors if elements don't exist
Used const instead of let - For variables that don't change
Fixed modal input clearing - You need to find the actual input element inside the modal
Better structure - More defensive programming
Additional recommendation: If you have a function to handle the modal's "Save" button, it should look something like this:
function saveModalValue() {
    const modalInput = document.getElementById("clayModal").querySelector('input[type="text"]');
    if (modalInput && currentIndex !== null) {
        const input = document.getElementById("clayInput_" + currentIndex);
        if (input) {
            input.value = modalInput.value;
        }
    }
}
Would you like me to help with any other part of this dropdown/modal functionality?