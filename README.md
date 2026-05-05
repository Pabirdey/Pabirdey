cokeBody.append(
    "<tr>" +
    "<td><b>" + bunker + "</b></td>" +
    "<td><input type='number' class='form-control c' value='" + (cokeRow ? getVal(cokeRow.C) : "") + "'></td>" +
    "<td><input type='number' class='form-control e' value='" + (cokeRow ? getVal(cokeRow.E) : "") + "'></td>" +
    "<td><input type='number' class='form-control f' value='" + (cokeRow ? getVal(cokeRow.F) : "") + "'></td>" +
    "<td><input type='number' class='form-control total' readonly></td>" +
    "</tr>"
);

nutBody.append(
    "<tr>" +
    "<td><b>" + bunker + "</b></td>" +
    "<td><input type='number' class='form-control c' value='" + (nutRow ? getVal(nutRow.C) : "") + "'></td>" +
    "<td><input type='number' class='form-control e' value='" + (nutRow ? getVal(nutRow.E) : "") + "'></td>" +
    "<td><input type='number' class='form-control f' value='" + (nutRow ? getVal(nutRow.F) : "") + "'></td>" +
    "<td><input type='number' class='form-control total' readonly></td>" +
    "</tr>"
);
