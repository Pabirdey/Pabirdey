function formatDate(dt) {
    if (!dt) return "";

    let d = new Date(dt);
    let day = ("0" + d.getDate()).slice(-2);
    let month = ("0" + (d.getMonth() + 1)).slice(-2);
    let year = d.getFullYear();

    return day + "/" + month + "/" + year;
}
