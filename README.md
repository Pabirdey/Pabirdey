document.querySelectorAll(".a, .b, .c, .d, .e, .f, .bunker") .forEach(el => { el.addEventListener("input", function () { let row = this.closest("tr"); calculateRow(row); }); });
