<!DOCTYPE html>
<html lang="en">
<head>
    <title>Cast House Details</title>

    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
    <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>

    <style>
        .input-wrapper {
            display: flex;
            border: 1px solid #999;
            position: relative;
        }

        .arrow-btn {
            width: 30px;
            text-align: center;
            cursor: pointer;
            background: #f0f0f0;
        }

        .list-box {
            position: absolute;
            background: #fff;
            border: 1px solid #999;
            display: none;
            z-index: 1500;
            width: 100%;
        }

        .list-box div {
            padding: 5px;
            cursor: pointer;
        }

        .list-box div:hover {
            background: #eee;
        }

        /* 🔥 FIX */
        .modal {
            z-index: 2000 !important;
        }
        .modal-backdrop {
            z-index: 1999 !important;
        }
    </style>
</head>

<body>

<div class="container mt-3">
    <table class="table" id="Mudgun_Details">
        <tbody>
            <tr>
                <td>
                    <div class="input-wrapper">
                        <input class="form-control" id="clayInput_0" readonly>
                        <div class="arrow-btn" onclick="toggleList(0)">▼</div>

                        <div class="list-box" id="list_0">
                            <div onclick="selectItem(this,0)">ACE</div>
                            <div onclick="selectItem(this,0)">BRL</div>
                            <div onclick="selectItem(this,0)">OTHERS</div>
                        </div>
                    </div>
                </td>
            </tr>
        </tbody>
    </table>
</div>

<!-- MODAL -->
<div class="modal fade" id="clayModal" tabindex="-1">
    <div class="modal-dialog modal-dialog-centered">
        <div class="modal-content">
            <div class="modal-header bg-primary text-white">
                <h5 class="modal-title">MG CLAY</h5>
                <button class="btn-close" data-bs-dismiss="modal"></button>
            </div>
            <div class="modal-body text-center">
                Modal is working ✔
            </div>
        </div>
    </div>
</div>

@section scripts {
<script>
    var activeRowIndex = null;

    function toggleList(index) {
        $("#list_" + index).toggle();
    }

    function selectItem(el, index) {
        $("#clayInput_" + index).val(el.innerText);
        $("#list_" + index).hide();

        if (el.innerText.trim() === "OTHERS") {
            activeRowIndex = index;
            new bootstrap.Modal(document.getElementById("clayModal")).show();
        }
    }

    $(document).click(function (e) {
        if (!$(e.target).closest(".input-wrapper").length) {
            $(".list-box").hide();
        }
    });
</script>
}
</body>
</html>
