function calculateRow(row) {

    let bunker = row.querySelector(".bunker").value;
    let A = parseFloat(row.querySelector(".a")?.value) || 0;
    let B = parseFloat(row.querySelector(".b")?.value) || 0;
    let C = parseFloat(row.querySelector(".c")?.value) || 0;
    let D = parseFloat(row.querySelector(".d")?.value) || 0;
    let E = parseFloat(row.querySelector(".e")?.value) || 0;
    let F = parseFloat(row.querySelector(".f")?.value) || 0;

    // ✅ TOTAL
    let total = A + B + C + D + E + F;
    row.querySelector(".total").value = total || "";

    // 🔥 CONDITIONS (Converted from Oracle)

    let result = {
        TON_F_SC_S: 0,
        TON_F_NC_H: 0,
        TON_F_NC_BF_KO: 0,
        TON_F_NC_P25: 0
    };

    // 👉 ST.COKE logic
    if (bunker && bunker.substring(0, 7) === "ST.COKE") {
        result.TON_F_SC_S = F * 40;
    }

    // 👉 H/S NC
    if (bunker === "H/S NC") {
        result.TON_F_NC_H = F * 21;
    }

    // 👉 NC BF KO
    if (bunker === "NC BF KO") {
        result.TON_F_NC_BF_KO = F * 12;
    }

    // 👉 PLS_25MM_NC
    if (bunker === "PLS_25MM_NC") {
        result.TON_F_NC_P25 = F * 40;
    }

    console.log("Calculated:", result);

    return result;
}
