 function calculateAF_ActOnDate() {
            debugger;
            var n1 = parseFloat(document.getElementById("CBF_ActOnDate").value) || 0;
            var n2 = parseFloat(document.getElementById("EBF_ActOnDate").value) || 0;
            var n3 = parseFloat(document.getElementById("FBF_ActOnDate").value) || 0;
            var n4 = parseFloat(document.getElementById("GBF_ActOnDate").value) || 0;
            var n5 = parseFloat(document.getElementById("HBF_ActOnDate").value) || 0;
            var n6 = parseFloat(document.getElementById("IBF_ActOnDate").value) || 0;
            var CtoFBF_ActOnDate = n1 + n2 + n3 + n4 + n5 + n6;
            document.getElementById("CtoFBF_ActOnDate").value = CtoFBF_ActOnDate;
        }
