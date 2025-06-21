  function DisplayPswBlock() {
        debugger;
        var source = document.getElementById("SourceSelect").value;
        var block1 = document.getElementById("pswBlock1");
        var block2 = document.getElementById("pswBlock2");
        var block3 = document.getElementById("pswBlock3");
        var block4 = document.getElementById("pswBlock4");
        if (source === 'RMBB_KNR') {
            block1.style.display = "block1";
            block2.style.display = "block2";
            block3.style.display = "block3";
            block4.style.display = "block4";
        } else {
            block1.style.display = "none";
            block2.style.display = "none";
            block3.style.display = "none";
            block4.style.display = "none";
        }
    }
