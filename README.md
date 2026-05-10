<table class="table table-bordered text-center bg-white text-dark">

    <thead>
        <tr>
            <th>Material</th>
            <th>Recd.</th>
            <th>Retd.</th>
            <th style="width:250px;">Reason</th>
            <th>U/L</th>
            <th style="width:80px;">Balance</th>
        </tr>
    </thead>

    <tbody>

        <tr>
            <td class="text-start ps-1 fw-bold">LRP(FLB)</td>
            <td><input type="text" class="form-control cell"></td>
            <td><input type="text" class="form-control cell"></td>
            <td><input type="text" class="form-control cell"></td>
            <td><input type="text" class="form-control cell ul"></td>
            <td><input type="text" class="form-control cell bal"></td>
        </tr>

        <tr>
            <td class="text-start ps-1 fw-bold">LRP(IN)</td>
            <td><input type="text" class="form-control cell"></td>
            <td><input type="text" class="form-control cell"></td>
            <td><input type="text" class="form-control cell"></td>
            <td><input type="text" class="form-control cell ul"></td>
            <td><input type="text" class="form-control cell bal"></td>
        </tr>

        <tr>
            <td class="text-start ps-1 fw-bold">JODA(FLB)</td>
            <td><input type="text" class="form-control cell"></td>
            <td><input type="text" class="form-control cell"></td>
            <td><input type="text" class="form-control cell"></td>
            <td><input type="text" class="form-control cell ul"></td>
            <td><input type="text" class="form-control cell bal"></td>
        </tr>

        <tr>
            <td class="text-start ps-1 fw-bold">JODA(IN)</td>
            <td><input type="text" class="form-control cell"></td>
            <td><input type="text" class="form-control cell"></td>
            <td><input type="text" class="form-control cell"></td>
            <td><input type="text" class="form-control cell ul"></td>
            <td><input type="text" class="form-control cell bal"></td>
        </tr>

        <tr>
            <td class="text-start ps-1 fw-bold">TFO</td>
            <td><input type="text" class="form-control cell"></td>
            <td><input type="text" class="form-control cell"></td>
            <td><input type="text" class="form-control cell"></td>
            <td><input type="text" class="form-control cell ul"></td>
            <td><input type="text" class="form-control cell bal"></td>
        </tr>

        <tr>
            <td class="text-start ps-1 fw-bold">PELLET</td>
            <td><input type="text" class="form-control cell"></td>
            <td><input type="text" class="form-control cell"></td>
            <td><input type="text" class="form-control cell"></td>
            <td><input type="text" class="form-control cell ul"></td>
            <td><input type="text" class="form-control cell bal"></td>
        </tr>

        <tr>
            <td class="text-start ps-1 fw-bold">SCRAP</td>
            <td><input type="text" class="form-control cell"></td>
            <td><input type="text" class="form-control cell"></td>
            <td><input type="text" class="form-control cell"></td>
            <td><input type="text" class="form-control cell ul"></td>
            <td><input type="text" class="form-control cell bal"></td>
        </tr>

        <tr>
            <td class="text-start ps-1 fw-bold">L/STONE</td>
            <td><input type="text" class="form-control cell"></td>
            <td><input type="text" class="form-control cell"></td>
            <td><input type="text" class="form-control cell"></td>
            <td><input type="text" class="form-control cell ul"></td>
            <td><input type="text" class="form-control cell bal"></td>
        </tr>

        <tr>
            <td class="text-start ps-1 fw-bold">PYROXINITE</td>
            <td><input type="text" class="form-control cell"></td>
            <td><input type="text" class="form-control cell"></td>
            <td><input type="text" class="form-control cell"></td>
            <td><input type="text" class="form-control cell ul"></td>
            <td><input type="text" class="form-control cell bal"></td>
        </tr>

        <tr>
            <td class="text-start ps-1 fw-bold">QUARTZ</td>
            <td><input type="text" class="form-control cell"></td>
            <td><input type="text" class="form-control cell"></td>
            <td><input type="text" class="form-control cell"></td>
            <td><input type="text" class="form-control cell ul"></td>
            <td><input type="text" class="form-control cell bal"></td>
        </tr>

        <tr>
            <td class="text-start ps-1 fw-bold">NUT COKE</td>
            <td><input type="text" class="form-control cell"></td>
            <td><input type="text" class="form-control cell"></td>
            <td><input type="text" class="form-control cell"></td>
            <td><input type="text" class="form-control cell ul"></td>
            <td><input type="text" class="form-control cell bal"></td>
        </tr>

        <tr>
            <td class="text-start ps-1 fw-bold">STOCK SINTER</td>
            <td><input type="text" class="form-control cell"></td>
            <td><input type="text" class="form-control cell"></td>
            <td><input type="text" class="form-control cell"></td>
            <td><input type="text" class="form-control cell ul"></td>
            <td><input type="text" class="form-control cell bal"></td>
        </tr>

        <tr>
            <td class="text-start ps-1 fw-bold">SINTER(FLB)</td>
            <td><input type="text" class="form-control cell"></td>
            <td><input type="text" class="form-control cell"></td>
            <td><input type="text" class="form-control cell"></td>
            <td><input type="text" class="form-control cell ul"></td>
            <td><input type="text" class="form-control cell bal"></td>
        </tr>

    </tbody>

</table>

<div class="text-end mt-2">

    <strong style="margin-right:20px;">Total</strong>

    <input type="text"
           id="txtTotul"
           class="form-control d-inline-block text-center"
           style="width:100px;"
           readonly />

    <input type="text"
           id="txtTotBal"
           class="form-control d-inline-block text-center"
           style="width:100px;"
           readonly />

</div>



<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>

<script>

    $(document).ready(function () {

        // ============================
        // AUTO TOTAL
        // ============================

        $(document).on("input", ".ul, .bal", function () {

            calculateULTotal();

            calculateBalanceTotal();

        });

    });



    // ==================================
    // U/L TOTAL
    // ==================================

    function calculateULTotal() {

        let total = 0;

        $(".ul").each(function () {

            let val = parseFloat($(this).val()) || 0;

            total += val;

        });

        $("#txtTotul").val(total.toFixed(2));

    }



    // ==================================
    // BALANCE TOTAL
    // ==================================

    function calculateBalanceTotal() {

        let total = 0;

        $(".bal").each(function () {

            let val = parseFloat($(this).val()) || 0;

            total += val;

        });

        $("#txtTotBal").val(total.toFixed(2));

    }

</script>
