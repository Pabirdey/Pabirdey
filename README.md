<style>
/* ===== Global ===== */
body {
    font-family: Courier New, Courier, monospace;
}

.Main-Heading {
    font-family: Allan, cursive;
    font-weight: bold;
    font-size: 6vh;
    text-align: center;
    padding: 20px;
    color: rgb(57,57,57);
    text-shadow: rgba(13,0,77,0.08) 0px 2px 4px,
                 rgba(13,0,77,0.08) 0px 3px 6px,
                 rgba(13,0,77,0.08) 0px 8px 16px;
    border-radius: 10px;
    margin: 20px 0;
}

/* ===== Sections ===== */
.form-section {
    background: #ffffff;
    padding: 20px;
    border-radius: 20px;
    box-shadow: 0 10px 20px rgba(0,0,0,0.1);
    margin-bottom: 25px;
    border: 1px solid #ccc;
    overflow: visible;
}

.section-title,
.section_Exception-title,
.section-Drill-title {
    background: #EEB86D;
    color: black;
    padding: 5px 10px;
    font-weight: bold;
    border-radius: 10px;
    margin-bottom: 10px;
}

.section-title { font-size: 18px; }
.section_Exception-title { font-size: 15px; width: 15vh; }
.section-Drill-title { font-size: 20px; border-radius: 4px; }

/* ===== Tables ===== */
.table th,
.table td {
    text-align: center;
    vertical-align: middle;
}

th {
    font-size: 14px;
    font-weight: bold;
    border: 1px solid;
    color: white;
}

.table thead th {
    position: sticky;
    top: 0;
    z-index: 2;
    border: 1px solid;
}

.scrollable-table {
    overflow-y: auto;
}

/* Highlight Rows */
.highlight {
    background-color: yellow !important;
}

/* ===== Column Sizes ===== */
.Long_Heading { min-width: 130px; }
.Long_Heading_Medium { min-width: 100px; }
.Heading_Tiny,
.Heading_Small {
    white-space: nowrap;
}

/* ===== Inputs ===== */
.form-control-lg {
    font-size: 1.5rem;
    color: black;
}

.table-input {
    font-size: 1rem;
    padding: 2px 4px;
    border: 2px solid;
}

/* ===== Fieldset ===== */
fieldset {
    border: 2px solid #ccc !important;
    padding: 10px 12px;
}

legend {
    font-size: 24px;
    font-weight: 800;
    padding: 0 8px;
}

/* ===== Buttons ===== */
.btnSaveCastHouse {
    background: linear-gradient(to bottom right, #EF4765, #FF9A5A);
    border: 0;
    border-radius: 10px;
    color: #fff;
    font-size: 15px;
    font-weight: bold;
    line-height: 2.5;
    padding: 0 1rem;
    width: 12vh;
    margin-left: 30px;
    margin-top: 100px;
    cursor: pointer;
    transition: box-shadow .2s ease-in-out;
}

.btnSaveCastHouse:hover,
.btnSaveCastHouse:focus {
    box-shadow: 0 0 .25rem rgba(0,0,0,.5),
                -.125rem -.125rem 1rem rgba(239,71,101,.5),
                .125rem .125rem 1rem rgba(255,154,90,.5);
}

.btnHMLogistics {
    margin: 10px;
    padding: 15px 30px;
    font-weight: bold;
    color: white;
    border-radius: 10px;
    border: 0;
    background-image: linear-gradient(45deg,#FF512F 0%,#F09819 51%,#FF512F 100%);
    background-size: 200% auto;
    cursor: pointer;
    transition: 0.5s;
    box-shadow: 0px 0px 14px -7px #f09819;
}

.btnHMLogistics:hover {
    background-position: right center;
}

.btnHMLogistics:active {
    transform: scale(0.95);
}

/* ===== SweetAlert ===== */
.my-swal-popup { font-family: Arial, sans-serif; }
.my-swal-title { font-family: Georgia, serif; font-size: 22px; }
.my-swal-text { font-family: Verdana, sans-serif; font-size: 18px; }

/* ===== Mudgun Clay Custom Dropdown ===== */
.input-wrapper {
    position: relative;
    display: flex;
}

.input-wrapper input {
    border: none;
    outline: none;
}

.arrow-btn {
    position: absolute;
    right: 5px;
    top: 6px;
    width: 30px;
    text-align: center;
    cursor: pointer;
    background: #f0f0f0;
    user-select: none;
}

.list-box {
    display: none;
    position: absolute;
    background: white;
    border: 1px solid #ccc;
    width: 100%;
    max-height: 200px;
    overflow-y: auto;
    z-index: 9999;
}

.list-box div {
    padding: 6px;
    cursor: pointer;
}

.list-box div:hover {
    background: #f0f0f0;
}

/* ===== Misc ===== */
#backgrcol_Tap_hole {
    color: white;
    font-weight: bold;
    padding: 8px;
}

select {
    appearance: auto !important;
}
</style>