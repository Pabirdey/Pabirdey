function toggleList(i){
    $(".list-box").hide();
    $("#list_"+i).toggle();
}
function selectItem(el, i){
    let val = el.innerText.trim();
    if(val === "OTHERS"){
        $("#hdnRowIndex").val(i);
        $("#txtOtherMGClay").val('');
        let modalEl = document.getElementById("mgClayOtherModal");
        let modal = new bootstrap.Modal(modalEl);
        modal.show();
        return;
    }
    $("#clayInput_"+i).val(val);
    $("#list_"+i).hide();
}
