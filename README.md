tbody.empty();

if (res.success && res.data.length > 0) {

    // Database rows
    res.data.forEach(function (item) {
        tbody.append(createRow(item));
    });

    // Remaining blank rows
    let remainingRows = 8 - res.data.length;

    for (let i = 0; i < remainingRows; i++) {
        tbody.append(createRow());
    }

} else {

    // If no data then show 8 blank rows
    for (let i = 0; i < 8; i++) {
        tbody.append(createRow());
    }
}
