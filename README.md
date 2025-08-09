tableBody += "<td><select class='form-select form-select-md'>";
tableBody += `<option value=""></option>`;
tableBody += `<option ${(parsedData[i].CAST_CLAY_COND === 'WET') ? 'selected' : ''}>WET</option>`;
tableBody += `<option ${(parsedData[i].CAST_CLAY_COND === 'DRY') ? 'selected' : ''}>DRY</option>`;
tableBody += `<option ${(parsedData[i].CAST_CLAY_COND === 'EXCESS WET') ? 'selected' : ''}>EXCESS WET</option>`;
tableBody += `<option ${(parsedData[i].CAST_CLAY_COND === 'BLEEDING') ? 'selected' : ''}>BLEEDING</option>`;
tableBody += "</select></td>";
Swal.fire({
    icon: 'success',
    text: 'Data Saved successfully!',
    showConfirmButton: true,
    customClass: {
        popup: 'my-swal-popup',   // Popup box
        title: 'my-swal-title',   // Title text
        htmlContainer: 'my-swal-text' // Text body
    }
});
.my-swal-popup {
    font-family: 'Arial', sans-serif; /* Whole popup font */
}

.my-swal-title {
    font-family: 'Georgia', serif;    /* Title font */
    font-size: 22px;                   /* Title size */
}

.my-swal-text {
    font-family: 'Verdana', sans-serif; /* Message text font */
    font-size: 18px;                     /* Message text size */
}
