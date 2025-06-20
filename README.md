 function DomesticOreFinesSum() {
        var n1 = parseFloat(document.getElementById("Bacheli").value) || 0;
        var n2 = parseFloat(document.getElementById("Jaroli").value) || 0;
        var n3 = parseFloat(document.getElementById("Daitari").value) || 0;
        var n4 = parseFloat(document.getElementById("KayPeeEntp").value) || 0;
        var n5 = parseFloat(document.getElementById("AhluwaliaFines").value) || 0;
        var tot_DomesticIOF = n1 + n2 + n3 + n4 + n5;
        document.getElementById("DomesticIOF").value = tot_DomesticIOF;

    }

    function IMPOreFinesSum() {
        var n1 = parseFloat(document.getElementById("Namisa").value) || 0;
        var n2 = parseFloat(document.getElementById("CoastalFines").value) || 0;
        var n3 = parseFloat(document.getElementById("FortescueBF").value) || 0;
        var n4 = parseFloat(document.getElementById("Pilbhara").value) || 0;
        var n5 = parseFloat(document.getElementById("SnFeedValue").value) || 0;
        var n6 = parseFloat(document.getElementById("FSFVenezuelan").value) || 0;
        var n7 = parseFloat(document.getElementById("Kumba").value) || 0;
        var n8 = parseFloat(document.getElementById("KirandulFines").value) || 0;
        var n9 = parseFloat(document.getElementById("KirandulLump").value) || 0;
        var n10 = parseFloat(document.getElementById("OtherImpOre").value) || 0;
        var tot_IMPOreFines = n1 + n2 + n3 + n4 + n5 + n6 + n7 + n8 + n9 + n10;
        document.getElementById("ImpOreFines").value = tot_IMPOreFines;
    }
    
    function IOFinesSum() {
        var n1 = parseFloat(document.getElementById("NoaFines").value) || 0;
        var n2 = parseFloat(document.getElementById("JodaFines").value) || 0;
        var n3 = parseFloat(document.getElementById("KBFines").value) || 0;
        var n4 = parseFloat(document.getElementById("YardFines").value) || 0;
        var n5 = parseFloat(document.getElementById("BHJ").value) || 0;
        var n6 = parseFloat(document.getElementById("NoaCrushed").value) || 0;
        var n7 = parseFloat(document.getElementById("JodaCrushed").value) || 0;
        var n8 = parseFloat(document.getElementById("KbCrushed").value) || 0;
        var n9 = parseFloat(document.getElementById("ImpOreFines").value) || 0;
        var n10 = parseFloat(document.getElementById("DomesticIOF").value) || 0;
        var n11 = parseFloat(document.getElementById("KatamatiFines").value) || 0;
        var tot_IOFines = n1 + n2 + n3 + n4 + n5 + n6 + n7 + n8 + n9 + n10 + n11;
        document.getElementById("IronOreFines").value = tot_IOFines;
    }
    
    function MixedFluxSum() {
        var n1 = parseFloat(document.getElementById("LimestoneHISilica").value) || 0;
        var n2 = parseFloat(document.getElementById("LimestoneRPD").value) || 0;
        var n3 = parseFloat(document.getElementById("LimestoneSPGrade").value) || 0;
        var n4 = parseFloat(document.getElementById("LimestoneGotan").value) || 0;
        var n5 = parseFloat(document.getElementById("BhutanDolo").value) || 0;
        var n6 = parseFloat(document.getElementById("LimestoneHimachal").value) || 0;
        var n7 = parseFloat(document.getElementById("PyroxeniteLocal").value) || 0;
        var n8 = parseFloat(document.getElementById("PyroxeniteImp").value) || 0;
        var n9 = parseFloat(document.getElementById("PyroxeniteSukinda").value) || 0;
        var n10 = parseFloat(document.getElementById("SoapStone").value) || 0;
        var n11 = parseFloat(document.getElementById("LDSlagOs").value) || 0;
        var n12 = parseFloat(document.getElementById("LimestoneImp").value) || 0;
        var n13 = parseFloat(document.getElementById("LimestonePhilipines").value) || 0;
        var n14 = parseFloat(document.getElementById("LimestoneCPGr").value) || 0;
        var n15 = parseFloat(document.getElementById("GomardihDolo").value) || 0;
        var n16 = parseFloat(document.getElementById("Olivine").value) || 0;
        var tot_MixedFlux = n1 + n2 + n3 + n4 + n5 + n6 + n7 + n8 + n9 + n10 + n11 + n12 + n13 + n14 + n15 + n16;
        document.getElementById("MixedFlux").value = tot_MixedFlux;
    }
    
    function MixedMaterialSum() {
        var n1 = parseFloat(document.getElementById("PelletSNFines").value) || 0;
        var n2 = parseFloat(document.getElementById("GSinterFines").value) || 0;
        var n3 = parseFloat(document.getElementById("GOreFines").value) || 0;
        var n4 = parseFloat(document.getElementById("BMEndCone").value) || 0;
        var n5 = parseFloat(document.getElementById("BMPrevious").value) || 0;
        var tot_MixedMaterial = n1 + n2 + n3 + n4 + n5;
        document.getElementById("MixedMaterial").value = tot_MixedMaterial;
    }

    function TotalPilesum() {
        debugger;
        var n1 = parseFloat(document.getElementById("IronOreFines").value) || 0;     
        var n2 = parseFloat(document.getElementById("MixedFlux").value) || 0;
        var n3 = parseFloat(document.getElementById("RevertMat").value) || 0;
        var n4 = parseFloat(document.getElementById("CokeBreeze").value) || 0;
        var n5 = parseFloat(document.getElementById("MixedMaterial").value) || 0;
        var n6 = parseFloat(document.getElementById("RPC").value) || 0;
        var n7 = parseFloat(document.getElementById("JhamaCoal").value) || 0;
        var n8 = parseFloat(document.getElementById("Anthracite").value) || 0;
        //var n9 = parseFloat(document.getElementById("NoaCrushed").value) || 0;
        //var n10 = parseFloat(document.getElementById("JodaCrushed").value) || 0;
        //var n11 = parseFloat(document.getElementById("KbCrushed").value) || 0;        
        var tot_TotalPile = n1 + n2 + n3 + n4 + n5 + n6+ n7 + n8;
        document.getElementById("TotalPile").value = tot_TotalPile;
     }
