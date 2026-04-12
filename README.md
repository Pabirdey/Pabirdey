 function Calc_AF_ActOnDate() {
        debugger;
        var n1 = parseFloat(document.getElementById('CBF_ActOnDate').value) || 0;        
        var n2 = parseFloat(document.getElementById('EBF_ActOnDate').value) || 0;
        var n3 = parseFloat(document.getElementById('FBF_ActOnDate').value) || 0;                
        let sum_A_F = n1 + n2 + n3;
        document.getElementById('CtoFBF_ActOnDate').value = sum_A_F;
    }
    function Calc_AG_ActOnDate() {
        debugger;
        var n4 = parseFloat(document.getElementById('GBF_ActOnDate').value) || 0;        
        var sum_A_G = Calc_AF_ActOnDate() + n4;
        document.getElementById('CtoGBF_ActOnDate').value = sum_A_G;
    }
    function Calc_AH_ActOnDate() {
        debugger;
        var n5 = parseFloat(document.getElementById('HBF_ActOnDate').value) || 0;
        var sum_A_H = Calc_AF_ActOnDate + Calc_AG_ActOnDate() + n5;
        document.getElementById('CtoHBF_ActOnDate').value = sum_A_H;
    }
    function Calc_AI_ActOnDate() {
        debugger;
        var n6 = parseFloat(document.getElementById('IBF_ActOnDate').value) || 0;
        var sum_A_I = Calc_AF_ActOnDate + Calc_AG_ActOnDate() + n6;
        document.getElementById('CtoIBF_ActOnDate').value = sum_A_I;
    }
