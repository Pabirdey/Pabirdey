 let currentIndex = null;

            function toggleList(i) {
                document.getElementById("list_" + i).classList.toggle("show");
            }

            function selectItem(el, i) {
                let value = el.innerText;
                let input = document.getElementById("clayInput_" + i);

                input.value = value;
                document.getElementById("list_" + i).classList.remove("show");

                // ⭐ THIS IS THE FIX
                if (value === "OTHERS") {
                    currentIndex = i;
                   // document.getElementById("clayModal").value = "";
                    let modal = new bootstrap.Modal(document.getElementById("clayModal"));
                    modal.show();
                }
            }
