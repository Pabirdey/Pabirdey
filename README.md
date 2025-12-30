<script>
document.addEventListener("click", function(e){

    let row = e.target.closest("tr");
    if(!row) return;

    let castCell = row.querySelector(".cast");
    if(!castCell) return;

    let castNo = castCell.innerText.trim();

    document.querySelectorAll("tr").forEach(r => r.classList.remove("highlight"));

    document.querySelectorAll(".cast").forEach(td => {
        if (td.innerText.trim() === castNo) {
            td.parentElement.classList.add("highlight");
        }
    });

});
</script>