<div class="modal fade" id="passwordModal">
    <div class="modal-dialog">
        <div class="modal-content">

            <div class="modal-header">
                <h5>Enter Password</h5>
            </div>

            <div class="modal-body">
                <input type="password"
                       id="txtPassword"
                       class="form-control">
            </div>

            <div class="modal-footer">
                <button type="button"
                        id="btnCheckPassword"
                        class="btn btn-primary">
                    Submit
                </button>
            </div>

        </div>
    </div>
</div>
<div class="modal fade" id="deleteModal">
    <div class="modal-dialog">
        <div class="modal-content">

            <div class="modal-header">
                <h5>Confirm Delete</h5>
            </div>

            <div class="modal-body">
                Do you want to delete this row?
            </div>

            <div class="modal-footer">
                <button type="button"
                        id="btnYesDelete"
                        class="btn btn-danger">
                    Yes
                </button>

                <button type="button"
                        class="btn btn-secondary"
                        data-bs-dismiss="modal">
                    No
                </button>
            </div>

        </div>
    </div>
</div>
var selectedRow = null;

$(document).on("click", ".btnDelete", function () {

    selectedRow = $(this).closest("tr");

    $("#txtPassword").val("");

    $("#passwordModal").modal("show");
});

$("#btnCheckPassword").click(function () {

    var pwd = $("#txtPassword").val();

    $.ajax({
        url: '/Granshot/CheckPassword',
        type: 'POST',
        data: { password: pwd },
        success: function (result) {

            if (result.success) {

                $("#passwordModal").modal("hide");
                $("#deleteModal").modal("show");
            }
            else {

                alert("Invalid Password");
            }
        }
    });

});
[HttpPost]
public JsonResult CheckPassword(string password)
{
    string actualPassword = "admin123";

    return Json(new
    {
        success = (password == actualPassword)
    });
}
$("#btnYesDelete").click(function () {

    var seqNo = selectedRow.find(".seqNo").val();  // or .text() if not input

    $.ajax({
        url: '/Granshot/DeleteCast',
        type: 'POST',
        data: { seqNo: seqNo },
        success: function () {

            selectedRow.remove();
            $("#deleteModal").modal("hide");
            alert("Deleted Successfully");
        },
        error: function () {
            alert("Delete failed");
        }
    });

});
[HttpPost]
public JsonResult DeleteCast(int seqNo)
{
    string connStr = ConfigurationManager.ConnectionStrings["OracleCon"].ConnectionString;

    using (OracleConnection con = new OracleConnection(connStr))
    {
        con.Open();

        string query = "DELETE FROM YOUR_TABLE_NAME WHERE SEQNO = :seqNo";

        using (OracleCommand cmd = new OracleCommand(query, con))
        {
            cmd.Parameters.Add(new OracleParameter("seqNo", seqNo));

            int rows = cmd.ExecuteNonQuery();

            if (rows > 0)
                return Json(new { success = true });
            else
                return Json(new { success = false });
        }
    }
}
