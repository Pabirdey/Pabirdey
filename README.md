success: function (res) {
    if (res.success) {

        if (bf === "BFCTRL") {
            SaveDEMOBFProdData(modelList);
        }
        else if (bf === "GBFCTRL") {
            Save_GBF_LadleData(modelList);
        }
        else if (bf === "HBFCTRL") {
            Save_HBF_LadleData(modelList);   // If you have this method
        }
        else if (bf === "IBFCTRL") {
            Save_IBF_LadleData(modelList);   // If you have this method
        }
        else {
            alert("BF Prod Save Data Successfully");
        }

    } else {
        alert(res.message);
    }
}
