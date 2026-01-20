//=====================================================
// SHIFT LOGIC AS PER YOUR RULE
//=====================================================
function getShiftFromTime(dt) {

    if (!dt) return "A";

    var date = new Date(dt);
    var hour = date.getHours();
    var min = date.getMinutes();

    var totalMin = hour * 60 + min;

    // 06:00 – 13:59  → A
    if (totalMin >= 360 && totalMin < 840) {
        return "A";
    }

    // 14:00 – 21:59 → B
    if (totalMin >= 840 && totalMin < 1320) {
        return "B";
    }

    // 22:00 – 05:59 → C
    return "C";
}