var tonInputs = document.querySelectorAll(".ton-input");

for (var i = 0; i < tonInputs.length; i++) {

    tonInputs[i].addEventListener("blur", function () {

        var ton = parseFloat(this.value) || 0;
        var kg = ton * 1000;

        var row = this.closest("tr");
        var kgInput = row.querySelector(".kg-input");

        kgInput.value = kg.toFixed(2);
    });

}