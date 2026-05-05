 cokeBody.append(
                                    "<tr>" +
                                    "<td><b>" + bunker + "</b></td>" +
                                    "<td><input type='number' class='form-control c' value='" + (cokeRow ? cokeRow.C : 0) + "'></td>" +
                                    "<td><input type='number' class='form-control e' value='" + (cokeRow ? cokeRow.E : 0) + "'></td>" +
                                    "<td><input type='number' class='form-control f' value='" + (cokeRow ? cokeRow.F : 0) + "'></td>" +
                                    "<td><input type='number' class='form-control total' readonly></td>" +
                                    "</tr>"
                                );                                
                                nutBody.append(
                                    "<tr>" +
                                    "<td><b>" + bunker + "</b></td>" +
                                    "<td><input type='number' class='form-control c' value='" + (nutRow ? nutRow.C : 0) + "'></td>" +
                                    "<td><input type='number' class='form-control e' value='" + (nutRow ? nutRow.E : 0) + "'></td>" +
                                    "<td><input type='number' class='form-control f' value='" + (nutRow ? nutRow.F : 0) + "'></td>" +
                                    "<td><input type='number' class='form-control total' readonly></td>" +
                                    "</tr>"
                                );
