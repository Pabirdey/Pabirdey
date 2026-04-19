<div class="btn-box-wrapper">
    <div class="btn-box">

        <button type="button" class="btn btn-success btn-sm" onclick="SaveProd()">
            Save
        </button>

        <button type="button" class="btn btn-primary btn-sm" onclick="Calculate()">
            Calculate
        </button>

        <button type="button" class="btn btn-warning btn-sm" onclick="RawMatCons()">
            Raw Mat Cons
        </button>

    </div>
</div>
.btn-box-wrapper {
    display: flex;
    justify-content: center;   /* center horizontally */
    margin-top: 15px;
}

.btn-box {
    padding: 8px 12px;
    border: 1.5px solid #444;
    border-radius: 8px;
    background-color: #f8f9fa;
    box-shadow: 0 2px 6px rgba(0,0,0,0.1);

    display: flex;
    gap: 8px; /* space between buttons */
}
